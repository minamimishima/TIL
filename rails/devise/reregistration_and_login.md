# Deviseで退会処理
## やりたいこと
- 論理削除での退会
- 退会したユーザーの再登録
- 再登録したユーザーのログイン
<br>

## 【論理削除】
### やりたいこと
- 論理削除で退会

### 方法
- usersテーブルにis_deletedカラム作成
<br>

- withdrawalアクション作成  

app/controllers/users_controller.rb
```
def withdrawal
  @user.update(is_deleted: true)
  reset_session
  flash[:notice] = "退会しました"
  redirect_to root_path
end
```
<br>

- confirmアクション、ビュー作成  

app/controllers/users_controller.rb
```
def confirm
end
```
app/views/users/confirm.html.erb
```
 退会手続きをされますと全てのサービスがご利用いただけなくなります。<br>
 再度ご利用いただく場合には新規登録のお手続きが必要になります。<br>
 本当に退会してよろしいですか？
 <%= link_to "退会する", withdrawal_users_path,
     data: { turbo_method: :patch, turbo_confirm: "本当に退会しますか？" } %>
 <%= link_to "退会しない（プロフィールに戻る）", user_path(@user) %>
```
<br>

- `active_for_authentication?`メソッドをオーバーライド

app/models/user.rb
```
def active_for_authentication?
  super && (is_deleted == false)
end
```

### 参考
- [【Rails】 退会機能を論理削除で実装する](https://qiita.com/__Wata16__/items/9e05596afb671e540365)
- [Rails 退会機能実装](https://zenn.dev/goldsaya/articles/ee812461bbea6b)

<br>

## 【退会したユーザーの再登録】
### やりたいこと
- 退会したユーザーが同じメールアドレスで再登録できるようにする  
（論理削除で実装しているためレコード自体は残っており、再登録しようとすると「メールアドレスはすでに存在します」というエラーが出る）

### 方法
- マイグレーションファイルの作成
```
class RemoveEmailIndexFromUsers < ActiveRecord::Migration[7.1]
  def change
    remove_index :users, :email
  end
end
```
<br>

- モデルファイルの編集  

app/models/user.rb
```
validates :email, presence: true, if: :devise_will_save_change_to_email?
validates :email, uniqueness: { scope: :is_deleted, if: -> { is_deleted == false } } # rubocop:disable Rails/UniqueValidationWithoutIndex
validates :email,
  format: { with: /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/, case_sensitive: true, if: :devise_will_save_change_to_email? }

validates :password, presence: true, if: :password_required?
validates :password, confirmation: true, if: :password_required?
validates :password, length: { within: 8..30 }, if: :password_required?

...

protected

def password_required?
  !persisted? || !password.nil? || !password_confirmation.nil?
end

def email_required?
  true
end
```

### ハマった箇所
- deviseのソースコードのコピペ（rails7仕様に書き方は整えた）だとプロフィール編集時に「パスワードは8文字以上で入力してください」とエラーが出るようになった

### 解決策
```
validates :password, length: { within: 8..30 }, if: :password_required?
```
パスワードの長さのバリデーションにもifを追加  
一度パスワードのバリデーションからifを消したところ「パスワードを入力してください」のエラーも表示されたため長さの部分のみが引っかかってることに気づいた

### 参考
- [Railsガイド](https://railsguides.jp/active_record_migrations.html#change%E3%83%A1%E3%82%BD%E3%83%83%E3%83%89%E3%82%92%E4%BD%BF%E3%81%86)
- [Deviseの設定手順をまとめてみた。 その4　ユーザーIDで、ログイン認証編](https://qiita.com/growthcoding/items/385d3cd539fc7578b52a)  
- [Rails｜退会処理済み会員が再度新規登録できるようにする方法](https://zenn.dev/airiin/articles/023fc13679e607)

<br>

## 【再登録したユーザーのログイン】
- `find_for_authentication`のオーバーライド

app/models/user.rb
```
def self.find_for_authentication(tainted_conditions)
  conditions = devise_parameter_filter.filter(tainted_conditions)
  conditions[:is_deleted] = false
  to_adapter.find_first(conditions)
end
```
<br>

- reject_deleted_userメソッドを作成しbefore_actionに設定  

app/controllers/users/sessions_controller.rb
```
before_action :reject_deleted_user, only: [:create]

def reject_deleted_user
  user = User.where(email: params[:user][:email])
  user_status = user.pluck(:is_deleted)
  if user.present? && user_status.all? { |is_deleted| is_deleted == true }
    flash[:alert] = "退会済みです。再度登録をしてご利用ください。"
    redirect_to new_user_registration_path
  end
end
```
<br>

- ルーティング編集
```
devise_for :users, controllers: {
  sessions: 'users/sessions'
}
```

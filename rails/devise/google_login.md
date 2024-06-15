## Googleログインの実装

### やりたいこと
- Googleでログインできるようにする

### 方法

1. Google APIの設定  
  - OAuth同意画面の構成  
  - クライアントIDの取得  
<br>

2. gemのインストール
```
gem "omniauth"
gem "omniauth-google-oauth2"
gem "omniauth-rails_csrf_protection"
```
<br>

3. 各種設定  

app/models/user.rb  
```
devise :database_authenticatable, :registerable,
       :recoverable, :rememberable, :omniauthable, omniauth_providers: [:google_oauth2] #omniauthable以降を追加
```
<br>

config/initializers/devise.rb  
```
config.omniauth :google_oauth2, ENV['GOOGLE_CLIENT_ID'], ENV['GOOGLE_CLIENT_SECRET']
```
<br>

config/routes.rb  
```
Rails.application.routes.draw do
  devise_for :users, controllers: {
    registrations: "users/registrations",
    sessions: "users/sessions",
    omniauth_callbacks: "users/omniauth_callbacks" #ここを追加
  }
```
<br>

4. コールバック用コントローラの作成
```
class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController
  def google_oauth2
    @user = User.from_omniauth(request.env['omniauth.auth'])

    if @user.persisted?
      flash[:notice] = I18n.t 'devise.omniauth_callbacks.success', kind: 'Google'
      sign_in_and_redirect @user, event: :authentication
    else
      session['devise.google_data'] = request.env['omniauth.auth'].except('extra') # Removing extra as it can overflow some session stores
      redirect_to new_user_registration_url, alert: @user.errors.full_messages.join("\n")
    end
  end
end
```  

ポイント：Deviseのコントローラを継承する  
【参考】https://github.com/zquestz/omniauth-google-oauth2?tab=readme-ov-file#devise  
<br>

5. app/models/user.rb
```
def self.from_omniauth(auth)
  find_or_create_by(provider: auth.provider, uid: auth.uid) do |user|
    user.email = auth.info.email
    user.password = Devise.friendly_token[0, 20]
    user.name = auth.info.name
  end
end
```
【参考】https://github.com/heartcombo/devise/wiki/OmniAuth:-Overview#facebook-example  
<br>

6. ログインボタン
```
<%= button_to 'Login with Google', user_google_oauth2_omniauth_authorize_path, method: :post, data: { turbo: "false" } %>
```
ポイント：`data: { turbo: "false" }`
<br>
<br>

### 【参考】
[Devise: OmniAuth: Overview](https://github.com/heartcombo/devise/wiki/OmniAuth:-Overview#facebook-example)  
[omniauth-google-oauth2: Devise](https://github.com/zquestz/omniauth-google-oauth2?tab=readme-ov-file#devise)  
[公式ドキュメント](https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid?hl=ja)  
[【Rails7】Googleログインを公式ドキュメントに沿って実装する](https://zenn.dev/yoiyoicho/articles/c44a80e4bb4515)  
[Google Login in Rails 7 with devise](https://dev.to/ahmadraza/google-login-in-rails-7-with-devise-2gpo)  
[【Rails7】WebアプリにGoogleアカウントでログイン](https://qiita.com/tanigawa0930/items/9b0985f364333df356dd)

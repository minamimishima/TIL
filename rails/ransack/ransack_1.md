# ransackで検索機能を実装①

【やりたいこと】

- 動画メモから検索
- ログイン中のユーザーのデータの中からのみ検索

<br>

【方法】
- 動画メモから検索


```
def self.ransackable_attributes(auth_object = nil)
  ["description"]
end
```
<br>

- scopeの設定

```
scope :by_user, -> (user) { where(user_id: user.id) }
```

```
def self.ransackable_scopes(auth_object = nil)
  [:by_user]
end
```
<br>

- コントローラ

```
@q = Bookmark.by_user(@user).latest.ransack(params[:q])
@bookmarks = @q.result(distinct: true).page(params[:page])
```
<br>

【参考】

[公式ドキュメント](https://activerecord-hackery.github.io/ransack/going-further/other-notes/)  

[Ransackで簡単に検索フォームを作る73のレシピ](https://nekorails.hatenablog.com/entry/2017/05/31/173925)

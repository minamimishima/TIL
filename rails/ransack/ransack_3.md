# ransackで検索機能を実装③

【やりたいこと】

- 昇順・降順を固定したリンクを作りたい

(`<%= sort_link(@q, :created_at, "Created at") %>`⁠でできるリンクはクリックするたびに昇順・降順が切り替わるタイプ)
  
<br>

【方法】
- ログを見てみる
![スクリーンショット 2024-05-30 22 21 44](https://github.com/minamimishima/TIL/assets/146907532/b64b1810-32c0-4587-abdd-d0d3ebfd841f)

 `Parameters: {"q"=>{"s"=>"created_at desc"}}` というパラメータが送られている

- 上記のパラメータを手動で送る

```
<%= link_to "新しい順", bookmarks_path("q"=>{"s"=>"created_at desc"}) %>
|
<%= link_to "古い順", bookmarks_path("q"=>{"s"=>"created_at asc"}) %>
```

  

【参考】  
[ransackやkaminariで任意のパラメータを送る方法](https://qiita.com/Kashiwara/items/4d02c94d3f974cf69e85)

## 戻るボタンで複数ページ移動する
### やりたいこと
- 戻るボタンを実装し、複数ページ戻れるようにする

### 問題
```
<%= link_to "戻る", :back %>
```
上記の記述だとループしてしまう  
（`bookmarks/show`, `bookmarks/edit`の2ページに上記の戻るリンクを実装していたが、`index`→`show`→`edit`と進んで`edit`で戻るボタンを押すと`show`に戻り、`show`で戻るを押すと`edit`に戻ってしまいループに入る

### 解決策
```
<%= link_to "戻る", "javascript:history.back()" %>
```
これで来た順に戻れる

### 参考
- [History: back() メソッド](https://developer.mozilla.org/ja/docs/Web/API/History/back)
- [【Rails】戻るボタンの実装方法【複数ページ戻ることも可能】](https://qiita.com/nekojoker/items/cb662de7cbb65e438985)

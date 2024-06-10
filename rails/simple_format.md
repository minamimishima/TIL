## simple_format
### やりたいこと
- 表示に改行を反映したい  


### 方法
```
<%= simple_format(h(@user.profile)) %>
```  
`h()`オプションはHTMLタグのエスケープのために付けている

### 参考
- [【Rails】simple_formatとは](https://qiita.com/mmaumtjgj/items/1b672f3accd37387b2f3)
- [【Rails/simple_format】フォームで入力した改行を反映させるヘルパーメソッド](https://qiita.com/saitok7/items/5754aea53ec79a413cd7)

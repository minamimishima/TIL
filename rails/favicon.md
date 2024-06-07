## faviconの設定
### やりたいこと
- faviconを設定する

### 方法
- favicon用の画像を作成  
- `app/assets/images`内に保存  

- ビューファイルへの記述  
app/views/layouts/application.html.erb  
head内に`<%= favicon_link_tag('favicon.ico') %>`を記述  

### 参考
[【Rails】アプリにファビコン(favicon)を設定しよう](https://qiita.com/mihooo24/items/380cc2b9c6980bfd0bfa)

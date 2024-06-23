## ページタイトルを動的に表示
### やりたいこと
- ページタイトルを動的に表示  

### 方法
- app/helpers/application_helper.rb
```
module ApplicationHelper
  def page_title(title)
    base_title = "推しTube"
    title.empty? ? base_title : title + " | " + base_title
  end
end
```

- app/views/layouts/application.html.erb  
```
<title><%= page_title(yield(:title)) %></title>
```

- ビューファイルの頭に下記の記述を追加  
```
<% content_for(:title, @category.name) %> #第2引数はページタイトル（この場合はカテゴリー名）
```

### 参考
- [Railsガイド](https://railsguides.jp/layouts_and_rendering.html#yield%E3%82%92%E7%90%86%E8%A7%A3%E3%81%99%E3%82%8B)
- [[Rails]タイトルを動的に出力する14/20](https://zenn.dev/redheadchloe/articles/ce0e1c43e35cd0)

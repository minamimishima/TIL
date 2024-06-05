# ransackで検索機能を実装②

【やりたいこと】

- 動画メモ、動画タイトルから検索（動画タイトルを追加）
  
<br>

【方法】

- bookmarkモデルにvideo_titleを追加
- ブックマーク登録時にvideo_titleを登録
- app/models/bookmark.rb

```
def self.ransackable_attributes(auth_object = nil) # rubocop:disable all
  ["description", "video_title"] #video_titleを追加 
end
```

```
def self.ransackable_associations(auth_object = nil)
  []
end
```

video_titleを追加したらこれも追加しないと`ActionView::Template::Error`が出てしまった   
associationも定義してね、ということらしい…  
  

- app/views/shared/_search.html.erb

```
<%= search_form_for q do |f| %>
  <%= f.search_field :description_or_video_title_cont, class: "form-control mb-2", autofocus: true %>
  <%= f.submit "検索", class: "search__button btn shadow-sm" %>
<% end %>
```

`description_or_video_title_cont` に変更

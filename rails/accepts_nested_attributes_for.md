## やりたいこと
- Userモデルに紐づいた画像を削除したい(Active Storageを使用)

### 方法
- app/models/user.rb
```
has_one_attached :icon
accepts_nested_attributes_for :icon_attachment, allow_destroy: true
```

- app/controllers/users_controller.rb
```
def profile_params
  params.require(:user).permit(
    :name,
    :profile,
    :icon,
    icon_attachment_attributes: [:id, :_destroy]
    )
end
```

- app/views/users/profile_edit.html.erb
```
<%= f.fields_for :icon_attachment do |icon| %>
  <%= icon.check_box :_destroy %>
<% end %>
```

### icon_attachmentについて
この場合の`icon_attachment`はActive Storageが自動的に生成する名前  
コンソールで確認できる
```
User.reflect_on_all_associations(:has_one).map(&:name)
```

### 参考
- [fields_forを使って親子関係にあるモデルのレコードを一度に編集・削除する](https://qiita.com/mnmnm_37/items/b78651500e61176b94c6)
- [モデルのアソシエーション情報を調べる](https://qiita.com/yusuke-matsuda/items/9af5e90dc4079e9d9548)

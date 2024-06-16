## 画像のバリデーションが有効か確認するテストの作成
### やりたいこと
- 下記のカスタムバリデーションが有効かどうか確認(Active Storageを使用)
```
validate :check_icon_format

def image?
  ["image/jpg", "image/jpeg", "image/gif", "image/png"].include?(icon.content_type)
end

def check_icon_format
  if icon.present? && !image?
    icon.purge
    errors.add(:base, "アップロードできる画像形式はjpg, jpeg, gif, pngのみです")
  end
end
```

### 方法
- `fixture_file_upload`を使用

```
it "アイコン画像の拡張子がjpg, jpeg, gif, pngであれば有効であること" do
  extensions = ["jpg", "jpeg", "gif", "png"]
  aggregate_failures do
    extensions.each do |ext|
      user = build(:user, icon: fixture_file_upload("spec/fixtures/test.#{ext}"))
      expect(user).to be_valid
    end
  end
end
```

## 参考
- [fixture_file_uploadメソッドを使用してテストコードを書く](https://qiita.com/orange159159/items/f32b4c364071b1f43cb2)

## 画像が表示されていることをaltを使用して検証

### やりたいこと
- 画像が表示されているかをテストしたい

### 方法
- alt属性を使って画像が表示されているか確認する

```
it "画像が表示されること" do
  visit bookmark_path(bookmark)
  expect(page).to have_selector "img[alt='画像']"
end
```

### 参考
- [RSpecでimgタグのオプションをテストする(alt, srcなど)](https://qiita.com/koki0527/items/26389de0497762527244)

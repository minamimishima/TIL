## 画像を変形する
### やりたいこと
- Active Storageを使用してアタッチした画像を変形し、任意のサイズで表示する

### 方法
- `libvips`のインストール  

Dockerfileに下記を追記
```
RUN apt-get install -y libvips
```

- `image_processing`のインストール

Gemfileに下記を追記
```
gem "image_processing"
```
bundle install

- ビューファイルの変更
```
<%= image_tag @user.icon.variant(resize_to_limit: [150, 150]) %>
```

### 参考
- [Railsガイド](https://railsguides.jp/v7.1/active_storage_overview.html#%E7%94%BB%E5%83%8F%E3%82%92%E5%A4%89%E5%BD%A2%E3%81%99%E3%82%8B)
- [【Rails】Active Storageについて](https://zenn.dev/meimei_kr/articles/571d350dabfc7e)

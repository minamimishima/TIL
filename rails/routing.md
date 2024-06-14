## ルーティング
- メンバールーティング(idが必要な場合)
```
resources :photos do
  member do
    get 'preview'
  end
end
```
メンバールーティングが1つしかない場合は`:on`オプションを使用することでブロック省略可
```
resources :photos do
  get 'preview', on: :member
end
```

- コレクションルーティング(idが不要な場合)
```
resources :photos do
  collection do
    get 'search'
  end
end
```
コレクションルーティングが1つしかない場合は`:on`オプションを使用することでブロック省略可
```
resources :photos do
  get 'search', on: :collection
end
```

### 参考
- [Railsガイド](https://railsguides.jp/routing.html#restful%E3%81%AA%E3%82%A2%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%92%E3%81%95%E3%82%89%E3%81%AB%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B)

## CSS 適用範囲
- クラス名をカンマで区切る  
複数クラスに対して同じスタイルを適用
```
.child1, .child2 {
  ...
}
```
`child1とchild2`の2つに適用

- クラス名を半角スペースで区切る
適用範囲の絞り込み
```
.parent .child {
  ...
}
```
`parentの中のchild`に適用される

- クラス名をつなげて記述
両方のクラスに属する要素のみに適用
```
.p1.child {
  ...
}
```
`p1とchildの両方を持つ要素`に適用される

### 参考
- [【HTML・CSS】class属性を複数指定するには？CSSセレクタを並べる方法もサンプルコードで解説](https://web-camp.io/magazine/archives/87658)

## ハッシュとシンボルについて
- 文字列をハッシュのキーにした場合
```
currencies = { 'japan' => 'yen', 'us' => 'dollar', 'india' => 'rupee' }
```
この場合、日本の通貨を取得したければ`currencies['japan']`

- シンボルをハッシュのキーにした場合
```
currencies = { 'japan': 'yen', 'us': 'dollar', 'india': 'rupee' }
```
この場合、日本の通貨を取得したければ`currencies[:japan]`  

これは下記の書き換え
```
currencies = { :japan => 'yen', :us => 'dollar', :india => 'rupee' }
```

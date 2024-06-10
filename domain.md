## アプリのカスタムドメイン名の設定
### やりたいこと
- お名前.comで取得した独自ドメインをherokuで使用する

### 事前準備
- お名前.comでドメイン取得  
- Cloudflareのアカウント作成

### 手順
1. heroku SSL certificateの設定
`Automatic Certificate Management (ACM)`に設定

![7B64B979-ADD4-466C-990F-F49CE19258C9](https://github.com/minamimishima/TIL/assets/146907532/4c0f7907-a9b6-44ec-9b09-567b24bfa794)

<br>

2. herokuにドメイン追加
```
heroku domains:add oshitube.com
heroku domains:add www.oshitube.com
```
```
heroku domains:wait oshitube.com
heroku domains:wait www.oshitube.com
```
`heroku domains`で表示されるDNS Targetをコピーしておく

![E7B6CCFB-0425-4BDE-9C63-CEC264DE0DBE_4_5005_c](https://github.com/minamimishima/TIL/assets/146907532/04c4e7dc-7f6f-4958-9e39-7636e9272b53)

<br>

3. ClowdflareのDNS設定  
    - ドメイン名を登録 今回は`oshitube.com`
    - `CNAME`でDNS Targetを登録

![DE6228D0-32D5-497C-B248-ED8CE6B564EE_1_201_a](https://github.com/minamimishima/TIL/assets/146907532/0d1d1d0b-f415-4d33-9452-b8e883c6d6c6)

<br>

4. お名前.comの設定変更  
CloudflareのDNSサーバーを使用する

![B51287B6-0AA1-43AD-9DB6-936BFDEFC673_1_201_a](https://github.com/minamimishima/TIL/assets/146907532/318a2551-2ca3-4dd9-816a-d51b215ab773)


以上で反映されるはず！  

<br>

### 用語
- `DNS(Domain Name System)`  
ドメインをIPアドレスに変換する仕組み  
インターネットの電話帳のようなもの  


### 参考
- [アプリのカスタムドメイン名](https://devcenter.heroku.com/ja/articles/custom-domains)
- [Configure Cloudflare and Heroku over HTTPS](https://developers.cloudflare.com/support/third-party-software/others/configure-cloudflare-and-heroku-over-https)
- [Cloudflareで取得した独自ドメインをHerokuで設定する方法](https://qiita.com/MIDO-ruby7/items/d846e4728b9800a045e6)
- [Herokuとお名前.comでサブドメインなしの独自ドメインを使う方法](https://zenn.dev/fj68/articles/12a2e514a221fa)

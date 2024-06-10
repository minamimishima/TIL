## アプリのカスタムドメイン名の設定
### やりたいこと
- お名前.comで取得した独自ドメインをherokuで使用する

### 事前準備
- お名前.comでドメイン取得  
- Cloudflareのアカウント作成

### 手順
1. heroku SSL certificateの設定  
`Automatic Certificate Management (ACM)`に設定

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

3. ClowdflareのDNS設定  
    - ドメイン名を登録 今回は`oshitube.com`
    - `CNAME`でDNS Targetを登録  

4. お名前.comの設定変更  
CloudflareのDNSサーバーを使用する  
<br>
以上で反映されるはず！

### 用語
- `DNS(Domain Name System)`  
ドメインをIPアドレスに変換する仕組み  
インターネットの電話帳のようなもの  


### 参考
- [アプリのカスタムドメイン名](https://devcenter.heroku.com/ja/articles/custom-domains)
- [Configure Cloudflare and Heroku over HTTPS](https://developers.cloudflare.com/support/third-party-software/others/configure-cloudflare-and-heroku-over-https)
- [Cloudflareで取得した独自ドメインをHerokuで設定する方法](https://qiita.com/MIDO-ruby7/items/d846e4728b9800a045e6)
- [Herokuとお名前.comでサブドメインなしの独自ドメインを使う方法](https://zenn.dev/fj68/articles/12a2e514a221fa)

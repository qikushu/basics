## apacheの設定
### cgi.load モジュールを読み込むようにする
mods-availableのcgi.loadを mods-enableにシンボリックリンクをはる。
```
sudo ln -s /etc/apache2/mods-available/cgi.load /etc/apache2/mods-enabled/cgi.load
```

### siteにcgiの利用を許可
sites-available/000-default.confの以下のコメントを外す
```
#Include conf-available/serve-cgi-bin.conf
```
000-defaultだとサイト全体に効く

### 必要な拡張子を追加
`mods-available/mime.conf`を編集。以下をコメントアウト後、.py .plとか
```
#AddHandler cgi-script .cgi
```



site-available にサイトごとにconfをかく

site-enabled にsite-availableのシンボリックリンクを作って活性化する



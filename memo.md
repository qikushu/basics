### apacheの設定
cgi.loadを活性化 mods-availableのcgi.loadを mods-enableにシンボリックリンクをはる。
```
sudo ln -s /etc/apache2/mods-available/cgi.load /etc/apache2/mods-enabled/cgi.load
```

sites-available/000-default.confの以下のコメントを外す
```
#Include conf-available/serve-cgi-bin.conf
```

必要な拡張子を追加する .py .plとか
```
#AddHandler cgi-script .cgi
```



site-available にサイトごとにconfをかく

site-enabled にsite-availableのシンボリックリンクを作って活性化する



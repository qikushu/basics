## apache cgi使えるように

```
# モジュール有効化 (シンボリックリンクをはってるそうな)
sudo a2enmod cgid
sudo a2enmod userdir
sudo a2enmod include
systemctl restart apache2
```

`conf-available/cgi-enabled.conf`を新規作成
```
<Directory "/home/*/public_html">
    Options +ExecCGI
    AddHandler cgi-script .cgi .pl .py .rb
</Directory>
```
その後以下を実行
```
sudo a2enconf cgi-enabled
sudo systemctl restart apache2
```

### ファイルのパーミッション
```
chmod 755 test.pl
```




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



### トラブルシューティング
```
sudo less /var/log/apache2/error.log
sudo less /var/log/apache2/access.log
```

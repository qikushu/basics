## apache cgi使えるように

```
# モジュール有効化 (シンボリックリンクをはってるそうな)
sudo a2enmod cgid
sudo a2enmod userdir
sudo a2enmod include
sudo apt install apache2-suexec-custom
sudo a2enmod suexec
sudo systemctl restart apache2

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
chrmod 755 dir
```


### トラブルシューティング
```
sudo less /var/log/apache2/error.log
sudo less /var/log/apache2/access.log
```

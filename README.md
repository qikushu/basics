## ベル音がうるさい

#### Powershellにてベル音を消す
```
## Powershellを管理者として実行
# 実行権限を付与 (恒久的
Set-ExecutionPolicy RemoteSigned

## いったんとじる

#　普通にPowershellを起動
## 場所を調べる
$profile
## 調べたフォルダを作成、今回の例
mkdir C:\Users\user\Documents\WindowsPowerShell
# 編集
notepad $profile
# 以下を書き込んで閉じる
Set-PSReadlineOption -BellStyle None
#　Powershellを再起動
```

#### bash on windowsでベル音を消す
```
echo "set bell-style none" >> ~/.inputrc
# シェルを再起動
```


#### bash on windows の vim でベル音を消す
```
echo "set visualbell t_vb=" >> ~/.vimrc
# シェルを再起動
```

## 美しいターミナルで仕事をする
#### Windows PowerShellの色を調整する 1
```
# 下記のURLからColorTool.zipをブラウザでおとして解凍する。
https://github.com/microsoft/terminal/releases/tag/1904.29002
# PowerSHellを開いて解凍して現れたColorTool.exeを実行する
C:\Users\user\Downloads\ColorTool\ColorTool.exe -s
# よさそうなやつを選んで決定
C:\Users\user\Downloads\ColorTool\ColorTool.exe -d OneHalfLight.itermcolors
# (ここが一番大事) PowerShellの規定値を選んで、画面を表示し、なにも変更することなくOKをおす。
## 再起動
```
このままでは bash on windowsにログインしたときに、フォルダがすごく見づらいので調整する

#### Windows PowerShellの色を調整する2
```
# WSL
bash
# LS_COLORS変数をparseして整形してくれるdiscolorを用いる
# -pオプションで成形し、~/.discolors に保存
discolor -p > ~/.discolors
# viで開いて訂正する
vi ~/.discolors
# OTHER_WRITABLE 34;42
# を
# OTHER_WRITABLE 01;32
# に変更する

# .bashrcに以下を追加
# eval $(dircolors -b ~/.dircolors)

# シェルを再起動
```
 
## rsync　　サーバー間通信の場合

サーバー間通信の時には、ディレクトリごと指定すると、ファイルの転送サイズが巨大化し、通信がタイムアウトになる可能性がある。
ファイルごとrsyncを実行することにした。nohupなどしてほったらかした後、あとでのこのこ来た時に、転送に失敗したファイルは残っている。
もう一度同じコマンドを実行すると、続きからアップロードしてくれる。

```
rsync -auvz --remove-source-files --partial --progress file dir/

-a コピー元のディレクトリを再帰的にオーナー・グループ・パーミッション・タイムスタンプをそのままコピーします。オプション -rlptgoD と同じ。
-u コピー元とコピー先を比較し、追加・更新されたファイル・ディレクトリのみをコピーします。
-v で詳細を出力する。
-z 圧縮して転送
--remove-source-file  転送後に転送元から削除
--partial 転送が中断したファイルを、途中から転送する。
```

## RAID
状態チェック
```
cat /proc/mdstat
```
状態チェック2
```
mdadm -D /dev/md0
```

そもそものRAID構成を確認する
```
blkid
mdadm --detail --scan
```


故障ディスク除去
```
mdadm /dev/md0 -r /dev/sdd1
```
新規ディスク追加
```
mdadm /dev/md0 --add /dev/sdd1
# チェック
mdadm -D /dev/md0

```

状態チェック
```
cat /proc/mdstat
```
UUIDはどうなるのだろうか

# ベル音がうるさい

### Powershellにてベル音を消す
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

### bash on windowsでベル音を消す
```
echo "set bell-style none" >> ~/.inputrc
# シェルを再起動
```


### bash on windows の vim でベル音を消す
```
echo "set visualbell t_vb=" >> ~/.vimrc
# シェルを再起動
```

# 美しいターミナルで仕事をする
### Windows PowerShellの色を調整する 1
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

### Windows PowerShellの色を調整する2
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






# basics

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

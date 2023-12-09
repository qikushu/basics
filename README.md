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


### あるディレクトリ以下のファイルあるいはディレクトリをリードオンリーにする
```
# ディレクトリの場合
find /path/to/directory -type d -exec chmod a-w {} \;
# ファイルの場合
find /path/to/directory -type f -exec chmod a-w {} \;
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
```
#状態チェック
cat /proc/mdstat
#状態チェック2
mdadm -D /dev/md0
#そもそものRAID構成を確認する
blkid
mdadm --detail --scan
#故障ディスク除去
mdadm /dev/md0 -r /dev/sdd1
#新規ディスク追加
mdadm /dev/md0 --add /dev/sdd1
# チェック
mdadm -D /dev/md0
#状態チェック
cat /proc/mdstat
```

## jbrowse2
Do not run below commands at your jbrowse2 directory
```
wget ref.fa.gz
gunzip ref.fa.gz
samtools faidx ref.fa
jbrowse add-assembly ref.fa --load copy --name mygenome1 --out /jbrowse2/insatall/dir

wget mygenome.gff.gz
gunzip mygenome.gff.gz
git clone https://github.com/billzt/gff3sort.git
gff3sort/gff3sort.pl mygenome.gff > bgzip -c mygenome.sorted.gff.gz
jbrowse add-track mygenome.gff.gz --load copy --name myanno --assemblyNames mygenome1 --out /jbrowse2/insatall/dir

# for confirmation
jbrowse admin-server

jbrowse upgrade
```

## pdftoppm
```
pdftoppm -png -singlefile A.pdf B
```

## 染色体ごとにじっこうしたいとき
```
for i in 01 02 03 04 05 06 07 08 09 10 11 12 ; do
 echo ${i}
done
```

## blast関係
```
## タンパク質
# database構築
makeblastdb -in protein.fa -dbtype prot
# blastp
blastp -query protein.fa -db db_prot.txt -evalue 1e-12 -out out.txt

# 塩基配列
makeblastdb -in nuc.fa -dbtype nucl
blastn -query query.fa -db nuc.fa -evalue 1e-12 -out out.txt -outfmt 6 -dust no
```

## ワークショップ等お世話
### 名札作成
名刺サイズが汎用性が高く、一般的な名札ケースにぴったり入る可能性が最も高い。今回は専用用紙は買わず、ケント紙で印刷を考える。

#### エクセルでリスト作成 (追加で何でも入れてよい)
+ ワークショップ名
+ 所属
+ 名前
+ その他属性 (一般、学生、講演者等)

#### Wordの差し込み文書機能を使った印刷
1. 差し込み印刷の開始 => ラベル を選択
2. A-ONE 51275 (A4版10面 (名刺サイズ (厚口))を選択
3. 宛先の選択、既存のリストを利用、当該エクセルファイルを選択
4. アドレス帳の編集で、印刷したいひとを選択する。
5. 差し込みフィールドの挿入で、印刷したい項目を選択する。左上の一枚目の名詞にのみフィールドが入る。
6. 適当に文字の大きさや場所などを調整する。Shift+改行で行方向には空白を入れる。
7. よければ、のこりの7枚にコピペで貼る。<<New recode>>の表記はプレビューには出てこない
8. プレビューで確認
9. 良ければいったん保存
10. 完了と差し込み、個々のドキュメントの編集
11. 印刷



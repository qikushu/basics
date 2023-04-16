## NGSデータをDRAで登録するときのメモ



Prefix | Object | 説明
--- | --- |--- 
BioProject | PRJD | 研究のゴールを説明し、関連するDRAとデータをまとめる
BioSample | SAMD | サンプルの情報
DRX | Experiment | Biosampleをどのように解読したのか
DRR | Run | 配列データ

BioProject 1 vs 多 Experimentの関係で紐づけられます
Experiment を介して、Biosample 1 vs 多 Run の関係で紐づけられます
Run 1 vs 多 Run_file (fastq) の関係で紐づけられます  


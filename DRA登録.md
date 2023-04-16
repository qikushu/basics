## NGSデータをDRAで登録するときのメモ



Prefix | Object | 説明
--- | --- |--- 
BioProject | PRJD | 研究のゴールを説明し、関連するDRAとデータをまとめる
BioSample | SAMD | サンプルの情報
DRX | Experiment | Biosampleをどのように解読したのか
DRR | Run | 配列データ

Submission 1 vs 多 Experiment (Biosample)の関係で紐づけられますExperiment
(Biosample) 1 vs 多 Run の関係で紐づけられます  Run 1 vs 多 Run_file (fastq) の関係で紐づけられます  


を読もうかな！という動機に相当します。Runは実際にシーケンサーの1runです
あれ、もうちょっと読もうかな、ということで、Runは複数回の可能性があります。
1回のRunの結果、複数ファイルのfastqが生成される場合がありますので、1 vs 多の関係で

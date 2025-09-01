🃏 MLカード No.2 – Pandas 基本編

📌 テーマ：info()（データの概要確認）

🔹 説明

info() は、データの全体像をざっくり把握するための関数。
カラム数・データ型・欠損値の有無を一目で確認できる。

🔹 使い方（サンプルコード）

import pandas as pd

df = pd.read_csv("data.csv")

# データの概要を表示
df.info()

🔹 出力される内容

行数と列数

カラム名

各カラムのデータ型（int, float, object など）

欠損値の数（Non-Null count）

メモリ使用量


🔹 応用例

# メモリ使用量も詳細表示
df.info(memory_usage="deep")


---

💡 ワンポイントヒント
df.head() とセットで df.info() を使うと、
「中身のイメージ」と「データの骨組み」を同時に把握できるよ😊
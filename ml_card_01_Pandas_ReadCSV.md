📊 MLカード No.1

テーマ：Pandas - データ読み込み

📝 概要

PandasはPythonでデータを扱うときの代表的なライブラリ。
最初のステップは「CSVファイルの読み込み」！


---

💡 コード例

import pandas as pd

# CSVファイルを読み込む
df = pd.read_csv("data.csv")

# データの最初の5行を表示
print(df.head())


---

🧩 ポイント

pd.read_csv("ファイル名") でCSVをDataFrameとして読み込める。

head() は最初の数行（デフォルトは5行）を確認できる。



---

🔑 応用

# 区切り文字を指定（例: タブ区切り）
df = pd.read_csv("data.tsv", sep="\t")

# 読み込み時に列の型を指定
df = pd.read_csv("data.csv", dtype={"id": int, "price": float})


---

✅ まとめ

read_csv はPandasの入口。

読み込んだらまず head() で中身をチェック！
🃏 MLカード No.5 – Pandas 基本編

📌 テーマ：groupby()（グループごとの集計）

🔹 説明

groupby() は、データを「グループ」に分けて、その中で合計や平均などの計算をするための関数。
エクセルの「ピボットテーブル」みたいなイメージだよ👍


---

🔹 使い方（サンプルコード）

import pandas as pd

data = {
    "store": ["A", "A", "B", "B", "A"],
    "sales": [100, 200, 150, 300, 250]
}
df = pd.DataFrame(data)

# 店ごとの売上合計
print(df.groupby("store")["sales"].sum())

🔹 出力例

store
A    550
B    450
Name: sales, dtype: int64


---

🔹 応用例

# 店ごとの売上平均
df.groupby("store")["sales"].mean()

# 複数の統計量をまとめて出す
df.groupby("store")["sales"].agg(["sum", "mean", "max"])


---

🔹 ポイント

groupby("列名") で分ける基準を決める

その後に sum() や mean() をつなげて集計

agg() を使えば一気に色々な統計をまとめられる



---

💡 ワンポイントヒント
「グループに分けて代表値を出す」＝データの特徴をつかむ最初の一歩だよ📊
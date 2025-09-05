🃏 MLカード No.6 – Pandas 応用編

📌 テーマ：merge()（データの結合）

🔹 説明

merge() は、SQLでいう「JOIN」と同じイメージ。
複数のDataFrameを「共通の列」でつなげて、ひとつにまとめられるよ😊


---

🔹 使い方（サンプルコード）

import pandas as pd

# 店舗データ
stores = pd.DataFrame({
    "store_id": [1, 2, 3],
    "store_name": ["A店", "B店", "C店"]
})

# 売上データ
sales = pd.DataFrame({
    "store_id": [1, 2, 2, 3],
    "sales": [100, 200, 150, 300]
})

# store_id をキーに結合
merged = pd.merge(sales, stores, on="store_id")
print(merged)

🔹 出力例

store_id  sales store_name
0         1    100        A店
1         2    200        B店
2         2    150        B店
3         3    300        C店


---

🔹 応用

# left join（左のデータを優先）
pd.merge(sales, stores, on="store_id", how="left")

# inner join（両方にあるデータだけ）
pd.merge(sales, stores, on="store_id", how="inner")


---

🔹 ポイント

on="列名" でキーを指定

how で結合の方法を選べる（inner / left / right / outer）

データ分析では「特徴量追加」のときによく使う



---

💡 ワンポイントヒント
KaggleやSIGNATEの前処理で「カテゴリ情報や外部データを結合する」時に必須になるスキルだよ✨

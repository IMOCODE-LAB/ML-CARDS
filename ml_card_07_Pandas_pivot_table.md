🃏 MLカード No.7 – Pandas 応用編

📌 テーマ：pivot_table()（ピボットテーブル）

🔹 説明

pivot_table() は、Excelのピボットテーブルみたいに「行・列・集計方法」を指定して、データをクロス集計できる便利な関数。


---

🔹 サンプルコード

import pandas as pd

data = pd.DataFrame({
    "store": ["A店", "A店", "B店", "B店", "C店"],
    "month": ["1月", "2月", "1月", "2月", "1月"],
    "sales": [100, 200, 150, 300, 250]
})

# 店 × 月ごとの売上合計
pivot = pd.pivot_table(data, values="sales", index="store", columns="month", aggfunc="sum", fill_value=0)
print(pivot)

🔹 出力例

month   1月   2月
store            
A店     100  200
B店     150  300
C店     250    0


---

🔹 ポイント

index → 行にしたい列

columns → 列にしたい列

values → 集計対象

aggfunc → 集計方法（sum mean count など）

fill_value=0 → 欠損値を埋める



---

💡 ワンポイントヒント
コンペや実務で「ユーザー×月ごとの平均値」とか「商品×店舗ごとの売上合計」を見る時に超便利！
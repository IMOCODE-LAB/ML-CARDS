🃏 MLカード No.8 – Pandas 応用編

📌 テーマ：apply()（関数の適用）

🔹 説明

apply() は、DataFrameやSeriesに独自の関数や処理を適用できる便利なメソッド。
「列ごと」「行ごと」にカスタム処理をしたいときに大活躍するよ😊


---

🔹 サンプルコード

import pandas as pd

# サンプルデータ
data = pd.DataFrame({
    "name": ["apple", "banana", "cherry"],
    "price": [100, 200, 300]
})

# price 列を2倍にする
data["double_price"] = data["price"].apply(lambda x: x * 2)
print(data)

🔹 出力例

name  price  double_price
0   apple    100           200
1  banana    200           400
2  cherry    300           600


---

🔹 行全体に関数を適用

# name と price を組み合わせて新しい列を作成
data["summary"] = data.apply(lambda row: f"{row['name']}は{row['price']}円", axis=1)

🔹 出力例

name  price  double_price        summary
0   apple    100           200   appleは100円
1  banana    200           400  bananaは200円
2  cherry    300           600  cherryは300円


---

🔹 ポイント

列に処理 → df["列名"].apply(...)

行に処理 → df.apply(..., axis=1)

lambda をよく使うけど、自作関数を渡すことも可能



---

💡 ワンポイントヒント
KaggleやSIGNATEの特徴量作成で「新しい列を柔軟に作りたい」ときに必須のスキルだよ✨
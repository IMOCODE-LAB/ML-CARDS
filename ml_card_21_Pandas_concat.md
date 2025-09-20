🃏 MLカード No.21 – Pandas concat()

📌 概要

複数のDataFrameやSeriesを 縦や横に結合 するための関数。
merge() と違い、キーを指定せず単純に「つなげる」イメージ。


---

🔹 基本構文

pd.concat(objs, axis=0, join='outer', ignore_index=False)

objs: DataFrameやSeriesのリスト [df1, df2, ...]

axis: 0=縦方向（デフォルト）、1=横方向

join: 'outer'=全てのラベルを結合、'inner'=共通部分だけ

ignore_index: Trueにすると新しい連番のインデックスになる



---

🔹 使用例

1. 縦に結合

import pandas as pd

df1 = pd.DataFrame({"A": [1, 2], "B": [3, 4]})
df2 = pd.DataFrame({"A": [5, 6], "B": [7, 8]})

result = pd.concat([df1, df2], axis=0)
print(result)

👉 結果

A  B
0  1  3
1  2  4
0  5  7
1  6  8


---

2. インデックスをリセットして縦結合

result = pd.concat([df1, df2], axis=0, ignore_index=True)
print(result)

👉 結果

A  B
0  1  3
1  2  4
2  5  7
3  6  8


---

3. 横に結合

result = pd.concat([df1, df2], axis=1)
print(result)

👉 結果

A  B  A  B
0  1  3  5  7
1  2  4  6  8


---

🌟 ポイント

merge: キーで結合（リレーショナルDBっぽい）

concat: 単純につなげるだけ

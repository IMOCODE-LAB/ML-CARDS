🃏 MLカード No.4 – Pandas 基本編

📌 テーマ：value_counts()（カテゴリごとの件数集計）

🔹 説明

value_counts() は、シリーズや列の中で 値がいくつ出現したか を数えてくれる関数。
データの偏りや分布を知るときにめちゃ便利だよ👍

🔹 使い方（サンプルコード）

import pandas as pd

data = {"fruit": ["apple", "banana", "apple", "orange", "banana", "apple"]}
df = pd.DataFrame(data)

print(df["fruit"].value_counts())

🔹 出力例

apple     3
banana    2
orange    1
Name: fruit, dtype: int64

🔹 ポイント

データの中で どれが多いか／少ないか を一瞬で把握できる

normalize=True を付けると 比率（割合） が出せる

sort=False で登場順を保持できる


🔹 応用例

# 割合を確認
df["fruit"].value_counts(normalize=True)

# 上位2件だけ表示
df["fruit"].value_counts().head(2)


---

💡 ワンポイントヒント
value_counts() は「人気投票」の結果を出してくれる感じだよ🍎🍌🍊

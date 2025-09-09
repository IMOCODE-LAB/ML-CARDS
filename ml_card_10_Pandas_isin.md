🃏 MLカード No.10 – Pandas 応用編

📌 テーマ：isin()（複数条件のフィルタリング）

🔹 説明

isin() は、Series（1列）の値が 指定したリストや集合に含まれるかどうか を判定するメソッド。
「特定の値だけ抽出したい」ときに便利だよ😊


---

🔹 サンプルコード

import pandas as pd

# サンプルデータ
data = pd.DataFrame({
    "fruit": ["apple", "banana", "cherry", "apple", "banana"],
    "price": [100, 200, 300, 150, 250]
})

# 果物が apple または banana の行だけ抽出
filtered = data[data["fruit"].isin(["apple", "banana"])]
print(filtered)

🔹 出力例

fruit  price
0   apple    100
1  banana    200
3   apple    150
4  banana    250


---

🔹 NOT 条件（除外したい場合）

# cherry 以外を抽出
not_cherry = data[~data["fruit"].isin(["cherry"])]


---

🔹 ポイント

複数の値でフィルタするときにスマート✨

NOT条件は ~ を前につけるだけ

リスト・タプル・集合が使える



---

💡 ワンポイントヒント
KaggleやSIGNATEで「特定のカテゴリだけ」「外れ値カテゴリを除外」するときに便利だよ👍
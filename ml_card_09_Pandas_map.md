🃏 MLカード No.9 – Pandas 応用編

📌 テーマ：map()（要素ごとの変換）

🔹 説明

map() は、Series（1列）に対して要素ごとに変換や関数適用をする便利なメソッド。
データをラベル変換したり、値を加工するときに大活躍だよ😊


---

🔹 サンプルコード

import pandas as pd

# サンプルデータ
data = pd.DataFrame({
    "fruit": ["apple", "banana", "cherry"],
    "price": [100, 200, 300]
})

# 果物の名前を日本語に変換
translate = {"apple": "りんご", "banana": "バナナ", "cherry": "さくらんぼ"}
data["fruit_jp"] = data["fruit"].map(translate)

print(data)

🔹 出力例

fruit  price fruit_jp
0   apple    100     りんご
1  banana    200     バナナ
2  cherry    300   さくらんぼ


---

🔹 関数を渡す

# 価格に10%の税を加える
data["price_tax"] = data["price"].map(lambda x: x * 1.1)


---

🔹 ポイント

map(dict) → 辞書で置換

map(func) → 関数やlambdaで処理

1列専用（複数列なら apply() の方が便利）



---

💡 ワンポイントヒント
KaggleやSIGNATEではカテゴリデータをIDやラベルに変換するときによく使うよ👍
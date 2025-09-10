🃏 MLカード No.11 – scikit-learn: train_test_split

📌 テーマ：データを学習用とテスト用に分割する

🔹 説明

train_test_split は、データを「学習用」と「テスト用」にランダム分割する関数。
機械学習で「汎化性能（新しいデータにも対応できる力）」を確認するために必須だよ😊


---

🔹 サンプルコード

from sklearn.model_selection import train_test_split
import pandas as pd

# サンプルデータ
df = pd.DataFrame({
    "x1": [1,2,3,4,5,6,7,8,9,10],
    "x2": [5,4,6,7,2,9,1,8,3,10],
    "y":  [0,1,0,1,0,1,0,1,0,1]
})

# 説明変数と目的変数
X = df[["x1", "x2"]]
y = df["y"]

# 学習7割、テスト3割に分割
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)

print("学習データ数:", len(X_train))
print("テストデータ数:", len(X_test))

🔹 出力例

学習データ数: 7
テストデータ数: 3


---

🔹 ポイント

test_size=0.3 → データの30%をテストに使う

random_state=42 → 毎回同じ分割結果にしたい時に便利

データが不均衡な場合は stratify=y を指定するとクラス比率を維持できる



---

💡 ワンポイントヒント
実務でもコンペでも「学習とテストをちゃんと分ける」が最初の基本✨
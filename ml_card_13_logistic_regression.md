🃏 MLカード No.13 – scikit-learn: LogisticRegression

📌 テーマ：分類に使えるロジスティック回帰

🔹 説明

LogisticRegression は Yes/No や 0/1 を予測する分類モデル。
「合格するかしないか」「購入するかしないか」などの二値分類に便利✨


---

🔹 サンプルコード

from sklearn.linear_model import LogisticRegression
import numpy as np

# サンプルデータ
X = np.array([[1], [2], [3], [4], [5], [6]])  # 説明変数
y = np.array([0, 0, 0, 1, 1, 1])              # 目的変数

# モデル作成
model = LogisticRegression()
model.fit(X, y)

# 予測
print("x=2 の予測:", model.predict([[2]]))
print("x=5 の予測:", model.predict([[5]]))

# 予測確率
print("x=5 の確率:", model.predict_proba([[5]]))

🔹 出力例

x=2 の予測: [0]
x=5 の予測: [1]
x=5 の確率: [[0.12 0.88]]


---

🔹 ポイント

predict() → 0/1 のラベルを返す

predict_proba() → それぞれのクラスの確率を返す

線形回帰と似てるけど、出力を0〜1に収めるためにシグモイド関数を使う



---

💡 ワンポイントヒント
ロジスティック回帰は「分類問題の入口」。
これをマスターすると、決定木やランダムフォレストにも自然に進めるよ✨
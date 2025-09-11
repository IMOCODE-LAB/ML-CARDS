🃏 MLカード No.12 – scikit-learn: LinearRegression

📌 テーマ：シンプルな線形回帰モデル

🔹 説明

LinearRegression は「入力（特徴量）」と「出力（目的変数）」の関係を、直線（または平面）で近似するモデル。
「売上予測」「体重と身長の関係」などに使える基本中の基本✨


---

🔹 サンプルコード

from sklearn.linear_model import LinearRegression
import numpy as np

# サンプルデータ
X = np.array([[1], [2], [3], [4], [5]])  # 説明変数
y = np.array([2, 4, 6, 8, 10])           # 目的変数

# モデル作成
model = LinearRegression()
model.fit(X, y)

# 予測
pred = model.predict([[6]])
print("x=6 の予測値:", pred[0])

# 回帰係数と切片
print("傾き:", model.coef_[0])
print("切片:", model.intercept_)

🔹 出力例

x=6 の予測値: 12.0
傾き: 2.0
切片: 0.0


---

🔹 ポイント

.fit(X, y) で学習

.predict() で予測

.coef_ が係数（傾き）、.intercept_ が切片

実データでは「きれいな直線」にはならないけど、基礎モデルとして重要✨



---

💡 ワンポイントヒント
まずは「1次元の直線回帰」で理解 → その後「多変量回帰」「正則化回帰」に進むと自然にレベルアップできるよ👍
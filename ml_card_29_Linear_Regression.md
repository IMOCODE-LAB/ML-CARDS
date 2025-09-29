📇 MLカード：LinearRegression

🌟 用途

シンプルな 回帰モデル。
家賃、売上、温度など「数値を予測するタスク」で、最初の比較モデルに最適。


---

📝 例題：家賃を予測してみよう

「部屋の広さ（㎡）」と「駅からの距離（分）」から、家賃を予測する例。

import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split

# データ（例）
data = pd.DataFrame({
    "area": [20, 35, 40, 55, 60],
    "distance": [10, 8, 12, 5, 3],
    "rent": [5.5, 8.0, 9.0, 12.5, 13.0]  # 家賃(万円)
})

X = data[["area", "distance"]]
y = data["rent"]

# 学習用とテスト用に分割
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# モデル作成
model = LinearRegression()

# 学習
model.fit(X_train, y_train)

# 予測
y_pred = model.predict(X_test)

print("予測結果:", y_pred)


---

🔑 ポイント

理解しやすい：単純な数式で説明可能。

ベースライン：まずLinearRegressionでスコアを出し、その後に複雑なモデルと比較。

高速：学習・予測がとても速い。
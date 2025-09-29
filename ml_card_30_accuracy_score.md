📇 MLカード：accuracy_score

🌟 用途

分類タスクの**正解率（Accuracy）**を測定する評価指標。
「どれくらい正しく分類できたか」をシンプルにチェックできる。


---

📝 例題：合格/不合格を予測したモデルの精度を評価

from sklearn.metrics import accuracy_score

# 予測結果（例）
y_true = [1, 0, 1, 1, 0]  # 正解ラベル
y_pred = [1, 0, 0, 1, 0]  # モデルの予測結果

# 精度を計算
accuracy = accuracy_score(y_true, y_pred)

print("Accuracy:", accuracy)


---

🔑 ポイント

分類タスク専用（回帰には使わない）。

値が 1.0に近いほど良い。

データが偏っている（例：95%が同じクラス）場合は、別の指標（F1スコアなど）と一緒に使うと良い。

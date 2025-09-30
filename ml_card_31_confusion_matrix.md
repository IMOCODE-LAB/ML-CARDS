🃏 MLカード#21：混同行列（confusion_matrix）

📚内容
分類問題の結果をもっと詳しく分析するのが 混同行列。
「どのクラスを正しく予測できて、どのクラスを間違えたか」が一目で分かるよ😊


---

💻サンプルコード

from sklearn.metrics import confusion_matrix

# 実際のラベル
y_true = [1, 0, 1, 1, 0, 0, 1]

# 予測ラベル
y_pred = [1, 0, 0, 1, 0, 1, 1]

# 混同行列を作成
cm = confusion_matrix(y_true, y_pred)
print("Confusion Matrix:\n", cm)

出力例（2クラスの場合）:

[[TN FP]
 [FN TP]]


---

📌ポイント

TN (True Negative)：0を0と予測した数

FP (False Positive)：0を1と間違えた数

FN (False Negative)：1を0と間違えた数

TP (True Positive)：1を1と予測した数

これを組み合わせて「precision」「recall」などの指標を計算できる



---

📝練習のヒント

sklearn.metrics.ConfusionMatrixDisplay を使うと可視化できるよ📊

2クラスだけじゃなく、多クラス分類でも活躍する
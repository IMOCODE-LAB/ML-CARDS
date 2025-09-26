📝 テーマ：モデルの精度評価（評価指標）
💡 内容：機械学習モデルの性能を測る指標の基礎

from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

# 予測値と正解ラベル
y_true = [0, 1, 1, 0, 1]
y_pred = [0, 1, 0, 0, 1]

print("Accuracy:", accuracy_score(y_true, y_pred))   # 正解率
print("Precision:", precision_score(y_true, y_pred)) # 適合率
print("Recall:", recall_score(y_true, y_pred))       # 再現率
print("F1:", f1_score(y_true, y_pred))               # F1スコア

🔑 ポイント

Accuracy（正解率）＝全体でどれだけ当たってるか

Precision（適合率）＝予測した正例がどれだけ正しかったか

Recall（再現率）＝本当の正例をどれだけ拾えたか

F1スコア＝PrecisionとRecallのバランス



---
MLカード No.19 — scikit-learn：データ分割と評価指標（train_test_split + 基本の評価）

📌 概要

モデルを作るときは「学習用データ」と「評価用データ」に分けて、過学習を防ぎつつ性能を正しく測るのが超重要。
代表的な分割ツールは train_test_split。評価指標は問題（分類 / 回帰）に合わせて選ぶよ。


---

🔹 サンプルコード（分類問題）

import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score, confusion_matrix

# ダミーデータ
X = np.random.rand(200, 10)
y = np.random.randint(0, 2, size=200)

# データ分割（標準は test_size=0.2、random_stateを固定すると再現性あり）
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)

# モデル学習
model = RandomForestClassifier(random_state=42)
model.fit(X_train, y_train)

# 予測
y_pred = model.predict(X_test)
y_proba = model.predict_proba(X_test)[:, 1]  # ROC AUC 用（陽性確率）

# 評価指標（分類）
acc = accuracy_score(y_test, y_pred)
prec = precision_score(y_test, y_pred, zero_division=0)
rec = recall_score(y_test, y_pred, zero_division=0)
f1 = f1_score(y_test, y_pred, zero_division=0)
roc_auc = roc_auc_score(y_test, y_proba)
cm = confusion_matrix(y_test, y_pred)

print("Accuracy:", acc)
print("Precision:", prec)
print("Recall:", rec)
print("F1:", f1)
print("ROC AUC:", roc_auc)
print("Confusion Matrix:\\n", cm)


---

✅ 指標の使い分け（ざっくり）

Accuracy（正解率）：クラスがほぼ均等なときに有効。

Precision（適合率）：陽性と予測した中でどれだけ正しかったか（誤検知を減らしたいとき採用）。

Recall（再現率）：実際に陽性のうちどれだけ拾えたか（見逃しを減らしたいとき重視）。

F1：Precision と Recall の調和平均（バランス重視）。

ROC AUC：予測確率の判別能力を評価（閾値に依存しない指標）。



---

💡 ワンポイント

stratify=y を使うと、分割後もクラス比率が保たれる（クラス不均衡時に重要）。

テストは必ず 未使用データ（訓練時に触ってない）で評価する。

最終評価用にさらに 検証用（validation） を作る（train → train/val → test の3分割）か、クロスバリデーション（CV） を使うと安心。

回帰問題なら mean_squared_error, r2_score などを使うよ。
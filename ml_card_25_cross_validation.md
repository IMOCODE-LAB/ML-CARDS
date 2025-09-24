MLカード No.25 — クロスバリデーション（K-Fold / StratifiedK-Fold）

📌 概要

モデルの汎化性能を安定して評価するために、データを複数の分割で訓練／検証して平均や分散を取る手法。1回の train_test_split より信頼性が高い。分類ではクラス比を保つ StratifiedKFold がよく使われる。


---

🔹 基本フロー（イメージ）

1. データを K 等分する（folds）。


2. 各 fold を順番に検証用にして、残りで学習 → スコアを記録。


3. K 回のスコア平均と標準偏差を見る → モデルの安定性を確認。




---

🔹 サンプルコード（scikit-learn）

import numpy as np
from sklearn.model_selection import KFold, StratifiedKFold, cross_val_score
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import make_classification

X, y = make_classification(n_samples=500, n_classes=2, random_state=42)

# 1) KFold（回帰やクラス比無視で使う）
kf = KFold(n_splits=5, shuffle=True, random_state=42)
model = RandomForestClassifier(random_state=42)
scores_kf = cross_val_score(model, X, y, cv=kf, scoring='roc_auc')
print("KFold AUC mean:", scores_kf.mean(), "std:", scores_kf.std())

# 2) StratifiedKFold（分類でクラス比を保つ）
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
scores_skf = cross_val_score(model, X, y, cv=skf, scoring='roc_auc')
print("StratifiedKFold AUC mean:", scores_skf.mean(), "std:", scores_skf.std())


---

✅ 使い分けの目安

分類問題 → StratifiedKFold を基本に。クラス不均衡時に有効。

回帰問題 → KFold（連続値の分布に注意）。

時系列データ → 標準のKFoldは不可。TimeSeriesSplit を使う（時刻順を守る）。



---

⚠️ よくある落とし穴

前処理の情報漏洩（Data Leakage）：
標準化や特徴量作成を全データでやってからCVするとダメ。→ Pipeline や cross_val_score と組み合わせて、fit は必ず学習データ内だけで行う。

シャッフルなしでKFoldを使う：偏った分割になることがある（shuffle=True 推奨）。

スコアの分散を見ない：平均だけで判断すると不安定なモデルを見逃す。標準偏差もチェックしよう。

長時間のCV：Kを大きくすると時間が増える（計算コストに注意）。



---

💡 実務ワンポイント

GridSearchCV / RandomizedSearchCV と組み合わせるとハイパーパラ探索の再現性が上がる。

小データでは LeaveOneOut や RepeatedKFold が有効な場合あり（ただし計算コスト注意）。

結果は 平均 ± 標準偏差 で報告する習慣をつけると、面接やレポートで説得力が出る。
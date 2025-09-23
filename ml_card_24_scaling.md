MLカード No.24 — 特徴量のスケーリング（StandardScaler / MinMaxScaler）

📌 概要

特徴量スケーリングは、モデル学習前の重要な前処理。
各特徴量のスケール（値の幅）が大きく違うと、勾配法や距離ベース（k-NN、SVM、KMeans、ニューラルネット等）の学習がうまくいかないことがある。代表的なのが StandardScaler（平均0・分散1）と MinMaxScaler（0〜1 に正規化）。


---

🔹 使い分け

StandardScaler（平均0、分散1）
→ 線形モデル、SVM、ニューラルネットでよく使う。外れ値に敏感だが、標準化は多くのモデルで安定する。

MinMaxScaler（0〜1）
→ 出力レンジが0〜1に揃うので、活性化関数の入力レンジを意識したいときや、距離ベースで扱うときに便利。外れ値があると圧縮されやすい。

木系（RandomForest / XGBoost）
→ 多くの場合スケーリング不要。ただし特徴量によってはやっても悪くない。



---

🔹 サンプルコード（典型ワークフロー）

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, MinMaxScaler
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import make_pipeline
from sklearn.metrics import accuracy_score

# ダミーデータ
X = pd.DataFrame({
    "age": [20, 30, 40, 50],
    "income": [200, 4000, 3000, 10000],  # スケールが大きく違う
})
y = [0, 1, 0, 1]

# 分割（重要！テストは学習時に触れない）
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=42, test_size=0.3)

# 1) StandardScaler を使った Pipeline
pipeline_std = make_pipeline(StandardScaler(), LogisticRegression())
pipeline_std.fit(X_train, y_train)
pred_std = pipeline_std.predict(X_test)

# 2) MinMaxScaler を使った Pipeline
pipeline_mm = make_pipeline(MinMaxScaler(), LogisticRegression())
pipeline_mm.fit(X_train, y_train)
pred_mm = pipeline_mm.predict(X_test)

print("accuracy (Standard):", accuracy_score(y_test, pred_std))
print("accuracy (MinMax):", accuracy_score(y_test, pred_mm))


---

⚠️ 注意点（よくあるミス）

1. データ分割後にスケーリングする
→ fit は必ず訓練データだけで行い、テスト/検証データは transform のみ。さもないと情報漏洩（データリーク）になる。
（→ Pipeline で fit を訓練セットにだけ行うのが安全）


2. カテゴリ変数を標準化しない
→ カテゴリはone-hotやembeddingで扱ってからスケールするか、そもそもスケーリング不要な場合が多い。


3. 外れ値の存在
→ 外れ値が多い列には RobustScaler（中央値基準・IQRでスケーリング）を検討。


4. 木系モデルに無駄に適用する
→ 木系はスケーリングの影響が小さい（ただし一貫性のため適用するチームもある）。




---

💡 実務ワンポイント

Pipeline を使うと前処理→学習→評価の流れが再現可能になり、交差検証やハイパーパラ探索で便利。

モデルごとにスケーラーを変えて試す（Standard / MinMax / Robust）と性能が変わることがあるので比較しよう。

学習ログに「どのスケーラーを使ったか」を残す（README or experiment log）と再現性が上がる。
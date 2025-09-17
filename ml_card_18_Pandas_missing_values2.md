MLカード No.18 — Pandas 欠損値処理（isna, fillna, dropna）

📌 概要

データ分析では「欠損値（NaN）」がよく出てくる。これをどう扱うかで結果が大きく変わるよ。

確認：isna(), notna()

除去：dropna()

補完：fillna()



---

🔹 サンプルコード

import pandas as pd
import numpy as np

df = pd.DataFrame({
    "name": ["Alice", "Bob", "Charlie", "David"],
    "score": [85, np.nan, 95, 88],
    "age": [24, 22, np.nan, 23]
})

# 1) 欠損値を確認
print(df.isna())      # True/Falseで表示
print(df.isna().sum()) # 列ごとの欠損数を集計

# 2) 欠損値を含む行を削除
df_drop = df.dropna()

# 3) 欠損値を特定の値で埋める
df_fill = df.fillna(0)   # 0で埋める
df_mean = df.fillna(df.mean(numeric_only=True))  # 平均で埋める

# 4) 列ごとに異なる埋め方
df_custom = df.fillna({"score": df["score"].median(), "age": 20})

# 5) 前後の値で埋める
df_ffill = df.fillna(method="ffill")  # 前の値で埋める
df_bfill = df.fillna(method="bfill")  # 後ろの値で埋める


---

✅ ポイント

dropna()：大事なデータが消えるので乱用注意

fillna()：数値なら平均/中央値、カテゴリならモード（最頻値）で埋めることが多い

前後の値で埋めるのは 時系列データ に便利



---

💡 ワンポイント

欠損の「意味」まで考えるのが本当の分析！
例：年齢がNaN → 「回答しなかった」のか「記録ミス」なのかで対処法が変わるよ
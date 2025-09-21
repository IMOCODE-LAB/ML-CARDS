MLカード No.22 — Pandas：型変換 astype()（＋実務でよく使う代替手段）

📌 概要

astype() は列のデータ型（dtype）を変換する基本メソッド。
数値・文字列・カテゴリ・bool・datetime などに変換して、計算やメモリ節約、モデル投入に備えるよ。


---

🔹 基本例

import pandas as pd

df = pd.DataFrame({
    "a": ["1", "2", "3"],
    "b": [1.0, 2.0, 3.0],
    "c": ["2023-01-01", "2023-02-03", None]
})

# 文字列→整数
df["a"] = df["a"].astype(int)

# float→int（小数がない前提）
df["b"] = df["b"].astype(int)

# 文字列→カテゴリ（メモリ削減、モデルに有用）
df["cat"] = df["a"].astype("category")


---

⚠️ よくある注意点（失敗ケースと対処）

NaNがある列に astype(int) を使うとエラーになる
→ 対処：pd.to_numeric(..., errors="coerce") で安全に数値化してから

df["a_num"] = pd.to_numeric(df["a"], errors="coerce").astype("Int64")  # pandasのnullable integer

文字列に不正な値が混ざると astype(float) で失敗
→ 先に pd.to_numeric(..., errors="coerce") で不正値を NaN にする

カテゴリ型は順序性（ordinal）が必要なら CategoricalDtype を使う

from pandas.api.types import CategoricalDtype
order = CategoricalDtype(categories=["low","mid","high"], ordered=True)
df["level"] = df["level"].astype(order)



---

🔧 便利な代替・補助関数

pd.to_numeric(series, errors="coerce")：安全な数値変換

pd.to_datetime(series, errors="coerce", format=...)：日付変換（次回詳述）

df.astype({ "col1": "int64", "col2": "float32", "col3": "category" })：複数列を一度に変換

pandas の nullable 型（例："Int64"）は NaN を許容する整数型として便利



---

💡 実践ワンポイント

モデル学習前はカテゴリ型にしておくと特徴量処理が明快（One-Hot 等）。

大規模データでは float32 / int32 にダウンサンプリングしてメモリ削減。

変換操作は不可逆なことがある（例：float→intで小数切り捨て）ので 元データは残すかコピー を推奨。
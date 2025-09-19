MLカード No.19— Pandas：データ結合（merge, concat, join）

📌 概要

複数の表（DataFrame）をキーや行・列でつなぎ合わせる基本操作。

merge()：SQL の JOIN に相当（キーで結合）

concat()：縦または横に単純連結（行や列の追加）

join()：インデックスを使った結合（merge の簡易版）



---

🔹 サンプルコード（使い分け）

import pandas as pd

# サンプル
df1 = pd.DataFrame({"id":[1,2,3], "name":["A","B","C"]})
df2 = pd.DataFrame({"id":[2,3,4], "score":[80,90,70]})

# 1) merge: デフォは inner join（共通キーだけ残す）
df_inner = pd.merge(df1, df2, on="id", how="inner")

# 2) 左外部結合（left join）: df1の行は全て残す
df_left = pd.merge(df1, df2, on="id", how="left")

# 3) 列名が違うキーで結合
df2b = pd.DataFrame({"user_id":[1,3], "score":[88,95]})
df_on_diff = pd.merge(df1, df2b, left_on="id", right_on="user_id", how="left")

# 4) concat: 縦に結合（axis=0）／横に結合（axis=1）
df_a = pd.DataFrame({"x":[1,2]})
df_b = pd.DataFrame({"x":[3,4]})
df_concat = pd.concat([df_a, df_b], axis=0, ignore_index=True)

# 5) join: インデックス基準の結合
df_idx1 = df1.set_index("id")
df_idx2 = df2.set_index("id")
df_joined = df_idx1.join(df_idx2, how="left")


---

✅ 使い分けポイント

キーで合体したい → merge()（左右どちらを基準にするかを how で指定）

単に行を追加／列を横付けしたい → concat()（indexの扱いに注意）

インデックスを基準にしたい → join()（set_index() してから使うと分かりやすい）



---

⚠️ 注意点（よくある落とし穴）

キーに重複があると行数が増える（意図しないクロス結合に注意）。

キー名が違うと on= ではなく left_on / right_on を使う必要がある。

merge の how（inner, left, right, outer）で結果が全然変わる。目的に合わせて選ぼう。

concat は列ラベルやインデックスを合わせないと NaN が入ることがある（ignore_index=True や axis に注意）。



---

💡 ワンポイント
結合前：df1.head() / df2.head() と df1.info() を確認して、キーの重複・欠損・データ型が揃っているかチェックすると失敗が減るよ。

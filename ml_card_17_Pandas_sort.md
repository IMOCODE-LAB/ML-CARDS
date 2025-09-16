MLカード No.17 — Pandas 並び替え (sort_values, sort_index)

概要

sort_values()：列（カラム）を基準に行を並び替える

sort_index()：インデックス（行ラベル／列ラベル）で並び替える



---

サンプルコード

import pandas as pd

df = pd.DataFrame({
    "name": ["Alice", "Bob", "Charlie", "Bob"],
    "score": [85, 90, 95, 88],
    "age": [24, 22, 23, 22]
})

# 1) scoreで昇順にソート（デフォルトは昇順）
df_sorted = df.sort_values("score")
print(df_sorted)

# 2) scoreで降順にソート
df_desc = df.sort_values("score", ascending=False)

# 3) 複数列でソート（まずname昇順、その中でscore降順）
df_multi = df.sort_values(["name", "score"], ascending=[True, False])

# 4) インデックスでソート
df_idx = df.set_index("name")
df_idx_sorted = df_idx.sort_index()  # アルファベット順など

# 5) 欠損値の位置指定（naは最後に置く）
df.sort_values("score", na_position="last")

# 6) in-placeで変更（元DFを書き換える）
df.sort_values("score", inplace=True)


---

出力イメージ（df_sorted）

name  score  age
0   Alice     85   24
3     Bob     88   22
1     Bob     90   22
2 Charlie     95   23


---

便利なオプションまとめ

ascending=True/False：昇順/降順

by=[...]：複数列でソート（順番が優先度）

na_position='first'/'last'：欠損値を先頭 or 最後に置く

inplace=True：元DFを直接書き換える（戻せないので注意）

sort_index(axis=0 or 1)：行（0）か列（1）のインデックスでソート



---

ワンポイント

大きなDataFrameで頻繁にソートすると重い（O(n log n)）。

インデックスでの高速検索を多用するなら、set_index()してからsort_index()で整えると用途に合うことがあるよ。

可読性のために「何で並べ替えたかをコメント or 列名に残す」習慣があると便利（後で見返すと助かる）。
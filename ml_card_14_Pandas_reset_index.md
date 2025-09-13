🃏 今日のMLカード

関数: reset_index()
カテゴリ: Pandas – インデックス操作

🔹 使い方

import pandas as pd

# サンプルDataFrame
df = pd.DataFrame({
    "名前": ["A", "B", "C"],
    "点数": [90, 80, 85]
}, index=["one", "two", "three"])

print("元のDataFrame:")
print(df)

# インデックスをリセット
df_reset = df.reset_index()

print("\nreset_index後:")
print(df_reset)

🔹 出力

元のDataFrame:
       名前  点数
one     A  90
two     B  80
three   C  85

reset_index後:
  index 名前  点数
0   one  A  90
1   two  B  80
2 three  C  85

🔹 ポイント

行ラベルを「普通の列」に変換して、新しい連番インデックスを振ってくれる。

よく使う場面は、groupby() や set_index() で特殊なインデックスになったときに元に戻すとき。

drop=True にすると、インデックスを列にせず破棄できる。
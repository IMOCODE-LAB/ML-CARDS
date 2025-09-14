🃏 MLカード No.15 Pandas 欠損値処理

✅ 基本メソッド

import pandas as pd

# サンプルデータ
df = pd.DataFrame({
    "A": [1, 2, None, 4],
    "B": [None, 2, 3, 4]
})

# 欠損値の確認
print(df.isnull())        # True/False で欠損かどうか
print(df.isnull().sum())  # 各列の欠損数カウント


---

🧹 欠損値の削除

# 行ごと削除
df_drop_row = df.dropna()

# 列ごと削除
df_drop_col = df.dropna(axis=1)


---

✨ 欠損値の補完

# 特定の値で埋める
df_fill_zero = df.fillna(0)

# 平均値で埋める
df_fill_mean = df.fillna(df.mean())

# 前の値で埋める (forward fill)
df_ffill = df.fillna(method="ffill")

# 後ろの値で埋める (backward fill)
df_bfill = df.fillna(method="bfill")


---

💡 ポイント

削除(dropna) はデータが多いときに有効

補完(fillna) はデータを活かしたいときに便利

実際は「どの方法が妥当か」はドメイン知識やデータ量次第
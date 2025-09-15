🃏 MLカード No.16 Pandas 重複データ処理

✅ 重複データの確認

import pandas as pd

# サンプルデータ
df = pd.DataFrame({
    "name": ["Alice", "Bob", "Alice", "Charlie"],
    "score": [85, 90, 85, 95]
})

# 重複の確認（行単位で）
print(df.duplicated())

# 重複の数を確認
print(df.duplicated().sum())


---

🗑️ 重複データの削除

# 全く同じ行を削除（最初の1つだけ残す）
df_unique = df.drop_duplicates()

# 特定の列だけで判定
df_unique_name = df.drop_duplicates(subset=["name"])

# keep引数で残すルールを変更
df_first = df.drop_duplicates(keep="first")   # 最初を残す（デフォルト）
df_last  = df.drop_duplicates(keep="last")    # 最後を残す
df_none  = df.drop_duplicates(keep=False)     # 全部削除


---

💡 ポイント

duplicated() は True/False で「重複かどうか」を返す。

drop_duplicates() は「重複をどう残すか」指定できる。

データクレンジングでよく使う必須テクニック。
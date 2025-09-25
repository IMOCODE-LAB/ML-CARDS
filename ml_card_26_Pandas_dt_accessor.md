🃏 MLカード No.26 — Pandas .dt アクセサ

📌 概要

datetime64 型の列から、年・月・日・曜日などを抽出するためのアクセサ。
時系列特徴量の作成に便利。


---

🖋️ サンプルコード

import pandas as pd

# サンプルデータ
data = {"date": pd.to_datetime(["2025-01-01", "2025-02-15", "2025-03-20"])}
df = pd.DataFrame(data)

# 年・月・日を抽出
df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
df["day"] = df["date"].dt.day

# 曜日（0=月曜, 6=日曜）
df["weekday"] = df["date"].dt.weekday
df["weekday_name"] = df["date"].dt.day_name()

print(df)


---

✅ 出力例

date  year  month  day  weekday weekday_name
0 2025-01-01  2025      1    1        2    Wednesday
1 2025-02-15  2025      2   15        5    Saturday
2 2025-03-20  2025      3   20        3    Thursday


---

🚀 ポイント

df["date"].dt.year / month / day で基本的な日付要素を取得。

dt.day_name() で曜日の文字列（英語表記）を取れる。

dt.is_month_start / is_month_end で月初や月末かどうか判定できる。

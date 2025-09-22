MLカード No.23 — Pandas：日付処理 pd.to_datetime() と実務での落とし穴

📌 概要

文字列の日時データを datetime64 型に変換して、時系列処理や日付差分、月/週/日抽出などを安全に行えるようにする関数。エラーや誤変換を避けるための工夫が重要。


---

🔹 基本コード

import pandas as pd

df = pd.DataFrame({
    "date_str": ["2023-01-02", "2023/02/03", "03-04-2023", None, "20230205", "invalid"]
})

# 標準の変換（自動推測）
df['date'] = pd.to_datetime(df['date_str'], errors='coerce')

# 明確なフォーマット指定（速くて安全）
df['date_fix'] = pd.to_datetime(df['date_str'], format='%Y-%m-%d', errors='coerce')


---

✅ よく使うオプション

errors='coerce'：変換できない値は NaT（欠損の日時）にする（推奨）

format='...'：厳密なフォーマットを指定 → 速くて誤変換が減る

dayfirst=True：日/月/年の順で与えられているデータに対応（例：31/12/2023）

utc=True：UTCとして扱う（タイムゾーンが関係する場合）



---

⚠️ よくある落とし穴と対処法

1. 混在フォーマット

複数フォーマットが混じると自動推測で誤認識されることがある。

→ 事前にフォーマット別に分けて to_datetime(..., format=...) を使うか、errors='coerce' で落としどころを作る。



2. 文字列に余分な空白や全角が含まれる

→ df['date_str'] = df['date_str'].str.strip() を先に実施。



3. 地域表記（日/月 vs 月/日）

欧州表記（DD/MM/YYYY）と米国表記（MM/DD/YYYY）の混在に注意。dayfirst=True を検討。



4. タイムゾーン（tz）問題

ログデータなどで tz 情報が混在すると解析が狂う。dt.tz_convert() / dt.tz_localize() で統一する。



5. 数値型の日付（YYYYMMDD）を読み込むと整数扱い

→ 文字列化してから変換：df['d'] = df['d'].astype(str); pd.to_datetime(df['d'], format='%Y%m%d')



6. 欠損（NaN）をそのまま astype('datetime64') しようとしてエラー

→ pd.to_datetime(..., errors='coerce') を使うか、nullable datetime 型を検討。





---

🔧 実務ワンポイント

まず df['date_str'].head() とユニークサンプルを確認して「どのフォーマットが何割か」を把握してから変換する。

変換後は df['date'].isna().sum() で失敗件数を確認 → どの行が失敗したか df[df['date'].isna()] で追う。

時系列モデルを作る前に インデックスを DatetimeIndex にする：

df = df.set_index('date').sort_index()

月末・月初の処理や営業日ベースの処理が必要なら pd.offsets や pd.tseries.offsets を活用。
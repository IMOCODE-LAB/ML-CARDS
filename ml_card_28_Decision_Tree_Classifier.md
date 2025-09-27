📚 今日のMLカード（モデリング編）
「DecisionTreeClassifier」

使う場面：分類タスク（Yes/No、ラベル分類など）

特徴：

木構造でデータを分割していく

直感的で解釈しやすい


基本コード：


from sklearn.tree import DecisionTreeClassifier

# モデルの作成
model = DecisionTreeClassifier(random_state=42)

# 学習
model.fit(X_train, y_train)

# 予測
y_pred = model.predict(X_test)

ヒント：

max_depth を指定すると木の深さを制限できる（過学習防止に役立つ）

criterion="gini"（ジニ係数）や "entropy"（情報利得）で分割基準を選べる
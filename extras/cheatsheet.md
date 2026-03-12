# ML Libraries Cheatsheet

Quick reference for the most commonly used commands. Every example shows the output.

---

## NumPy

```python
import numpy as np

# Create arrays
np.array([1, 2, 3])          # [1 2 3]
np.zeros((3, 4))             # 3x4 matrix of 0s
np.ones((2, 3))              # 2x3 matrix of 1s
np.eye(3)                    # 3x3 identity matrix
np.arange(0, 10, 2)         # [0 2 4 6 8]
np.linspace(0, 1, 5)        # [0.   0.25 0.5  0.75 1.  ]
np.random.randn(3, 3)       # 3x3 standard normal

# Shape & reshape
a.shape                      # (rows, cols)
a.reshape(2, 6)              # change shape, same data
a.flatten()                  # always returns a copy — 1D
a.ravel()                    # returns a view when possible — 1D
a.T                          # transpose

# Indexing
a[0]                         # first row
a[:, 0]                      # first column
a[1:3, :]                    # rows 1 and 2, all columns
a[a > 5]                     # boolean indexing

# Math
np.sum(a)                    # sum of all elements
np.sum(a, axis=0)            # sum along columns
np.sum(a, axis=1)            # sum along rows
np.mean(a)
np.std(a)
np.max(a) / np.min(a)
np.argmax(a)                 # index of max value
np.dot(a, b)                 # matrix multiplication (also a @ b)
np.linalg.inv(a)             # matrix inverse
np.linalg.norm(a)            # L2 norm

# Stacking
np.vstack([a, b])            # stack vertically (row-wise)
np.hstack([a, b])            # stack horizontally (col-wise)
np.concatenate([a, b], axis=0)

# Broadcasting rule: dimensions are compatible if they are equal or one of them is 1
```

---

## Pandas

```python
import pandas as pd

# Create
pd.DataFrame({'col1': [1,2], 'col2': [3,4]})
pd.read_csv('file.csv')
pd.read_csv('file.csv', index_col=0, parse_dates=['date_col'])

# Inspect
df.shape                     # (rows, cols)
df.dtypes                    # data type of each column
df.head(5)                   # first 5 rows
df.tail(5)                   # last 5 rows
df.info()                    # dtypes + null counts
df.describe()                # stats for numeric columns
df.columns.tolist()          # list of column names
df.nunique()                 # unique values per column

# Select
df['col']                    # Series
df[['col1', 'col2']]         # DataFrame
df.loc[0:5, 'col1':'col3']   # label-based — inclusive on both ends
df.iloc[0:5, 0:3]            # position-based — exclusive on end

# Filter
df[df['age'] > 25]
df[(df['age'] > 25) & (df['city'] == 'Delhi')]
df.query('age > 25 and city == "Delhi"')

# Missing values
df.isnull().sum()            # null count per column
df.dropna()                  # drop rows with any null
df.fillna(0)                 # fill nulls with 0
df['col'].fillna(df['col'].mean())   # fill with mean

# Transform
df['col'].apply(lambda x: x * 2)
df.rename(columns={'old': 'new'})
df.drop(columns=['col1'])
df.sort_values('col', ascending=False)
df.reset_index(drop=True)

# Groupby
df.groupby('city')['sales'].sum()
df.groupby('city').agg({'sales': 'sum', 'age': 'mean'})

# Merge / Join
pd.merge(df1, df2, on='id', how='inner')   # inner, left, right, outer
pd.concat([df1, df2], axis=0)              # stack rows

# Value counts
df['col'].value_counts()
df['col'].value_counts(normalize=True)     # proportions
```

---

## Matplotlib

```python
import matplotlib.pyplot as plt

# Basic plot
plt.plot(x, y, color='blue', linewidth=2, label='train')
plt.scatter(x, y, c='red', s=50, alpha=0.6)
plt.bar(categories, values, color='steelblue')
plt.hist(data, bins=30, edgecolor='black')
plt.boxplot(data)

# Labels and formatting
plt.title('My Plot', fontsize=14)
plt.xlabel('X axis')
plt.ylabel('Y axis')
plt.legend()
plt.grid(True, alpha=0.3)
plt.tight_layout()

# Subplots
fig, axes = plt.subplots(1, 2, figsize=(12, 4))
axes[0].plot(x, y)
axes[0].set_title('Plot 1')
axes[1].scatter(x, y)
axes[1].set_title('Plot 2')
plt.tight_layout()
plt.show()

# Save
plt.savefig('plot.png', dpi=150, bbox_inches='tight')
plt.show()    # always call after savefig, not before
```

---

## Scikit-learn

```python
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.metrics import accuracy_score, mean_squared_error, r2_score, classification_report

# Split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# Scale
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)   # fit + transform on train
X_test_scaled  = scaler.transform(X_test)        # transform only on test — never fit on test

# Train any model
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
y_prob = model.predict_proba(X_test)[:, 1]       # probability of positive class

# Evaluate — classification
accuracy_score(y_test, y_pred)
print(classification_report(y_test, y_pred))

# Evaluate — regression
mean_squared_error(y_test, y_pred, squared=False)   # RMSE
r2_score(y_test, y_pred)

# Cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')
print(f"CV Accuracy: {scores.mean():.3f} ± {scores.std():.3f}")
```

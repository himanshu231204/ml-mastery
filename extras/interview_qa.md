# ML Interview Q&A

Concise answers to the most commonly asked ML interview questions.

---

## Fundamentals

**Q: What is the bias-variance tradeoff?**
Bias is error from wrong assumptions in the model (underfitting). Variance is error from sensitivity to small fluctuations in training data (overfitting). Increasing model complexity reduces bias but increases variance. The goal is to find the sweet spot where total error is minimized.

**Q: What is overfitting? How do you prevent it?**
Overfitting is when a model learns the training data too well, including noise, and fails to generalize to new data. Prevention: regularization (L1/L2), cross-validation, dropout, early stopping, more training data, feature selection, simpler model.

**Q: Explain the difference between L1 and L2 regularization.**
L1 (Lasso) adds the sum of absolute weights to the loss — encourages sparsity, drives some weights to exactly zero, useful for feature selection. L2 (Ridge) adds the sum of squared weights — shrinks weights but rarely to zero, handles correlated features better.

**Q: What is cross-validation and why do we need it?**
Cross-validation splits data into k folds, trains on k-1 folds, tests on the remaining fold, and repeats k times. It gives a more reliable estimate of model performance than a single train/test split, especially on small datasets.

---

## Algorithms

**Q: How does gradient descent work?**
It minimizes the cost function by iteratively updating parameters in the direction of the negative gradient. At each step: `θ = θ - α * ∂J/∂θ`, where α is the learning rate. Stochastic GD updates on one sample at a time; mini-batch GD updates on a small batch.

**Q: What is the difference between bagging and boosting?**
Bagging (e.g. Random Forest) trains multiple models in parallel on random subsets of data and averages predictions — reduces variance. Boosting (e.g. XGBoost) trains models sequentially where each model focuses on errors of the previous one — reduces bias.

**Q: Why does Random Forest perform better than a single Decision Tree?**
A single tree overfits easily. Random Forest trains many trees on random data subsets and random feature subsets, then aggregates predictions. The randomness reduces correlation between trees, and averaging their predictions reduces variance without increasing bias much.

**Q: What is the kernel trick in SVM?**
Instead of explicitly mapping data to a higher-dimensional space, the kernel function computes the dot product in that space directly. This makes it computationally feasible to find non-linear decision boundaries. Common kernels: RBF (Gaussian), polynomial, linear.

**Q: When would you use Naive Bayes over Logistic Regression?**
Naive Bayes works well with small data, high-dimensional data (text), and when the independence assumption roughly holds. It is faster to train. Logistic Regression generally performs better when you have enough data and features are correlated.

**Q: What is the difference between KNN for classification vs regression?**
Classification: takes majority vote among K nearest neighbors. Regression: takes the mean (or weighted mean) of K nearest neighbors' values. The distance metric and choice of K matter equally in both cases.

---

## Model Evaluation

**Q: When should you use AUC-ROC vs accuracy?**
Accuracy is misleading on imbalanced datasets. AUC-ROC measures the model's ability to distinguish between classes across all classification thresholds — use it when class imbalance exists. For highly imbalanced data, Precision-Recall AUC is often more informative than ROC AUC.

**Q: What is precision and recall? When do you optimize for each?**
Precision = TP / (TP + FP) — of all predicted positives, how many are actually positive. Recall = TP / (TP + FN) — of all actual positives, how many did we catch. Optimize precision when false positives are costly (spam detection). Optimize recall when false negatives are costly (cancer screening).

**Q: What is data leakage? Give an example.**
Data leakage is when information from outside the training data leaks into the model, giving artificially high performance. Example: fitting a scaler on the full dataset before splitting — the test set has influenced the scaling. Always fit preprocessing on training data only.

---

## Feature Engineering

**Q: Why do we need to scale features?**
Algorithms that compute distances (KNN, SVM) or use gradient descent (linear/logistic regression) are sensitive to feature magnitude. A feature on a 0-1 scale and another on a 0-100,000 scale will cause the algorithm to disproportionately weight the larger one.

**Q: What is the difference between StandardScaler and MinMaxScaler?**
StandardScaler centers data to mean 0 and std 1 — best when data is roughly Gaussian or when you need to preserve outlier information. MinMaxScaler scales to [0, 1] range — best for neural networks and when you know the bounds. Both must be fit only on training data.

**Q: How do you handle missing values?**
Numerical: mean/median imputation (median for skewed data), or model-based imputation. Categorical: mode imputation or a separate "Unknown" category. If missingness is informative, add a binary indicator column before imputing. Do not drop rows unless data is missing completely at random and the fraction is small.

**Q: What is the curse of dimensionality?**
As the number of features grows, the volume of the space increases exponentially — data becomes sparse and distances become less meaningful. Models need exponentially more data to generalize well. Solutions: dimensionality reduction (PCA), feature selection, regularization.

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

---

## 👨‍💻 Author

**Himanshu Kumar**

- 🌐 GitHub: [@himanshu231204](https://github.com/himanshu231204)
- 💼 LinkedIn: [himanshu231204](https://www.linkedin.com/in/himanshu231204)
- 🐦 Twitter/X: [@himanshu231204](https://twitter.com/himanshu231204)
- 📧 Email: himanshu231204@gmail.com


---

## Extended Q&A — 100 More Interview Questions

---

### Section 1: Mathematics and Statistics (Q1–Q15)

**Q1: What is the difference between population and sample variance? Why does sample variance use n-1?**
Population variance divides by N (all data points). Sample variance divides by n-1 (Bessel's correction) because the sample mean is itself estimated from the data, which introduces one degree of constraint. Dividing by n would systematically underestimate the true population variance. The n-1 correction makes the estimator unbiased.

**Q2: What is the Central Limit Theorem and why does it matter in ML?**
The CLT states that the mean of a large number of independent, identically distributed random variables approaches a normal distribution, regardless of the original distribution. In ML it justifies using normal-based confidence intervals for model performance estimates (e.g., CV scores), and explains why many features tend toward normality as they aggregate many small effects.

**Q3: What is maximum likelihood estimation (MLE)?**
MLE finds the parameter values that maximize the probability of observing the training data under the model. Formally: θ* = argmax_θ P(X | θ). Log-likelihood is used in practice to convert the product of probabilities into a sum. Linear regression (MSE) and logistic regression (cross-entropy) are both derived from MLE under specific distributional assumptions.

**Q4: What is the difference between a parametric and non-parametric model?**
Parametric models assume a fixed functional form with a finite number of parameters (e.g., linear regression: y = wx + b). The complexity is fixed regardless of data size. Non-parametric models make no strong assumptions about the functional form — their complexity grows with data (e.g., KNN, kernel SVM, decision trees). Non-parametric does not mean "no parameters" — it means parameters are not fixed in advance.

**Q5: What is covariance vs correlation? When would you use each?**
Covariance measures the direction of a linear relationship between two variables but is scale-dependent — a covariance of 1000 or 0.001 means different things for different features. Correlation normalizes covariance by the product of standard deviations, giving a dimensionless value in [-1, 1]. Use correlation when comparing relationships across features with different units. Use the covariance matrix directly in PCA and Gaussian models.

**Q6: What is a p-value? What are its limitations?**
A p-value is the probability of observing data at least as extreme as what was observed, assuming the null hypothesis is true. It does not tell you the probability that the null hypothesis is true. Common limitations: sensitive to sample size (tiny effects become significant with large n), does not measure effect size, binary threshold (p < 0.05) is arbitrary, and it can be misinterpreted as the probability that results are due to chance.

**Q7: Explain Type I and Type II errors. What controls the tradeoff?**
Type I error (false positive): rejecting the null hypothesis when it is actually true. Controlled by the significance level α. Type II error (false negative): failing to reject the null hypothesis when it is false. Controlled by statistical power (1 - β). Reducing α reduces Type I errors but increases Type II errors. The tradeoff is also equivalent to the precision-recall tradeoff in classification — adjusting the decision threshold shifts between them.

**Q8: What is a confusion matrix and what can you derive from it?**
A confusion matrix shows TP, TN, FP, FN for a classifier. From it you can derive: accuracy = (TP+TN)/total, precision = TP/(TP+FP), recall = TP/(TP+FN), F1 = harmonic mean of precision and recall, specificity = TN/(TN+FP), false positive rate = FP/(FP+TN). It captures the complete performance profile of a binary classifier at a fixed threshold.

**Q9: What is the difference between MAE and RMSE? When would you choose each?**
MAE (mean absolute error) takes the average of absolute residuals — it treats all errors equally and is robust to outliers. RMSE (root mean squared error) penalizes large errors more due to squaring — it is more sensitive to outliers. Choose MAE when outliers in the target are real data points that the model should handle gracefully. Choose RMSE when large errors are especially costly and should be penalized more heavily.

**Q10: What is the curse of dimensionality?**
As the number of features increases, the volume of the feature space grows exponentially. Data becomes increasingly sparse — the concept of "distance" loses meaning because all points become approximately equidistant. Consequences: KNN performs poorly, density estimation requires exponentially more data, overfitting becomes easier. Solutions: feature selection, dimensionality reduction (PCA), regularization.

**Q11: What is the difference between joint, marginal, and conditional probability?**
Joint probability P(A ∩ B): probability that both A and B occur simultaneously. Marginal probability P(A): probability of A regardless of B, obtained by summing (or integrating) over all values of B. Conditional probability P(A|B) = P(A ∩ B) / P(B): probability of A given that B has occurred. In ML, naive Bayes uses conditional probability, and the chain rule P(A,B) = P(A|B)P(B) underlies many generative models.

**Q12: What is entropy and how is it used in decision trees?**
Entropy measures the amount of uncertainty or disorder in a probability distribution: H = -Σ p_k log2(p_k). In decision trees, it measures the impurity of a node — entropy is 0 for a pure node (all one class) and 1 for a 50/50 binary split. Information gain = parent entropy - weighted sum of child entropies. The tree picks the split that maximizes information gain at each step.

**Q13: What is the difference between discriminative and generative models?**
Discriminative models (logistic regression, SVM, neural nets) learn P(y|x) directly — the decision boundary between classes. They are usually more accurate when you have enough data. Generative models (Naive Bayes, GMMs, HMMs) learn P(x|y) and P(y), then use Bayes theorem to compute P(y|x). They can generate new samples, work with less data, and handle missing features naturally, but require stronger assumptions.

**Q14: What is the difference between frequentist and Bayesian approaches?**
Frequentist statistics treats model parameters as fixed but unknown values estimated from data. Probability represents long-run frequency. Bayesian statistics treats parameters as random variables with a prior distribution P(θ), updated by data to get the posterior P(θ|X) = P(X|θ)P(θ)/P(X). Bayesian methods can incorporate prior knowledge and provide uncertainty estimates, but require choosing a prior and can be computationally expensive.

**Q15: What is the law of large numbers?**
The law of large numbers states that as the number of i.i.d. samples increases, the sample mean converges to the true population mean. In ML this justifies: CV scores as reliable performance estimates with enough folds, training loss as a proxy for generalization with enough data, and ensemble methods (averaging many models reduces variance toward the true expected prediction).

---

### Section 2: Linear and Logistic Regression (Q16–Q25)

**Q16: What are the assumptions of linear regression? What happens if they are violated?**
The five assumptions are: linearity (y is a linear function of X), independence (residuals are uncorrelated), homoscedasticity (constant residual variance), normality (residuals are normally distributed), and no multicollinearity (features are not perfectly correlated). Violations: non-linearity causes biased coefficients, heteroscedasticity makes standard errors unreliable, multicollinearity makes coefficient estimates unstable (but predictions may still be fine). Fixes: feature transformation, robust regression, Ridge regularization, VIF analysis.

**Q17: How do you interpret coefficients in linear regression?**
Each coefficient w_j represents the expected change in y for a one-unit increase in x_j, holding all other features constant. This interpretation assumes linearity and is only meaningful when features are on the same scale (after standardization). For log-transformed features or targets, interpret coefficients as percentage changes.

**Q18: What is multicollinearity and how do you detect/fix it?**
Multicollinearity occurs when two or more features are highly correlated. It makes coefficient estimates unstable (small changes in data cause large changes in coefficients) and inflates standard errors. Detection: correlation matrix, Variance Inflation Factor (VIF > 5-10 indicates multicollinearity). Fixes: remove one of the correlated features, use PCA to create uncorrelated components, use Ridge regression (L2 regularization stabilizes coefficient estimates under multicollinearity).

**Q19: Why is log loss better than MSE for logistic regression?**
MSE combined with the sigmoid activation creates a non-convex loss surface with many local minima — gradient descent may not converge to the global optimum. Log loss (cross-entropy) is convex when combined with the sigmoid function, so gradient descent is guaranteed to find the global minimum. Additionally, log loss heavily penalizes confident wrong predictions (log(0) → ∞), which is the right behavior for classification.

**Q20: What is the difference between odds and probability? What are log-odds?**
Probability p ∈ [0,1] gives the likelihood of an event. Odds = p/(1-p) ∈ [0, ∞), which is unbounded but only positive. Log-odds (logit) = log(p/(1-p)) ∈ (-∞, ∞), which is unbounded in both directions. Logistic regression models log-odds as a linear function of features: log(p/(1-p)) = w·x + b. This maps the linear combination to a probability via the sigmoid function.

**Q21: What is the decision boundary of logistic regression? Can it be non-linear?**
The decision boundary is where the predicted probability equals 0.5, which occurs when w·x + b = 0 — a linear hyperplane in feature space. Without transformation, logistic regression can only create a linear boundary. To model non-linear boundaries, you add polynomial features (x², x₁x₂, etc.) to create a richer feature space where a linear boundary corresponds to a non-linear boundary in original space.

**Q22: What is regularization? Why is it necessary?**
Regularization adds a penalty term to the loss function to discourage overly complex models. Without it, models (especially linear models with many features) can memorize training data by assigning arbitrarily large weights. L1 (Lasso): penalty = λΣ|w_j|, drives some weights to zero (feature selection). L2 (Ridge): penalty = λΣw_j², shrinks all weights but rarely to zero. Both reduce variance at the cost of slightly increased bias.

**Q23: What is the difference between Ridge and Lasso in terms of geometry?**
The constraint regions have different shapes. Ridge L2 constraint: w₁² + w₂² ≤ t² (a circle/sphere) — smooth edges, so the optimum rarely lands exactly on an axis. Lasso L1 constraint: |w₁| + |w₂| ≤ t (a diamond/polytope) — corners at the axes, so the optimum frequently lands at a corner where one coordinate is exactly zero. This geometric difference explains why Lasso produces sparse solutions and Ridge does not.

**Q24: What is the normal equation for linear regression? When should you not use it?**
The normal equation gives the exact solution: w* = (X^T X)^{-1} X^T y. It requires no iterations or learning rate. Avoid it when: (1) n or d is large — computing (X^T X)^{-1} is O(d³) time, (2) X^T X is singular (multicollinear features) — Ridge adds λI to regularize: w* = (X^T X + λI)^{-1} X^T y, (3) you need online/incremental updates — gradient descent can incorporate new data without recomputing from scratch.

**Q25: How does class imbalance affect logistic regression? How do you handle it?**
Logistic regression minimizes cross-entropy averaged over all samples. With imbalanced classes, the model tends to predict the majority class because this minimizes average loss. Fixes: class_weight='balanced' (upweights minority class in loss), oversample minority class (SMOTE), undersample majority class, adjust classification threshold, use precision-recall AUC instead of ROC-AUC as the evaluation metric.

---

### Section 3: Trees and Ensembles (Q26–Q38)

**Q26: How does a decision tree decide the best split?**
At each node, the tree evaluates every feature and every possible threshold. For each candidate split, it computes the weighted impurity of the two child nodes. The split that maximizes information gain (entropy reduction) or Gini gain is selected. For regression, variance reduction is used instead. The brute-force search is O(nd log n) per level, where n = samples and d = features.

**Q27: What is pruning in decision trees? What are the two types?**
Pruning removes branches that provide little predictive power to reduce overfitting. Pre-pruning (early stopping): stop splitting when the node has too few samples (min_samples_split), the depth limit is reached (max_depth), or the impurity decrease is below a threshold. Post-pruning: grow the full tree then remove branches that do not improve validation performance. Sklearn supports cost-complexity pruning via ccp_alpha.

**Q28: Why does Random Forest have lower variance than a single decision tree?**
For B trees each with variance σ² and pairwise correlation ρ, the variance of their average is ρσ² + (1-ρ)/B × σ². As B→∞, variance approaches ρσ². Random Forest reduces ρ (correlation between trees) through two mechanisms: (1) training each tree on a bootstrap sample, and (2) considering only a random subset of features at each split. Lower correlation → lower variance floor, which is why RF outperforms plain Bagging.

**Q29: What is out-of-bag (OOB) error in Random Forest?**
Each bootstrap sample contains ~63.2% of the training data. The remaining ~36.8% (out-of-bag samples) were never seen by that particular tree. For each training sample, predictions are collected only from trees that did not see it during training. These OOB predictions form a natural validation set, giving a nearly unbiased estimate of test performance without needing a separate validation set.

**Q30: What is feature importance in tree-based models? What are its limitations?**
Mean Decrease in Impurity (MDI): average total reduction in impurity (Gini or entropy) caused by splits on each feature, weighted by sample count, averaged across all trees. Limitation: biased toward features with many unique values or high cardinality because they offer more split thresholds. Alternative: permutation importance (shuffle each feature and measure performance drop) — slower but unbiased and model-agnostic.

**Q31: What is the difference between Bagging and Boosting?**
Bagging (Bootstrap Aggregating): trains multiple models in parallel on random subsets of data, then averages predictions. Reduces variance. Each model is independent. Examples: Random Forest. Boosting: trains models sequentially, where each new model focuses on errors made by previous models. Reduces bias. Models are dependent. Examples: AdaBoost, Gradient Boosting, XGBoost. Bagging is better when the base model has high variance (deep trees). Boosting is better when the base model has high bias (shallow trees).

**Q32: How does Gradient Boosting work?**
Gradient Boosting builds an ensemble of weak learners (typically shallow trees) sequentially. At each step t, it fits a new tree h_t(x) to the negative gradient of the loss function with respect to the current ensemble prediction. For MSE loss, this is simply the residuals y - F_{t-1}(x). The prediction is updated: F_t(x) = F_{t-1}(x) + α × h_t(x), where α is the learning rate. It effectively does gradient descent in function space.

**Q33: What are the key hyperparameters of Gradient Boosting?**
n_estimators: number of trees — more trees reduce training error but increase risk of overfitting. learning_rate (shrinkage): controls step size — smaller = lower variance but needs more trees. max_depth: depth of each tree — shallow trees (3-5) are typical for boosting. subsample: fraction of samples per tree — acts as stochastic regularization. min_samples_leaf: smooths predictions. The n_estimators and learning_rate must be tuned jointly — smaller learning_rate requires more estimators.

**Q34: What is XGBoost and how does it differ from standard Gradient Boosting?**
XGBoost adds several improvements over standard GBM: (1) regularization terms (L1 and L2) directly in the objective to prevent overfitting, (2) second-order Taylor expansion of the loss for more accurate gradient computation, (3) built-in handling of missing values, (4) column subsampling (like Random Forest feature randomness), (5) parallel tree construction within each boosting round, (6) cache-aware and out-of-core computation for large datasets.

**Q35: Why are tree-based models robust to outliers?**
Decision trees split data into regions based on feature thresholds. An extreme outlier only affects the split if it changes which threshold is optimal. In practice, trees split at the median of two adjacent values — an extreme outlier just makes the range wider but does not change the optimal split threshold. Predictions at leaf nodes are means or modes, which are less affected by individual extreme values than in linear models.

**Q36: What is the difference between hard voting and soft voting in ensembles?**
Hard voting: each model predicts a class label, majority wins. Each model gets one vote regardless of confidence. Soft voting: each model outputs class probabilities, which are averaged across models, then the class with the highest average probability is predicted. Soft voting is generally better because it weights confident predictions more heavily and produces better-calibrated probability estimates.

**Q37: When would you choose Random Forest over Gradient Boosting?**
Choose Random Forest when: training speed is important (parallelizable), you want to avoid tuning many hyperparameters, data has many noisy features (RF's feature randomness handles this well), or you need OOB error estimates. Choose Gradient Boosting when: maximum predictive performance is the goal, you have time to tune hyperparameters, data is relatively clean, or you need feature importance for interpretation.

**Q38: What is stacking (stacked generalization)?**
Stacking trains multiple diverse base models (level-0) and uses their predictions as input features to train a meta-model (level-1). The meta-model learns how to best combine the base model predictions. To avoid leakage, base models are trained on k-fold CV folds and out-of-fold predictions are used as meta-features. Stacking often outperforms individual models and simple voting but is computationally expensive.

---

### Section 4: Support Vector Machines and Kernel Methods (Q39–Q45)

**Q39: What is the kernel trick and why is it powerful?**
The kernel trick avoids explicitly mapping data to a higher-dimensional space φ(x). Instead, it replaces all inner products x_i · x_j in the dual SVM problem with a kernel function K(x_i, x_j) = φ(x_i) · φ(x_j). The RBF kernel corresponds to an infinite-dimensional feature space — you get the power of infinite features without ever computing them. This makes non-linear SVM computationally feasible.

**Q40: What does the C parameter control in SVM? What happens at extremes?**
C is the regularization parameter (inverse of regularization strength). Large C: small slack allowed, narrow margin, model tries hard to classify all training points correctly — low bias, high variance, risk of overfitting. Small C: large slack allowed, wide margin, more misclassifications tolerated on training data — higher bias, lower variance. C = 1/λ in the hinge loss formulation, so reducing C is equivalent to increasing regularization strength.

**Q41: What is the gamma parameter in RBF kernel SVM?**
γ controls the width of the Gaussian kernel: K(x_i, x_j) = exp(-γ||x_i - x_j||²). Large γ: the kernel decays quickly with distance — each training point has very local influence, decision boundary is complex and can overfit. Small γ: the kernel decays slowly — each training point influences a wider region, decision boundary is smoother. Must tune C and γ together — they interact strongly.

**Q42: Why must you scale features before SVM?**
SVM relies on computing distances (||x_i - x_j||²) between points. If one feature has range [0, 1000] and another has range [0, 1], the distance is almost entirely determined by the large-scale feature. The model effectively ignores the small-scale feature. After standardization, all features contribute equally to distance computations, and the optimal hyperplane can be found in a balanced space.

**Q43: What are support vectors? What happens to non-support vectors?**
Support vectors are the training points that lie on or within the margin boundaries (satisfy y_i(w·x_i + b) ≤ 1). The optimal weight vector is a linear combination of support vectors only: w* = Σ α_i y_i x_i where α_i > 0 only for support vectors. All other training points have α_i = 0 — they could be removed from the training set without changing the model. This makes SVM memory-efficient.

**Q44: How does SVM handle multi-class classification?**
SVM is inherently binary. Two common extensions: One-vs-Rest (OvR): train K binary classifiers, one per class (class k vs all others). Predict the class whose classifier gives the highest decision function value. One-vs-One (OvO): train K(K-1)/2 binary classifiers, one for each pair of classes. Predict by majority vote. OvO is the sklearn default — it trains more models but each on fewer samples, and often performs better.

**Q45: When would you not use SVM?**
Avoid SVM when: (1) dataset is large (n > 10,000) — SVC is O(n²) to O(n³) in time, use LinearSVC or SGDClassifier instead, (2) many features but sparse data (text) — linear models handle this better, (3) you need well-calibrated probabilities without additional computation (SVC requires Platt scaling), (4) interpretability is required — SVM coefficients are hard to interpret with non-linear kernels.

---

### Section 5: Clustering and Unsupervised Learning (Q46–Q53)

**Q46: What are the limitations of K-Means?**
K-Means assumes: clusters are spherical (equal variance in all directions), clusters have roughly equal size, the number of clusters K is known in advance. It fails on: non-convex shapes (moons, rings), clusters with very different sizes or densities. It is sensitive to outliers (they pull centroids), sensitive to initialization (use K-Means++), and cannot detect noise points. Solutions: DBSCAN for arbitrary shapes, GMM for soft assignments.

**Q47: How does DBSCAN find clusters? What makes it different from K-Means?**
DBSCAN defines clusters as connected regions of high density. A core point has at least min_samples neighbors within radius ε. Points density-reachable from core points form a cluster. Points not reachable from any core point are noise (labeled -1). Differences from K-Means: does not require specifying K in advance, handles arbitrary shapes, explicitly identifies outliers, but requires tuning ε and min_samples, and struggles with varying density clusters.

**Q48: What is the silhouette score? How do you interpret it?**
For each point i: a(i) = mean distance to all other points in the same cluster (cohesion). b(i) = mean distance to all points in the nearest other cluster (separation). s(i) = (b(i) - a(i)) / max(a(i), b(i)) ∈ [-1, 1]. Score close to +1: well-clustered, far from neighboring cluster. Score close to 0: on the cluster boundary. Score close to -1: may be in the wrong cluster. Mean silhouette score across all points is used to compare different K values.

**Q49: What is PCA and what problem does it solve?**
PCA finds an orthogonal linear transformation of the data that aligns the new coordinate axes with the directions of maximum variance. It solves: (1) dimensionality reduction — project to k < d dimensions while retaining maximum variance, (2) decorrelation — the principal components are uncorrelated by construction, (3) noise reduction — lower components often capture noise, (4) visualization — project to 2-3 dimensions for visual exploration. PCA is a linear technique and does not preserve non-linear structure.

**Q50: What is the difference between PCA and t-SNE?**
PCA is linear, deterministic, fast (O(nd²)), and preserves global variance structure — good for feature extraction and preprocessing. t-SNE is non-linear, stochastic, slow (O(n²)), and optimizes to preserve local neighborhood structure — good for visualization only. t-SNE output cannot be used for downstream ML tasks (distances are not meaningful, the map changes with random seed). Use PCA for feature reduction before modeling, t-SNE only for visualization.

**Q51: How do you evaluate clustering when there are no true labels?**
Internal metrics (no labels needed): Silhouette score (cohesion vs separation), Davies-Bouldin index (lower = better, measures cluster similarity), Calinski-Harabasz index (higher = better, ratio of between-cluster to within-cluster variance), Inertia (K-Means within-cluster sum of squares — use the elbow method). External metrics (when labels are available): Adjusted Rand Index (ARI), Normalized Mutual Information (NMI), Fowlkes-Mallows score.

**Q52: What is the Elbow method and why is it sometimes ambiguous?**
The elbow method plots inertia (within-cluster sum of squares) vs K. The "elbow" is where inertia stops decreasing rapidly, suggesting the optimal K. It is ambiguous when the true clusters are not well-separated — the curve is smooth without a clear kink. In that case, use silhouette score (which has a clear maximum) or domain knowledge. The elbow is a heuristic, not a definitive rule.

**Q53: What is the difference between hard and soft clustering?**
Hard clustering: each point belongs to exactly one cluster (K-Means, DBSCAN). Soft (fuzzy) clustering: each point has a probability of belonging to each cluster. Gaussian Mixture Models (GMM) use the EM algorithm to find soft cluster assignments — each point has responsibility r_ik = P(cluster k | point i). Soft clustering is more appropriate when cluster boundaries are ambiguous or when you need uncertainty estimates about cluster membership.

---

### Section 6: Neural Networks and Deep Learning Basics (Q54–Q60)

**Q54: What is a neuron in a neural network? What does it compute?**
A neuron computes z = w·x + b (linear transformation), then applies a non-linear activation function: a = f(z). The linear part allows learning weights that scale and combine input features. Without the non-linear activation, stacking multiple layers would collapse to a single linear transformation. The activation introduces the non-linearity that allows neural networks to learn complex functions.

**Q55: What is backpropagation? How does it work?**
Backpropagation efficiently computes the gradient of the loss with respect to all weights using the chain rule of calculus. Forward pass: compute activations layer by layer from input to output and compute loss. Backward pass: propagate the error gradient from output to input, layer by layer, using: ∂L/∂w^l = δ^l · (a^{l-1})^T where δ^l = (∂L/∂z^l) is the error signal. The key insight is that these gradients can be reused efficiently across layers, making it O(number of parameters) rather than O(parameters²).

**Q56: What is vanishing/exploding gradient problem?**
In deep networks, gradients are multiplied together through many layers during backpropagation. If weights are initialized small or activations like sigmoid saturate near 0 or 1, gradients shrink exponentially with depth (vanishing) — early layers learn extremely slowly. If weights are large, gradients grow exponentially (exploding) — training becomes unstable. Solutions for vanishing: ReLU activations, batch normalization, residual connections (skip connections). Solutions for exploding: gradient clipping, careful initialization.

**Q57: What are common activation functions and when do you use each?**
Sigmoid: σ(z) = 1/(1+e^{-z}), output ∈ (0,1) — used for binary output, not in hidden layers (vanishing gradient). Tanh: output ∈ (-1,1), zero-centered, better than sigmoid but still vanishes. ReLU: f(z) = max(0,z) — fast, avoids vanishing gradient for positive inputs, but "dying ReLU" problem. Leaky ReLU: small slope for negative inputs, avoids dying ReLU. GELU/SiLU: smoother versions of ReLU used in transformers. Softmax: multi-class output layer — converts logits to probabilities summing to 1.

**Q58: What is dropout regularization?**
During training, dropout randomly sets a fraction p (dropout rate) of neuron activations to zero in each forward pass. This forces the network to learn redundant representations because it cannot rely on any single neuron always being present. Effectively trains an ensemble of 2^n sub-networks. During inference, all neurons are used but activations are scaled by (1-p) to compensate. Reduces overfitting significantly in large networks.

**Q59: What is batch normalization?**
Batch normalization normalizes the activations of each layer to zero mean and unit variance across the mini-batch, then applies learnable scale and shift parameters: y = γ × (x - μ_B)/σ_B + β. Benefits: reduces internal covariate shift (distribution of activations changes during training), allows higher learning rates, acts as regularization, makes training less sensitive to initialization. Applied before or after the activation function (before is more common).

**Q60: What is the difference between batch gradient descent, SGD, and mini-batch gradient descent?**
Batch GD: computes gradient on the entire dataset — accurate gradient but slow per update, cannot use for online learning. SGD: computes gradient on one sample — noisy but fast, can escape local minima due to noise. Mini-batch GD: computes gradient on a small batch (32-256 samples) — balances accuracy and speed, leverages GPU parallelism. In practice "SGD" usually means mini-batch GD. Adam optimizer adapts learning rates per parameter using running estimates of gradient mean and variance.

---

### Section 7: Model Evaluation and Validation (Q61–Q72)

**Q61: What is data leakage? Give three examples.**
Data leakage occurs when information from the test/future data leaks into training, causing overly optimistic performance estimates. Examples: (1) Fitting a StandardScaler on the full dataset before train/test split — test distribution influences training normalization. (2) Including the target variable as a feature — directly encodes the answer. (3) Using future data to predict the past in time series — features computed from data after the prediction time horizon. (4) Imputing missing values using the global mean rather than the training mean.

**Q62: What is the difference between validation set and test set?**
Validation set: used to tune hyperparameters, select models, and make decisions during the development cycle. It is used multiple times. Test set: used exactly once to report final performance after all decisions are made. If you use the test set to make any decision (including choosing between two final models), it becomes a validation set and you need a new test set. The test set represents the final unbiased performance estimate.

**Q63: What is nested cross-validation and why is it needed?**
Standard GridSearchCV + test set evaluation is optimistically biased — the test set indirectly influenced hyperparameter selection. Nested CV has two loops: outer K-fold CV evaluates performance, inner K-fold CV performs hyperparameter tuning within each outer fold. The outer test folds are never used in any decision. This provides an unbiased estimate of how well the entire model selection procedure will generalize — not just a specific model.

**Q64: When should you use stratified cross-validation?**
Always use stratified CV for classification tasks, especially with imbalanced classes. Stratification ensures each fold has the same class distribution as the full dataset. Without stratification, some folds might contain very few or no minority class samples, making evaluation unreliable. StratifiedKFold in sklearn maintains class proportions automatically. For regression, standard KFold is usually fine.

**Q65: What is the AUC-ROC? What is its probabilistic interpretation?**
AUC (Area Under the ROC Curve) equals the probability that a randomly chosen positive example gets a higher predicted score than a randomly chosen negative example: P(score_positive > score_negative). AUC = 1.0 is perfect, 0.5 is random. AUC is threshold-independent and robust to class imbalance — it evaluates the model's ranking ability across all possible thresholds. Use PR-AUC instead of ROC-AUC when the positive class is rare (<5%).

**Q66: What is the F-beta score and when would you use β > 1 vs β < 1?**
F_β = (1+β²) × (P×R) / (β²×P + R). β controls how much more you weight recall vs precision. β = 1: equal weight (standard F1). β = 2: recall is twice as important as precision — use when false negatives are especially costly (disease screening — missing a sick patient is worse than a false alarm). β = 0.5: precision is twice as important — use when false positives are especially costly (spam filter — wrongly flagging a legitimate email is worse than missing spam).

**Q67: What is calibration and why does it matter?**
A well-calibrated model means that when it predicts P(y=1|x) = 0.7, approximately 70% of those examples actually belong to class 1. Poorly calibrated models may be accurate (correct ranking) but have misleading probability estimates. Matters when: probabilities are used for downstream decisions (medical risk scores, fraud thresholds), or when combining predictions from multiple models. Calibration curve (reliability diagram) checks this. Fix with CalibratedClassifierCV using isotonic regression or Platt scaling.

**Q68: What is the difference between precision@k and mean average precision (MAP)?**
Precision@k: of the top-k predicted items, what fraction is relevant. Used in recommendation systems. Average Precision (AP): area under the precision-recall curve, computed as the weighted mean of precisions at each recall threshold. Mean Average Precision (MAP): average of AP across multiple queries or classes — the standard metric for information retrieval and object detection.

**Q69: How do you evaluate a regression model beyond R² and RMSE?**
Residual plots (residuals vs fitted values — should show no pattern), Q-Q plot (residuals should be normally distributed), scale-location plot (square root of standardized residuals vs fitted — checks homoscedasticity), Cook's distance (identifies influential points), Durbin-Watson test (checks autocorrelation in residuals), VIF (variance inflation factor for multicollinearity), and comparing against a simple baseline (predicting the mean gives R²=0, RMSE=target std).

**Q70: What is learning curve analysis? How do you diagnose model problems?**
Plot training and validation error vs training set size. High bias (underfitting): both curves plateau at high error — adding more data does not help, model is too simple. High variance (overfitting): training error is low but validation error is much higher — large gap, model is too complex or too little data. Converged well: both curves are low and close to each other — good fit. Use this to decide: if high bias, increase model complexity. If high variance, get more data or regularize.

**Q71: What is a validation curve? How do you use it?**
A validation curve plots training and validation performance as a function of a single hyperparameter (e.g., C for SVM, max_depth for trees). Helps identify: underfitting region (both train and val performance are low — hyperparameter too constrained), overfitting region (train performance is high, val is low — hyperparameter too flexible), sweet spot (where val performance peaks). Use cross-validation for the validation scores to get a reliable estimate.

**Q72: What is SMOTE and when should you use it?**
SMOTE (Synthetic Minority Over-sampling Technique) generates synthetic minority class samples by interpolating between existing minority samples and their k nearest neighbors in feature space. Use when: class imbalance is severe (>10:1 ratio) and you cannot collect more real minority samples. Apply SMOTE only to the training set (not test). Alternatives: class_weight='balanced' in sklearn (simpler, no synthetic data), undersampling the majority class, or generating synthetic data with a generative model.

---

### Section 8: Feature Engineering and Data Preprocessing (Q73–Q82)

**Q73: What is target encoding and what is the risk?**
Target encoding replaces a categorical feature with the mean target value for that category. It is compact (one column instead of K columns for OHE) and handles high-cardinality features. The risk is target leakage — the encoded value directly incorporates target information, causing the model to overfit. Solution: use cross-validation-based target encoding (encode using out-of-fold means), or Bayesian smoothing: encode(c) = (n_c × mean_c + α × global_mean) / (n_c + α), pulling rare categories toward the global mean.

**Q74: When should you use StandardScaler vs MinMaxScaler vs RobustScaler?**
StandardScaler (z-score): default choice for gradient-based models (logistic regression, SVM, neural nets), PCA, KNN. Assumes approximately Gaussian distribution. MinMaxScaler ([0,1] range): when algorithm requires bounded inputs (some neural nets), image pixel values. Very sensitive to outliers — a single extreme value compresses all others. RobustScaler (median/IQR): when data has significant outliers you cannot remove — uses median and IQR, so outliers have minimal effect on the transform.

**Q75: What is the difference between missing MCAR, MAR, and MNAR?**
MCAR (Missing Completely At Random): missingness is independent of any variable — safe to delete or impute. MAR (Missing At Random): missingness depends on other observed variables but not on the missing value itself — use multiple imputation using those other variables. MNAR (Missing Not At Random): missingness depends on the missing value itself (e.g., high-income people refuse to report income) — hardest to handle, may need to model the missingness mechanism. Ignoring MNAR can introduce bias.

**Q76: What is feature selection vs feature extraction? Give examples of each.**
Feature selection: choose a subset of the original features without transformation. Examples: Lasso (drives irrelevant weights to zero), RFE (recursive feature elimination), variance threshold, mutual information. Feature extraction: create new features from the original ones, often of lower dimensionality. Examples: PCA (linear combination maximizing variance), t-SNE (non-linear), autoencoders (learned non-linear compression), polynomial features (expand feature space).

**Q77: What is the Variance Inflation Factor (VIF) and how do you use it?**
VIF measures how much the variance of a coefficient is inflated due to multicollinearity. For feature j: VIF_j = 1/(1 - R²_j), where R²_j is the R² of regressing feature j on all other features. VIF = 1: no multicollinearity. VIF > 5: moderate, consider removing. VIF > 10: severe, strongly consider removing. Fix: remove one of the collinear pair, use PCA, or use Ridge regression which handles multicollinearity naturally.

**Q78: How do you handle high-cardinality categorical features?**
Options: (1) Target encoding with cross-validation or smoothing (compact, data-driven). (2) Frequency encoding — replace category with its frequency of occurrence. (3) Embedding (for neural nets) — learn a dense representation. (4) Hashing trick — map categories to a fixed number of buckets using a hash function (handles unseen categories, some collision risk). (5) Group rare categories — combine categories with count < threshold into "Other". (6) Leave as ordinal if there is a meaningful order.

**Q79: What is interaction features and when do you add them?**
Interaction features are products of two or more features: x₁ × x₂. They allow linear models to capture relationships where the effect of one feature depends on the value of another (interaction effects). When to add: when domain knowledge suggests a relationship (e.g., age × income for credit scoring), when EDA shows different slopes for subgroups, or when a linear model underfits and adding polynomial/interaction features improves performance. Always add regularization (Ridge/Lasso) when adding many interaction features.

**Q80: What is the difference between normalization and standardization?**
Normalization (MinMaxScaler): scales data to [0,1] or [-1,1] range — preserves relative distances, sensitive to outliers, loses shape of distribution. Standardization (StandardScaler): scales to mean 0, std 1 — does not bound the range, robust to outliers (compared to normalization), preserves shape of distribution. The terms are often used interchangeably in practice but technically normalization = MinMax scaling, standardization = z-score scaling.

**Q81: Why should you never impute before splitting data?**
If you impute using the mean/median computed on the full dataset (including test data), the test data's statistics leak into the training process. This inflates performance estimates because the model has seen statistical information about test samples through the imputed values. Always compute imputation statistics on training data only and apply the same transform to test data — use sklearn's Pipeline to enforce this automatically.

**Q82: What is the difference between feature importance from MDI vs permutation?**
MDI (Mean Decrease in Impurity): computed during tree building — sum of impurity reduction at nodes that use that feature. Fast but biased: inflates importance of high-cardinality features (more split thresholds to choose from) and correlated features. Permutation importance: randomly shuffles each feature and measures the decrease in model performance. Slower but unbiased, model-agnostic, reflects true impact on predictions including non-linear effects. Use permutation importance when features are correlated or have varying cardinality.

---

### Section 9: System Design and Practical ML (Q83–Q100)

**Q83: How would you approach a new ML problem from scratch?**
(1) Understand the business problem — what decision does the model enable, what is the cost of errors. (2) Define the ML task — classification, regression, ranking, etc. (3) Identify data sources and collect data. (4) EDA — distributions, missing values, correlations, class balance. (5) Establish a simple baseline — mean predictor for regression, majority class for classification. (6) Feature engineering based on domain knowledge and EDA. (7) Model selection with cross-validation. (8) Hyperparameter tuning. (9) Final evaluation on held-out test set. (10) Error analysis — understand where the model fails.

**Q84: What is a data pipeline and why is reproducibility important?**
A data pipeline is a sequence of automated steps that transform raw data into model-ready features. Reproducibility matters because: (1) debugging requires re-running the exact same preprocessing, (2) serving requires applying identical transforms to new data, (3) experiments must be reproducible to compare models fairly. Use sklearn Pipelines (auto-prevent leakage), version control data (DVC), set random seeds, and log all preprocessing parameters.

**Q85: How do you handle concept drift in production?**
Concept drift is when the statistical properties of the target or features change over time, degrading model performance. Detection: monitor prediction distribution, feature distributions, and model performance metrics over time. Statistical tests: KS test, PSI (Population Stability Index). Handling: retrain periodically (scheduled retraining), retrain on trigger (when metrics degrade), use online/incremental learning, use time-based feature weighting (down-weight old samples).

**Q86: What metrics would you monitor in a deployed ML model?**
Technical metrics: prediction distribution drift, feature distribution drift (PSI), model latency (p50, p95, p99), throughput (requests per second), error rate. Business metrics: click-through rate, conversion rate, revenue, customer churn — whatever the model ultimately affects. Data quality: missing feature rate, out-of-range values, schema violations. Model performance: accuracy/RMSE computed on a sample with ground truth labels (when available, possibly delayed).

**Q87: How do you decide whether to collect more data or tune the model?**
Look at the learning curve. If training error ≈ validation error but both are high: high bias — collect more data does NOT help significantly, improve the model (more complex model, better features). If training error << validation error: high variance — collect more data WILL help, also try regularization. More data is almost always helpful but has diminishing returns — check whether the validation error is still decreasing as you add more training examples.

**Q88: What is the difference between online learning and batch learning?**
Batch learning: model is trained on the full dataset at once, then deployed. To update the model with new data, retrain from scratch. Suitable for most offline ML tasks. Online learning: model is updated incrementally as new data arrives, one sample or mini-batch at a time. Suitable for streaming data, large datasets that don't fit in memory, or when data distribution changes over time (concept drift). sklearn's SGDClassifier and SGDRegressor support online learning via partial_fit().

**Q89: What is A/B testing and how does it relate to model evaluation?**
A/B testing serves two model versions (A=control, B=treatment) to different user groups simultaneously, then measures the business metric difference. It is the gold standard for evaluating a model's real-world impact. Key requirements: random assignment, sufficient sample size (power analysis), single metric to optimize, run until statistical significance. Common mistakes: stopping early when you see significance, running too many simultaneous tests (multiple comparison problem), ignoring novelty effects.

**Q90: What is the difference between precision and recall in a search engine context?**
Precision: of all documents returned, what fraction is relevant — measures result quality. Recall: of all relevant documents in the corpus, what fraction was returned — measures completeness. In search, users care more about precision (top results should be relevant) — showing irrelevant results is worse than missing some relevant ones. In a safety-critical recall system (e.g., detecting all defective products), recall matters more — missing a defective item is worse than some false alarms.

**Q91: What is transfer learning?**
Transfer learning reuses a model trained on one task or dataset to improve performance on a different but related task. The pretrained model has already learned general features (edges, shapes, language patterns). Two strategies: feature extraction (freeze pretrained layers, train only a new head on your data) and fine-tuning (update all or some pretrained weights with a small learning rate on your dataset). Especially effective when your dataset is small and similar to the pretraining domain.

**Q92: What is the difference between generative and discriminative models in the context of data generation?**
Discriminative models only learn the decision boundary P(y|x) — they cannot generate new samples. Generative models learn the joint distribution P(x,y) = P(x|y)P(y) — they can generate new samples by sampling from P(x|y). Examples of generative models: VAEs (variational autoencoders), GANs (generative adversarial networks), Gaussian Mixture Models, Naive Bayes. Generative models are useful for data augmentation, anomaly detection, and semi-supervised learning.

**Q93: What is class imbalance and how do you handle it beyond resampling?**
Beyond SMOTE/oversampling: (1) class_weight='balanced' in sklearn — scales loss contribution of minority samples, (2) threshold adjustment — lower classification threshold to increase recall for minority class, (3) use appropriate metrics — F1, AUC-ROC, PR-AUC rather than accuracy, (4) anomaly detection framing — treat minority class as anomalies, (5) cost-sensitive learning — specify a misclassification cost matrix, (6) ensemble methods designed for imbalance (EasyEnsemble, BalancedRandomForest).

**Q94: What is the difference between structured and unstructured data? How do you handle each?**
Structured data: tabular format with rows and columns, well-defined schema (SQL tables, CSV). Classical ML algorithms (tree ensembles, logistic regression) work directly. Unstructured data: no predefined structure (images, text, audio, video). Requires feature extraction: for text (TF-IDF, word embeddings, transformers), for images (CNNs, pretrained features like ResNet), for audio (MFCCs, spectrograms). Deep learning typically handles unstructured data end-to-end.

**Q95: How do you handle class imbalance in multi-class settings?**
Compute per-class weights: w_c = n_total / (n_classes × n_c) and set class_weight parameter. Use macro-averaged or weighted F1 instead of accuracy. Apply SMOTE per class or use sklearn's imblearn. Split evaluation with stratified CV to ensure each fold has all classes represented. Consider hierarchical classification if some classes are very rare. Monitor per-class precision and recall in the classification report to identify which classes are poorly predicted.

**Q96: What is model interpretability and why does it matter?**
Interpretability is the degree to which humans can understand model predictions. It matters for: (1) trust — stakeholders need to understand why the model makes predictions, (2) debugging — identifying what patterns the model is learning incorrectly, (3) fairness — detecting discriminatory patterns, (4) regulatory compliance (GDPR's right to explanation), (5) domain expert validation. Methods: intrinsically interpretable models (logistic regression, shallow trees), SHAP (SHapley Additive exPlanations), LIME (local approximations), partial dependence plots.

**Q97: What is SHAP and how does it work?**
SHAP (SHapley Additive exPlanations) assigns each feature a contribution to a specific prediction based on Shapley values from cooperative game theory. The Shapley value for feature j is the average marginal contribution of feature j across all possible orderings of features. Key properties: efficiency (SHAP values sum to the model output minus the baseline), symmetry (identical features get equal values), dummy (features with no effect get zero). TreeSHAP computes exact Shapley values for tree models in polynomial time.

**Q98: What is the difference between a model that memorizes and one that generalizes?**
A memorizing model (high variance) fits the training data perfectly, including noise — it learns the specific idiosyncrasies of the training set rather than the underlying pattern. Performance on unseen data degrades significantly. A generalizing model captures the true underlying relationship and performs similarly on training and test data. Indicators of memorization: training accuracy much higher than validation accuracy, model behaves unexpectedly on slightly perturbed inputs. Fixes: regularization, simpler model, more data, cross-validation.

**Q99: What is the difference between correlation and causation in ML?**
Correlation measures the statistical relationship between two variables — if X and Y move together. Causation means X directly causes Y. ML models capture correlations, not causation. A model can achieve high accuracy by correlating with confounders (e.g., predicting hospital mortality from doctor quality when sicker patients are admitted to better hospitals). In production, changing X based on a correlated model may not change Y if the relationship is not causal. Causal inference (instrumental variables, randomized experiments, causal graphs) is needed to make reliable interventions.

**Q100: How would you explain overfitting to a non-technical stakeholder?**
Imagine you're studying for an exam by memorizing every question from last year's exams, including all typos and quirks. You'd score perfectly on last year's exams but fail a new exam because you memorized the specific questions rather than learning the underlying subject. Overfitting is the same — the model memorizes the training data, including its noise, instead of learning the general pattern. The fix is to teach it from a wider variety of examples (more data), simplify the model, or check its understanding on new examples it has never seen before (validation set).
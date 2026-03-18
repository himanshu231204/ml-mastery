# ML Mastery

A structured, beginner-to-advanced reference repository for Machine Learning engineers.
Every notebook is self-contained — open it, run it top to bottom, and learn.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/ml-mastery/blob/main/01_libraries/numpy.ipynb)

---

## Who is this for?

- ML engineers who keep forgetting library syntax mid-project
- Students learning ML from scratch and wanting one place that covers everything
- Anyone who wants math intuition behind algorithms, not just copy-paste code

---

## Repository Structure

```
ml-mastery/
│
├── 01_libraries/               # Core Python libraries for ML
│   ├── numpy.ipynb             # Arrays, operations, broadcasting, indexing
│   ├── pandas.ipynb            # DataFrames, cleaning, groupby, merging
│   └── matplotlib.ipynb        # Plots, subplots, styling, saving figures
│
├── 02_ml_concepts/             # ML algorithms with math intuition + code
│   ├── linear_regression.ipynb     # OLS, gradient descent, cost function
│   ├── logistic_regression.ipynb   # Sigmoid, log loss, decision boundary
│   ├── decision_trees.ipynb        # Entropy, Gini, information gain
│   ├── random_forest.ipynb         # Bagging, feature importance, OOB error
│   ├── svm.ipynb                   # Hyperplane, margin, kernel trick
│   ├── knn.ipynb                   # Distance metrics, choosing K
│   ├── naive_bayes.ipynb           # Bayes theorem, conditional probability
│   ├── unsupervised.ipynb          # K-Means, DBSCAN, PCA, t-SNE
│   ├── feature_engineering.ipynb   # Encoding, scaling, selection, pipelines
│   └── model_evaluation.ipynb      # Metrics, cross-validation, bias-variance
│
├── 03_projects/                # End-to-end ML projects on real datasets
│   ├── titanic/                # Binary classification — survival prediction
│   └── house_price/            # Regression — price prediction
│
├── extras/                     # Quick reference materials
│   ├── cheatsheet.md           # Most-used commands across all libraries
│   └── interview_qa.md         # Common ML interview questions and answers
│
├── requirements.txt            # All dependencies
├── CONTRIBUTING.md             # How to contribute
└── README.md                   # You are here
```

---

## How to use this repo

**Option 1 — Google Colab (recommended, zero setup)**

Click any "Open in Colab" badge at the top of each notebook. Everything runs in the browser.

**Option 2 — Local setup**

```bash
git clone https://github.com/YOUR_USERNAME/ml-mastery.git
cd ml-mastery
pip install -r requirements.txt
jupyter notebook
```

---

## Learning Path

Follow this order if you are starting from scratch:

```
NumPy → Pandas → Matplotlib
         ↓
Linear Regression → Logistic Regression
         ↓
Decision Trees → Random Forest
         ↓
SVM → KNN → Naive Bayes
         ↓
Feature Engineering → Model Evaluation
         ↓
Unsupervised Learning
         ↓
Projects (Titanic → House Price)
```

Each concept builds on the previous one. Do not skip the libraries section — everything in `02_ml_concepts` uses NumPy and Pandas heavily.

---

## What makes each algorithm notebook different

Every notebook in `02_ml_concepts/` follows this structure:

| Section | What you get |
|---|---|
| Concept overview | Plain English explanation of what the algorithm does |
| Math intuition | The actual math — cost function, derivation, key equations |
| Visual intuition | Plots and diagrams built from scratch to show what is happening |
| Code from scratch | Implement the algorithm using only NumPy |
| Sklearn implementation | The production way — with all parameters explained |
| Common mistakes | What goes wrong and why |
| Exercises | Practice problems with solutions |

---

## Dependencies

| Library | Version | Purpose |
|---|---|---|
| numpy | ≥ 1.24 | Array operations, math |
| pandas | ≥ 2.0 | Data manipulation |
| matplotlib | ≥ 3.7 | Visualization |
| seaborn | ≥ 0.12 | Statistical plots |
| scikit-learn | ≥ 1.3 | ML algorithms |
| scipy | ≥ 1.11 | Scientific computing |

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding notebooks, fixing errors, or improving explanations.

---

## License

MIT License — free to use, share, and modify with attribution.

## 👨‍💻 Author
 
**Himanshu Kumar**
 
- 🌐 GitHub: [@himanshu231204](https://github.com/himanshu231204)
- 💼 LinkedIn: [himanshu231204](https://www.linkedin.com/in/himanshu231204)
- 🐦 Twitter/X: [@himanshu231204](https://twitter.com/himanshu231204)
- 📧 Email: himanshu231204@gmail.com

Thanks for checking out the repo! If you find it useful, please give it a star ⭐ and share it with your friends. Happy learning
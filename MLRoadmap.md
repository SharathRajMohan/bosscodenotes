Machine Learning Interview Preparation Roadmap

Section 1: Foundations & Core Mathematics

Before tackling complex model architectures, you must master the fundamental mathematical concepts and data transformation techniques that form the backbone of machine learning algorithms.

1.1 Probability & Mathematical Statistics

Core Concepts:

Bayes' Theorem & Conditional Probability: Understanding $P(A\vert{}B) = \frac{P(B\vert{}A)P(A)}{P(B)}$ and its application in generative models.

Expectation, Variance & Covariance: Mathematical definitions of expected value $E[X]$, variance $\text{Var}(X) = E[(X - \mu)^2]$, and covariance matrices.

Probability Distributions:

Discrete: Bernoulli, Binomial, Poisson distributions.

Continuous: Gaussian (Normal) distribution, Uniform distribution, Exponential distribution.

Hypothesis Testing:

Null ($H_0$) vs. Alternative ($H_1$) hypotheses.

Type I Error ($\alpha$, False Positive) vs. Type II Error ($\beta$, False Negative).

$p$-values, $t$-tests, $z$-tests, Chi-Square ($\chi^2$) test, and Confidence Intervals.

1.2 Linear Algebra & Vector Calculus

Core Concepts:

Vector & Matrix Operations: Matrix multiplication, transpose, trace, rank, and determinants.

Eigenvalues & Eigenvectors: Characteristic equation $\det(A - \lambda I) = 0$, eigendecomposition, and geometric interpretation.

Singular Value Decomposition (SVD): Factoring matrix $A$ into $U \Sigma V^T$ for dimensionality reduction and latent factor analysis.

Vector Calculus & Gradients:

Directional derivatives and gradient vectors $\nabla f(x)$.

Jacobian matrix (first-order partial derivatives) and Hessian matrix (second-order partial derivatives for convex optimization).

1.3 Data Preprocessing & Feature Engineering

Core Concepts:

Missing Value Imputation: Mean/median/mode substitution, $k$-NN imputation, and iterative multivariate imputation.

Feature Scaling:

Min-Max Normalization: Rescaling features to $[0, 1]$ via $x' = \frac{x - x_{\min}}{x_{\max} - x_{\min}}$.

Standardization ($Z$-Score): Centering data to zero mean and unit variance via $x' = \frac{x - \mu}{\sigma}$.

Categorical Feature Encoding:

One-Hot Encoding: Creating $N$ binary dummy variables (and avoiding the dummy variable trap by dropping one column).

Ordinal/Label Encoding: Mapping ordered categories to integers.

Target (Mean) Encoding: Replacing categories with the mean target value, using smoothing to prevent target leakage:


$$S_i = w_i \cdot \bar{y}_i + (1 - w_i) \cdot \bar{y}_{\text{global}}$$

1.4 Dimensionality Reduction Techniques

Core Concepts:

Principal Component Analysis (PCA): Unsupervised linear dimensionality reduction by maximizing variance along orthogonal principal components (eigenvectors of the sample covariance matrix).

t-SNE & UMAP: Non-linear dimensionality reduction algorithms designed for high-dimensional data visualization by preserving local vs. global manifold structures.

Section 2: Fundamental Classical Algorithms

Understanding the mechanics, loss functions, assumptions, and computational complexity of classical algorithms is essential for passing technical screens.

2.1 Linear & Logistic Regression

Linear Regression:

Model equation: $y = X\beta + \epsilon$.

Closed-form Ordinary Least Squares (OLS) solution: $\hat{\beta} = (X^T X)^{-1} X^T y$.

Key assumptions: Linearity, independence of errors, homoscedasticity (constant variance of errors), and no multicollinearity.

Logistic Regression:

Sigmoid mapping function: $\sigma(z) = \frac{1}{1 + e^{-z}}$.

Binary Cross-Entropy (Log-Loss) objective function:


$$\mathcal{L}(\beta) = -\frac{1}{N} \sum_{i=1}^{N} \left[ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right]$$

Parameter estimation via Gradient Descent or Newton-Raphson optimization.

2.2 Distance-Based Models

$k$-Nearest Neighbors ($k$-NN):

Non-parametric instance-based learning.

Distance metrics: Euclidean ($L_2$ norm), Manhattan ($L_1$ norm), Minkowski distance, and Cosine similarity.

Impact of feature scaling and choice of hyperparameter $k$.

$k$-Means Clustering:

Unsupervised iterative partitioning algorithm minimizing Within-Cluster Sum of Squares (WCSS).

Initialization sensitivity ($k$-means++ initialization) and selecting $k$ via Elbow Method or Silhouette Score.

Support Vector Machines (SVM):

Max-margin hyperplanes minimizing $\Vert{}w\Vert{}^2$ subject to functional margin constraints.

Soft-margin formulation introducing slack variables $\xi_i$ controlled by penalty hyperparameter $C$.

Kernel Trick: Implicit mapping to higher-dimensional feature spaces via Kernel functions (RBF/Gaussian kernel $K(x, x') = \exp(-\gamma \Vert{}x - x'\Vert{}^2)$).

2.3 Naive Bayes Classifiers

Core Mechanics:

Applies Bayes' Theorem assuming conditional independence between features given the class label.

Classification decision rule: $\hat{y} = \arg\max_c P(Y=c) \prod_{j=1}^{D} P(X_j \vert{} Y=c)$.

Laplace (Additive) Smoothing: Handling zero-frequency token probabilities during inference.

2.4 Decision Trees & Splitting Mechanics

Core Mechanics:

Non-parametric hierarchical tree structure constructed via recursive binary splitting.

Splitting Criteria:

Gini Impurity (Classification): $\text{Gini}(D) = 1 - \sum_{i=1}^{C} p_i^2$.

Entropy & Information Gain (Classification): $\text{Entropy}(D) = -\sum_{i=1}^{C} p_i \log_2(p_i)$.

Variance Reduction (Regression): Minimizing MSE of target variables in split nodes.

2.5 Algorithm Comparison & Complexity Matrix

Algorithm

Training Time Complexity

Inference Time Complexity

Main Hyperparameters

Primary Strengths

Linear / Logistic Regression

$O(N \cdot D^2 + D^3)$

$O(D)$

Regularization parameter ($\lambda$ / $C$)

Fast, highly interpretable

$k$-Nearest Neighbors

$O(1)$ (Lazy learner)

$O(N \cdot D)$

$k$, Distance Metric

No training phase required

Support Vector Machines

$O(N^2 \cdot D)$ to $O(N^3)$

$O(N_{\text{support}} \cdot D)$

$C$, Kernel, $\gamma$

Robust in high-dimensional spaces

Decision Trees

$O(D \cdot N \log N)$

$O(\text{Depth})$

max_depth, min_samples_split

Handles non-linear data natively

Section 3: Regularization & Model Generalization

Preventing overfitting and ensuring generalization to unseen data is a major focus area in technical machine learning interviews.

3.1 The Bias-Variance Trade-off

Expected Generalization Error Decomposition:


$$\text{Expected Error} = \text{Bias}^2 + \text{Variance} + \text{Irreducible Error}$$

High Bias (Underfitting): The model is too simple to capture underlying patterns. High error on both training and test sets.

High Variance (Overfitting): The model memorizes training noise and fails to generalize. Low training error, high test error.

3.2 Mathematical Formulation of Regularization

Regularization adds a penalty term $\Omega(w)$ to the loss function $\mathcal{L}(w)$ to constrain model weights:


$$\mathcal{L}_{\text{reg}}(w) = \mathcal{L}(w) + \lambda \Omega(w)$$

$L_1$ Regularization (Lasso Regression):

Penalty term: $\Omega(w) = \Vert{}w\Vert{}_1 = \sum_{j=1}^{D} \vert{}w_j\vert{}$.

Geometric effect: Creates a diamond-shaped constraint region with sharp corners at coordinate axes, forcing non-essential weights to exactly zero (sparse feature selection).

$L_2$ Regularization (Ridge Regression):

Penalty term: $\Omega(w) = \frac{1}{2} \Vert{}w\Vert{}_2^2 = \frac{1}{2} \sum_{j=1}^{D} w_j^2$.

Geometric effect: Creates a circular constraint region, shrinking weights smoothly toward zero without forcing them to zero.

ElasticNet Regularization:

Combines $L_1$ and $L_2$ penalties with mixing parameter $\alpha \in [0, 1]$:


$$\Omega(w) = \alpha \Vert{}w\Vert{}_1 + \frac{1 - \alpha}{2} \Vert{}w\Vert{}_2^2$$

3.3 Cross-Validation & Data Leakage Prevention

Validation Schemes:

$k$-Fold Cross-Validation: Splitting training data into $k$ disjoint subsets to rotate validation folds.

Stratified $k$-Fold: Preserving class label proportions across every fold (critical for imbalanced classification).

Time-Series Split: Using expanding/sliding temporal windows to prevent future data from leaking into past predictions.

Data Leakage Mitigation:

Always fit scalers, encoders, and feature selectors only on the training fold, then transform the validation fold.

Section 4: Advanced Ensemble Methods

Ensemble techniques combine multiple base estimators ("weak learners") to create a robust model with lower error.

4.1 Bagging Principles & Random Forests

Bootstrap Aggregating (Bagging):

Trains multiple base models independently in parallel on bootstrap samples (random sampling with replacement).

Reduces variance without increasing bias.

Random Forest Algorithm:

Extends bagging by adding Feature Subspace Sampling (selecting a random subset of $\sqrt{D}$ features at each node split) to decorrelate individual decision trees.

Out-of-Bag (OOB) Error: Using unsampled instances ($\approx 36.8\%$ of data per tree) as a built-in validation set.

4.2 Sequential Boosting Mechanics

Boosting builds sequential models where each new model is trained to correct errors made by previous models, primarily reducing bias.

AdaBoost (Adaptive Boosting):

Iteratively re-weights training samples, assigning higher weights to instances misclassified by the previous weak learner.

Combines weak learners via weighted majority voting based on each learner's error rate $\epsilon_m$.

Gradient Boosting Machines (GBM):

Sequential trees are fitted directly to the pseudo-residuals (the negative gradient of the loss function $\mathcal{L}(y, f(x))$) of the ensemble's current prediction:


$$r_{im} = -\left[ \frac{\partial \mathcal{L}(y_i, f(x_i))}{\partial f(x_i)} \right]_{f(x) = f_{m-1}(x)}$$

4.3 Modern Gradient Boosted Decision Trees (GBDT)

Interviewers frequently compare modern GBDT implementations:

XGBoost (Extreme Gradient Boosting):

Uses a second-order Taylor expansion approximation of the loss function (utilizing both gradients $g_i$ and Hessians $h_i$).

Built-in $L_1$ and $L_2$ regularization on tree leaf weights ($\gamma T + \frac{1}{2} \lambda \sum w_j^2$).

Supports parallelized tree node splitting and exact/approximate greedy quantile algorithms.

LightGBM:

Uses Leaf-Wise (Best-First) tree growth instead of Depth-Wise growth, resulting in faster convergence and lower loss.

Uses Histogram-Based Feature Binning to convert continuous features into discrete bins, drastically reducing compute complexity.

Applies Gradient-based One-Side Sampling (GOSS) to keep instances with large gradients and sample instances with small gradients.

CatBoost:

Native handling of categorical features using Ordered Target Statistics to prevent target leakage.

Uses Symmetric (Oblivious) Trees where the same split condition is applied across an entire tree level, optimizing GPU execution speed.

4.4 Meta-Learning Architectures

Stacking (Stacked Generalization): Trains heterogeneous base estimators (e.g., XGBoost, SVM, Neural Net) and uses their out-of-fold predictions as features to train a second-stage meta-learner (e.g., Logistic Regression).

Blending: Similar to stacking, but uses a single held-out validation set instead of out-of-fold cross-validation predictions to train the meta-learner.

Section 5: Evaluation Metrics & Diagnostic Debugging

Choosing the correct evaluation metric depends on business requirements, cost asymmetries, and dataset balance.

5.1 Classification Metrics & Trade-offs

Confusion Matrix Components: True Positive (TP), False Positive (FP), True Negative (TN), False Negative (FN).

Core Metrics:

Precision: $\frac{\text{TP}}{\text{TP} + \text{FP}}$ (Focuses on minimizing False Positives, e.g., spam detection).

Recall (Sensitivity): $\frac{\text{TP}}{\text{TP} + \text{FN}}$ (Focuses on minimizing False Negatives, e.g., cancer diagnosis).

$F_1$-Score: Harmonic mean balancing precision and recall:


$$F_1 = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$$

Diagnostic Curves:

ROC-AUC: Plots True Positive Rate vs. False Positive Rate across decision thresholds. Measure of class separation probability.

PR-AUC: Plots Precision vs. Recall. Superior metric for highly skewed/imbalanced datasets where TNs dominate.

5.2 Regression Performance Metrics

Mean Squared Error (MSE): $\frac{1}{N} \sum (y_i - \hat{y}_i)^2$ (Heavily penalizes large outliers).

Root Mean Squared Error (RMSE): $\sqrt{\text{MSE}}$ (Restores error units to the scale of the target variable).

Mean Absolute Error (MAE): $\frac{1}{N} \sum \vert{}y_i - \hat{y}_i\vert{}$ (Robust to extreme outliers).

Coefficient of Determination ($R^2$): Proportion of target variance explained by the model:


$$R^2 = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}$$

5.3 Imbalanced Data Strategies

Resampling Techniques: Random Oversampling, SMOTE (Synthetic Minority Over-sampling Technique via $k$-NN interpolation), Random Undersampling.

Cost-Sensitive Learning: Adjusting loss function class weights (e.g., scale_pos_weight in XGBoost).

Decision Threshold Tuning: Moving prediction probability cutoffs away from $0.5$ based on precision-recall cost-benefit matrices.

Section 6: Deep Learning & Neural Network Regularization

For roles with deep learning requirements, focus on neural network optimization mechanics and stabilization techniques.

6.1 Neural Network Mechanics & Activation Functions

Backpropagation: Computing gradients of the loss function with respect to weights using the Multivariate Chain Rule.

Activation Functions:

Sigmoid: $\sigma(z) = \frac{1}{1 + e^{-z}}$ (Sustains vanishing gradient issues at saturation limits).

ReLU (Rectified Linear Unit): $f(z) = \max(0, z)$ (Solves vanishing gradient for positive inputs, but subject to "Dying ReLU").

GELU (Gaussian Error Linear Unit): Smooth, non-monotonic approximation used in modern Transformer architectures.

6.2 Optimization Algorithms

Stochastic Gradient Descent (SGD): Weight updating via mini-batches: $w_{t+1} = w_t - \eta \nabla \mathcal{L}(w_t)$.

Momentum: Accelerates updates along directional vectors using exponential moving averages of past gradients.

Adam (Adaptive Moment Estimation): Combines Momentum (first moment $m_t$) and RMSprop (second raw moment $v_t$).

AdamW: Decouples weight decay regularization from gradient updates, resolving Adam's weight decay decay error.

6.3 Neural Network Regularization & Stability Techniques

Dropout: Randomly deactivates a fraction $p$ of hidden neurons during training forward passes to prevent co-adaptation.

Batch Normalization: Normalizes layer inputs across mini-batches to zero mean and unit variance, stabilizing internal activations.

Layer Normalization: Normalizes activations across features per individual sample (essential for sequence/Transformer models).

Early Stopping: Halts network training when validation loss stops improving over a predefined epoch patience window.

6.4 Sequence & Attention Architectures

Transformers & Self-Attention: Computes scaled dot-product attention mapping Queries ($Q$), Keys ($K$), and Values ($V$):


$$\text{Attention}(Q, K, V) = \text{softmax}\left( \frac{Q K^T}{\sqrt{d_k}} \right) V$$

Section 7: Hands-on Coding & ML System Design

Interview preparation requires both algorithmic coding from scratch and high-level system design capabilities.

7.1 NumPy Algorithmic Implementations (From Scratch)

Practice writing basic ML algorithms in pure Python and NumPy to prepare for live coding rounds.

import numpy as np

def logistic_regression_fit(X: np.ndarray, y: np.ndarray, lr: float = 0.01, epochs: int = 1000) -> np.ndarray:
    """Trains a Logistic Regression model using Gradient Descent."""
    num_samples, num_features = X.shape
    weights = np.zeros(num_features)
    bias = 0.0
    
    for _ in range(epochs):
        # Linear combination and sigmoid activation
        linear_model = np.dot(X, weights) + bias
        y_predicted = 1 / (1 + np.exp(-linear_model))
        
        # Compute gradients
        dw = (1 / num_samples) * np.dot(X.T, (y_predicted - y))
        db = (1 / num_samples) * np.sum(y_predicted - y)
        
        # Update parameters
        weights -= lr * dw
        bias -= lr * db
        
    return weights


7.2 ML System Design Framework

When asked to design a real-world machine learning system (e.g., fraud detection, recommendation system, or search ranking), structure your response using these 5 phases:

Problem Framing & Scope Definition:

Clarify business goals, online KPIs (e.g., CTR, conversion rate), and offline evaluation metrics (e.g., ROC-AUC, $F_1$).

Identify constraints: Inference latency budget (P95/P99 < 50ms), throughput (QPS), hardware constraints.

Data Pipeline & Feature Engineering:

Define static features (user demographics), dynamic real-time features (recent clicks), and contextual features.

Plan feature storage: Offline Feature Store (Batch/S3/BigQuery) vs. Online Feature Store (Low-latency Redis/DynamoDB).

Model Selection & Training:

Propose a simple baseline model (e.g., Logistic Regression) before moving to complex models (e.g., Two-Tower Neural Nets, GBDT).

Plan training strategy: Batch offline training vs. continuous online model updates.

Inference & Serving Architecture:

Evaluate deployment patterns: Real-time synchronous API vs. Asynchronous batch inference vs. On-device edge deployment.

Model optimization techniques: Quantization (FP16/INT8), Pruning, and TensorRT/ONNX compilation.

Monitoring & Operational Maintenance:

Track Data Drift (Feature distribution shift using Population Stability Index) and Concept Drift (P(Y|X) changes).

Set up automated model re-training triggers and fallback strategies (e.g., reverting to rule-based baselines).
# Weekly Mathematics and AI

**William Zhou · Mathematical derivations and NumPy experiments**

It's my study archive for number theory, probability, statistics, and machine learning. Each weekly set contains seven problems: two in number theory, one in probability, two in statistics, and two in AI. The computational exercises connect model assumptions and mathematical analysis with parameter estimation, optimization, and evaluation.

## Table of Contents

|  | Questions | Implementation |
| --- | --- | --- |
| **Optimization** | [November 2, Problem 7](11-02-26.pdf): regularized logistic regression, gradient and Hessian derivations, existence of a minimizer, and a Lipschitz bound | [Notebook](11-02-26.ipynb): `loss_grad`, `grad_des`, and `Sgrad_des`; finite-difference and extreme-score checks |
| **Probability calibration** | [November 9, Problems 6–7](11-09-26.pdf): Gaussian classification with unequal covariances and confidence scaling | [Notebook](11-09-26.ipynb): `fit_gaussian`, `gaussian_score`, `scale_loss_grad`, `fit_scale`, and `calibration_bins` |

## The Latest Experiment

**November 16, 2026 · How closely do Gaussian discriminant analysis and Softmax regression agree?**

I generated three Gaussian classes with a shared covariance matrix. Under this assumption, both models can represent the true class probabilities. I fit both models on the same 300 training cases, using the training means and standard deviations to scale every split. For Softmax, I ran 600 full-gradient updates at each of three penalties (0.001, 0.01, 0.1). The lowest mean log loss on 180 validation cases selected λ = 0.001. I then froze both fits and evaluated them on the same 2,000 fresh test cases.

| Model | Test error | Mean test log loss |
| --- | ---: | ---: |
| Gaussian discriminant analysis (GDA) | 22.30% | 0.538219 |
| Softmax regression (λ = 0.001) | 22.80% | 0.541029 |

Only GDA was wrong on 8 cases, and only Softmax was wrong on 18. GDA made 10 fewer errors overall, a **0.50 percentage-point** reduction. That falls below my practical threshold of **2 percentage points**.

The selected Softmax fit had a final training gradient norm of 2.29 × 10⁻¹⁰. On the independent test set, the 95% Hoeffding interval for its error rate was **19.76%–25.84%**, using a radius of √(ln(40) / (2 × 2,000)). Both fitted models can make errors even with accurate parameter estimates because the Gaussian classes overlap.

[November 16 notebook](11-16-26.ipynb) · [Worksheet, Problems 5–7](11-16-26.pdf)

## Weekly index

| Edition | Mathematical topics | Computational topics | Files |
| --- | --- | --- | --- |
| November 2, 2026 | Finite Euler-factor removal; weighted divisibility probabilities; binomial factorial moments; unbiased estimation versus maximum likelihood; Wilson intervals | Shared-covariance Gaussian discriminant analysis; regularized logistic regression; full-batch GD and mini-batch SGD | [PDF](11-02-26.pdf) · [Notebook](11-02-26.ipynb) |
| November 9, 2026 | Gcd averages and convolution; proper scoring rules; beta–Bernoulli prediction; exact paired comparisons of classifier errors | Class-specific covariance estimation and pooling; confidence scaling by convex one-dimensional optimization; calibration-bin summaries | [PDF](11-09-26.pdf) · [Notebook](11-09-26.ipynb) |

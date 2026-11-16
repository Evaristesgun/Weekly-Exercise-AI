# Weekly Mathematics and AI

**William Zhou · Mathematical derivations and NumPy experiments**

It's my study archive for number theory, probability, statistics, and machine learning. Each weekly set contains seven problems: two in number theory, one in probability, two in statistics, and two in AI. The computational exercises connect model assumptions and mathematical analysis with parameter estimation, optimization, and evaluation.

## Table of Contents

| Interest | Suggested reading | Companion implementation |
| --- | --- | --- |
| **Optimization** | [November 2, Problem 7](11-02-26.pdf): regularized logistic regression, gradient and Hessian derivations, existence of a minimizer, and a Lipschitz bound | [Notebook](11-02-26.ipynb): `loss_grad`, `grad_des`, and `Sgrad_des`; finite-difference and extreme-score checks |
| **Probability calibration** | [November 9, Problems 6–7](11-09-26.pdf): Gaussian classification with unequal covariances and confidence scaling | [Notebook](11-09-26.ipynb): `fit_gaussian`, `gaussian_score`, `scale_loss_grad`, `fit_scale`, and `calibration_bins` |
| **Number theory** | [November 2, Problems 1–2](11-02-26.pdf): removing Euler factors and weighted local densities; [November 9, Problems 1–2](11-09-26.pdf): gcd sums and Dirichlet convolution | Written calculations in the PDFs |

For a quick computational example, start with the **November 9 notebook** and the result below. For the mathematical arguments, follow the matching problem numbers in the PDFs.

## One experiment at a glance

**Can confidence change without changing the predicted class?**

The November 9 experiment fits a Gaussian classifier to synthetic two-dimensional data, chooses covariance pooling on a validation split, and then fits a positive scalar to its log-odds on a separate calibration split. Positive scaling preserves the decision boundary while changing predicted probabilities.

The notebook's saved outputs on 2,000 test observations are:

| Model | Classification error | Mean log loss | Brier loss |
| --- | ---: | ---: | ---: |
| Fully pooled covariance baseline | 0.1995 | 0.423790 | 0.136393 |
| Validation-selected covariance pooling | 0.1960 | 0.368349 | 0.123577 |
| Selected model after confidence scaling | 0.1960 | 0.369101 | 0.123000 |

Here, scaling leaves classification error unchanged, slightly improves Brier loss, and slightly worsens test log loss. Minimizing calibration-sample log loss does not guarantee an improvement on a separate test sample. These are results from one synthetic experiment, not evidence of a universal model ranking.

## Weekly index

| Edition | Mathematical topics | Computational topics | Files |
| --- | --- | --- | --- |
| November 2, 2026 | Finite Euler-factor removal; weighted divisibility probabilities; binomial factorial moments; unbiased estimation versus maximum likelihood; Wilson intervals | Shared-covariance Gaussian discriminant analysis; regularized logistic regression; full-batch GD and mini-batch SGD | [PDF](11-02-26.pdf) · [Notebook](11-02-26.ipynb) |
| November 9, 2026 | Gcd averages and convolution; proper scoring rules; beta–Bernoulli prediction; exact paired comparisons of classifier errors | Class-specific covariance estimation and pooling; confidence scaling by convex one-dimensional optimization; calibration-bin summaries | [PDF](11-09-26.pdf) · [Notebook](11-09-26.ipynb) |

## Reading the materials

- **PDFs:** exercise statements, written working, source notes, and separate solutions/checks sections. Read these sections distinctly; the complete PDFs should not be interpreted as independently authored research papers.
- **Notebooks:** implementations and saved numerical outputs for the AI exercises, principally Problems 6 and 7. They are working study notebooks, not a complete implementation of every worksheet subquestion.
- **Sources:** the PDFs identify the references and adaptations used in each exercise, including material from Stanford CS229 and MIT probability, statistics, and number theory courses. Consult each problem's “Source and use” note for attribution.

## Running the notebooks

The code uses **Python 3 and NumPy**. Install Jupyter to run it interactively:

```bash
python -m pip install numpy jupyterlab
jupyter lab
```

Open either `.ipynb` file, restart the kernel, and run the cells from top to bottom. The synthetic datasets are generated in the notebooks; no external dataset is required. Data-generation seeds are specified in the code.

### Current implementation notes

The notebooks are still being revised. In the November 2 notebook, the GDA selection cell currently fits on validation data, and `fit_gda` adds its diagonal regularizer before dividing by the sample count. The SGD sampler is not seeded, and the final evaluation cell uses manually specified parameter vectors. Consequently, those saved comparisons should not be read as a fully reproduced execution of the PDF's intended protocol. The November 9 notebook includes calibration-bin summaries, but the paired-error test requested in the worksheet is not yet implemented there.

The result table above summarizes saved November 9 outputs; it is not a claim that every exercise or implementation has been independently verified.

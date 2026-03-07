<img width="1536" height="1024" alt="Simulation of Statistical Models Using R" src="https://github.com/user-attachments/assets/cae28e2b-1584-42a1-8068-27da592a073b" />


Simulation of Statistical Models Using R: Covers fixed and mixed effect models including t-test, ANOVA, regression, ANCOVA, factorial ANOVA, random intercept and slope models, correlated and uncorrelated mixed models, and nested ANOVA. Demonstrates model behavior and inference through simulation in R.

This repository presents a comprehensive and practical guide to Simulation of Statistical Models Using R, focusing on both fixed effect and mixed effect modeling frameworks. The primary objective of this project is to demonstrate how statistical models can be generated, analyzed, and validated through simulation techniques in R.

Simulation plays a central role in modern statistics and data science. By generating synthetic datasets under controlled assumptions, we can evaluate model behavior, test statistical properties, understand bias and variance, and compare modeling approaches. This repository emphasizes conceptual clarity, reproducibility, and hands-on implementation.

The project systematically progresses from foundational fixed effect models to more advanced mixed effect and hierarchical structures, providing both theoretical explanation and R-based simulation workflows.


#### 1. Introduction

* Overview of statistical simulation
* Importance of simulation in hypothesis testing and model validation
* Monte Carlo framework in R
* Understanding sampling variability and inference through simulation

#### 2. Fixed Effect Models

This section focuses on classical parametric models where effects are assumed to be constant across observations.

* Simple t-test
    * Simulating two-group comparisons
    * Type I and Type II error evaluation
    * Power analysis through repeated sampling

* One-way ANOVA
    * Simulating multiple group means
    * Variance decomposition
    * F-statistic behavior under null and alternative hypotheses

* Linear Regression
    * Simulating predictor–response relationships
    * Estimator bias, variance, and confidence intervals
    * Residual diagnostics and model assumptions

* ANCOVA (Analysis of Covariance)
    * Controlling for continuous covariates
    * Comparison of adjusted group means
    * ANCOVA without interaction
          * Parallel slope assumption
          * Interpretation of adjusted effects
    * ANCOVA with interaction
          * Testing slope heterogeneity
          * Model comparison and interpretation

* Factorial ANOVA
    * Simulating multi-factor experimental designs
    * Main effects and interaction effects
    * Factorial ANOVA without interaction
        * Additive model structure
        * Interpretation of independent factor effects
    * Factorial ANOVA with interaction
        * Interaction visualization
        * Effect interpretation under dependency

#### 3. Mixed Effect Models
This section extends simulations to hierarchical and multilevel modeling, where variability exists at multiple levels.
* Random Effect ANCOVA
     * Modeling group-level variability
     * Understanding random intercepts and slopes
     * Random effect on Intercept
        * Group-level baseline variation
     * Random effect on Slope
        * Variation in covariate effects across groups
     * Random effect on Intercept and Slope (with correlation)
         * Correlated random components
         * Realistic hierarchical modeling structure
     * Random effect on Intercept and Slope (no correlation)
         * Independent random components
         * Model comparison and variance structure

* Nested ANOVA
    * Hierarchical experimental designs
    * Partitioning variance across nested levels
    * Simulation of cluster-based sampling

#### Features of This Repository
✔ Step-by-step simulation workflows in R

✔ Clear model formulation and interpretation

✔ Monte Carlo validation of statistical properties

✔ Reproducible code with detailed comments

✔ Suitable for students, researchers, and instructors

✔ Bridges theory with computational practice


### Tools & Libraries
The simulations primarily use R along with common statistical libraries such as:
* stats
* car
* lme4
* nlme
* ggplot2

### Learning Outcomes
By working through this repository, you will be able to:
* Generate simulated datasets under controlled assumptions
* Understand sampling distributions empirically
* Evaluate estimator performance using repeated simulation
* Compare fixed and mixed effect modeling frameworks
* Interpret interaction effects correctly
* Apply hierarchical modeling concepts using R

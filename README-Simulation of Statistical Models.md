# 📘 Simulation of Statistical Models

> **Author:** Ms. Mrunalini (Data Science Trainer)
> 📧 mrunalini0107@gmail.com | 📍 Mumbai – 400095

---

## 📋 Table of Contents

1. [Introduction](#introduction)
2. [Fixed Effect Models](#fixed-effect-models)
   - [Simple t-test](#simple-t-test)
   - [One-Way ANOVA](#one-way-anova)
   - [Linear Regression](#linear-regression)
   - [ANCOVA (Analysis of Covariance)](#ancova-analysis-of-covariance)
     - [ANCOVA Without Interaction](#ancova-without-interaction)
     - [ANCOVA With Interaction](#ancova-with-interaction)
   - [Factorial ANOVA](#factorial-anova)
     - [Factorial ANOVA Without Interaction](#factorial-anova-without-interaction)
     - [Factorial ANOVA With Interaction](#factorial-anova-with-interaction)
3. [Mixed Effect Models](#mixed-effect-models)
   - [Random Effect ANCOVA](#random-effect-ancova)
     - [Random Effect on Intercept](#random-effect-on-intercept)
     - [Random Effect on Slope](#random-effect-on-slope)
     - [Random Effect on Intercept and Slope (with Correlation)](#random-effect-on-intercept-and-slope-with-correlation)
     - [Random Effect on Intercept and Slope (no Correlation)](#random-effect-on-intercept-and-slope-no-correlation)
   - [Nested ANOVA](#nested-anova)
4. [Learning Objectives](#learning-objectives)
5. [Project Structure](#project-structure)
6. [Requirements](#requirements)
7. [How to Run](#how-to-run)
8. [Conclusion](#conclusion)

---

## Introduction

This project is a comprehensive, hands-on series of R-based simulation notebooks designed to build deep intuition for statistical modelling through data simulation. Rather than simply fitting models to existing datasets, each notebook teaches how to **generate synthetic data** that conform to a known underlying structure — and then **verify** that the fitted model recovers that structure.

This "simulation-first" approach is invaluable for understanding the mathematical assumptions behind each model class, diagnosing model behaviour, evaluating statistical power, and developing the confidence to apply these models to real-world research data.

The series covers two fundamental families of statistical models:

- **Fixed Effect Models** — where all factors and predictors have specific, repeatable levels of interest (gender, treatment group, dose concentration, etc.)
- **Mixed Effect Models** — where at least one factor represents a random sample from a larger population of levels (subjects, schools, classes), introducing hierarchical or multilevel structure.

All simulations are implemented in **R** using a step-by-step pedagogical style, with mathematical model equations, diagnostic plots, and interpretive commentary throughout.

---

## Fixed Effect Models

### Simple t-test

**Notebook:** `R01_Simulation_of_Statistical_Models_-_Fixed_Effect_Models.ipynb`

**Description:**
The simplest fixed effect model is the two-sample t-test, treated here as a one-way ANOVA with two factor levels. The simulation creates a two-level factor (e.g., Male vs. Female) with 15 replications per group. Expected means are assigned to each group, and random Gaussian noise is added to simulate realistic variability. A linear model (`lm()`) is fitted and ANOVA results are compared against the known simulation parameters.

**Model equation:**
$$Y_{ij} = \mu + \tau_i + \varepsilon_{ij}, \quad \varepsilon_{ij} \sim N(0, \sigma^2)$$

---

### One-Way ANOVA

**Notebook:** `R02_Simulation_of_Statistical_Models_-_One_Way_ANOVA.ipynb`

**Description:**
Extends the t-test to four treatment groups (Treat1–Treat4), each with five replications. The simulation assigns distinct expected means to each group and introduces controlled error variance. Box plots and ANOVA tables allow direct comparison between the simulated truth and estimated model parameters. Post-hoc comparisons can be explored to understand pairwise treatment differences.

**Model equation:**
$$Y_{ij} = \mu + \tau_i + \varepsilon_{ij}$$

where $\tau_i$ is the treatment effect for group $i$.

---

### Linear Regression

**Notebook:** `R03_Simulation_of_Statistical_Models_-_Linear_Regression.ipynb`

**Description:**
Introduces continuous predictors (covariates) through two simulation scenarios: (1) randomly generated cadmium (Cd) concentrations drawn from a uniform distribution, and (2) controlled, fixed laboratory concentrations replicated across levels. Both cases simulate a known slope and intercept, add Gaussian noise, then recover these parameters with `lm()`. Scatter plots with fitted regression lines illustrate how noise level affects parameter recovery.

**Model equation:**
$$Y_i = \beta_0 + \beta_1 X_i + \varepsilon_i, \quad \varepsilon_i \sim N(0, \sigma^2)$$

---

### ANCOVA (Analysis of Covariance)

**Notebook:** `R04_Simulation_of_Statistical_Models_-__ANCOVA__Analysis_of_Covariance_.ipynb`

**Description:**
ANCOVA combines a categorical factor (treatment group) and a continuous covariate (Cd concentration) in a single model. Two sub-scenarios are simulated:

#### ANCOVA Without Interaction
Factor levels shift the intercept but share a common slope. This produces parallel regression lines per group — the covariate effect is the same regardless of treatment.

**Model equation:**
$$Y = \alpha_i + \beta X + \varepsilon$$

#### ANCOVA With Interaction
Both the intercept and slope differ by treatment group, producing non-parallel (crossing or diverging) regression lines. This captures the situation where the effect of the covariate depends on which treatment group is observed.

**Model equation:**
$$Y = \alpha_i + \beta_i X + \varepsilon$$

---

### Factorial ANOVA

**Notebook:** `R05_Simulation_of_Statistical_Models_-_Factorial_ANOVA.ipynb`

**Description:**
Factorial ANOVA examines the joint effects of two categorical factors (Fact1: 2 levels; Fact2: 3 levels) in a balanced 2×3 design with 6 replications per cell.

#### Factorial ANOVA Without Interaction
Factor effects are purely additive. The effect of Fact1 is the same at every level of Fact2 and vice versa. Simulated cell means are constructed by summing separate factor contributions.

**Model equation:**
$$Y_{ijk} = \mu + \alpha_i + \beta_j + \varepsilon_{ijk}$$

#### Factorial ANOVA With Interaction
Certain factor-level combinations produce responses that deviate from pure additivity. Interaction terms are explicitly added to the simulation, and interaction plots reveal the crossing or fan-shaped patterns characteristic of true interactions.

**Model equation:**
$$Y_{ijk} = \mu + \alpha_i + \beta_j + (\alpha\beta)_{ij} + \varepsilon_{ijk}$$

---

## Mixed Effect Models

### Random Effect ANCOVA

**Notebook:** `R06_Simulation_of_Statistical_Models_-_Mixed_Effect_Models.ipynb`

**Description:**
This notebook introduces the mixed effects framework using a repeated-measures ANCOVA design. Twenty subjects (10 Male, 10 Female) each receive 6 Epo dosage levels (0–5), yielding 120 total observations. Fixed effects include Gender, Epo dose, and their interaction. Random effects capture subject-to-subject variability. Models are fitted using `lme4::lmer()`.

**Mixed model equation:**
$$Y_{ij} = (\beta_0 + u_{0j}) + (\beta_1 + u_{1j})\,\text{Epo} + \varepsilon_{ij}$$

#### Random Effect on Intercept
Each subject has their own baseline response drawn from $N(0, \sigma^2_u)$, but the slope (Epo effect) is the same for all subjects.

#### Random Effect on Slope
The Epo dose response varies across subjects; each individual has their own slope but a shared intercept.

#### Random Effect on Intercept and Slope (with Correlation)
Both intercept and slope vary by subject, and these random effects are allowed to correlate — capturing the realistic scenario where subjects with higher baselines also tend to respond more strongly.

#### Random Effect on Intercept and Slope (no Correlation)
Both intercept and slope vary by subject, but their random effects are assumed independent (zero correlation), providing a more parsimonious model.

---

### Nested ANOVA

**Notebook:** `R07_Simulation_of_Statistical_Models_-_Nested_ANOVA.ipynb`

**Description:**
Nested ANOVA models true hierarchical data structures where lower-level units are clustered within higher-level units. The study design simulates:

- **7 Schools**, each containing **5 Classes**, each containing **15 Boys + 15 Girls**
- Total: 1,050 student grade observations
- Hierarchical structure: Students ⊂ Classes ⊂ Schools

The simulation progresses through four layers of complexity: (1) sex effect only (equivalent to a t-test), (2) school-level random effects added, (3) class-within-school random effects added, and (4) the full three-level nested model. Each layer illustrates how ignoring hierarchical structure inflates Type I error rates, and how nested random effects correctly partition variance across levels.

---

## Learning Objectives

By working through this series of notebooks, learners will be able to:

- **Understand model structure** by building datasets from scratch using known parameters, building true intuition for what each term in a statistical equation represents.
- **Simulate data for fixed effect models** including t-tests, one-way ANOVA, linear regression, ANCOVA, and factorial ANOVA, with and without interaction terms.
- **Simulate data for mixed effect models** with random intercepts, random slopes, correlated random effects, and nested random effects using `lme4` syntax.
- **Recover simulation parameters** by fitting appropriate models and verifying that estimated coefficients match the known simulation inputs.
- **Interpret ANOVA tables and model summaries** in the context of both fixed and random effects, including understanding variance components.
- **Visualize model structure** using box plots, scatter plots with fitted lines, interaction plots, and caterpillar plots for random effects.
- **Distinguish between fixed and random factors** and understand when each modelling approach is appropriate for a given research design.
- **Handle hierarchical data structures** and appreciate how ignoring clustering inflates false positive rates, motivating the use of mixed models in practice.
- **Apply R programming skills** including use of `gl()`, `rnorm()`, `rep()`, `lm()`, `aov()`, `lmer()`, `ggplot2`, and `lattice` for statistical simulation and analysis.

---

## Project Structure

```
Simulation-of-Statistical-Models/
│
├── R01_Simulation_of_Statistical_Models_-_Fixed_Effect_Models.ipynb
│       └── Simple t-test (two-level factor)
│
├── R02_Simulation_of_Statistical_Models_-_One_Way_ANOVA.ipynb
│       └── One-Way ANOVA (four treatment groups)
│
├── R03_Simulation_of_Statistical_Models_-_Linear_Regression.ipynb
│       └── Simple Linear Regression (random & controlled covariates)
│
├── R04_Simulation_of_Statistical_Models_-__ANCOVA__Analysis_of_Covariance_.ipynb
│       └── ANCOVA with and without interaction
│
├── R05_Simulation_of_Statistical_Models_-_Factorial_ANOVA.ipynb
│       └── Two-Way Factorial ANOVA with and without interaction
│
├── R06_Simulation_of_Statistical_Models_-_Mixed_Effect_Models.ipynb
│       └── Random-effect ANCOVA (intercept, slope, correlated, uncorrelated)
│
├── R07_Simulation_of_Statistical_Models_-_Nested_ANOVA.ipynb
│       └── Nested ANOVA (Students ⊂ Classes ⊂ Schools)
│
└── README.md
```

---

## Requirements

These notebooks use an **R kernel** in Jupyter. The following R packages are required:

| Package | Purpose |
|---|---|
| `lme4` | Mixed effect model fitting (`lmer`) |
| `lmerTest` | p-values for mixed model coefficients |
| `lattice` | Dot plots, trellis graphics for random effects |
| `ggplot2` | Data visualisation |
| `base R` | `lm()`, `aov()`, `gl()`, `rnorm()`, `rep()`, `set.seed()` |

### Installation

```r
install.packages(c("lme4", "lmerTest", "lattice", "ggplot2"))
```

### Jupyter R Kernel Setup

```bash
# Install IRkernel for Jupyter
install.packages("IRkernel")
IRkernel::installspec(user = TRUE)
```

---

## How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/simulation-of-statistical-models.git
   cd simulation-of-statistical-models
   ```

2. **Launch Jupyter Notebook:**
   ```bash
   jupyter notebook
   ```

3. **Open notebooks in order** — each notebook is self-contained but the series builds conceptually from R01 through R07.

4. **Run all cells** in each notebook sequentially. Each notebook begins by defining the study design, assigns expected values, simulates response data with noise, fits the appropriate model, and interprets results.

> 💡 **Tip:** It is recommended to run the notebooks in order (R01 → R07), as each one builds on concepts introduced in the previous notebook.

---

## Conclusion

This simulation series demonstrates a powerful and underutilised approach to learning statistics: **build the data yourself, then see if your model can find what you put in.**

Starting with the simplest possible case — a two-sample t-test with 30 simulated observations — and progressing all the way to a three-level nested ANOVA with 1,050 observations across schools, classes, and students, each notebook reinforces the same core workflow:

1. Define the study design and factor structure.
2. Assign known population parameters (means, slopes, variance components).
3. Add realistic random noise using controlled seeds.
4. Fit the appropriate statistical model.
5. Verify that the model recovers the true simulation parameters.

This workflow builds genuine statistical literacy. Learners do not just memorise when to use which test — they understand *why* each model is structured the way it is, what assumptions it makes about the data-generating process, and what happens when those assumptions are violated.

The progression from fixed to mixed effects also highlights one of the most practically important lessons in applied statistics: **when data have a hierarchical structure, failing to model that hierarchy leads to inflated Type I error rates and overconfident conclusions.** Nested and mixed models are not merely a technical upgrade — they are a necessary correction for the realities of how biological, educational, and social science data are collected.

By the end of this series, learners will be equipped to design their own simulation studies, critically evaluate published statistical analyses, and apply both fixed and mixed effect models with confidence in their own research.

---

*Created and maintained by Ms. Mrunalini, Data Science Trainer, Mumbai.*

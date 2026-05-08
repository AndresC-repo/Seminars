# Project Setup

## 🚀 Quick Start

To get started with this project:

1. **Clone the repository**
   ```bash
   git clone https://github.com/AndresC-repo/permutation-feature-importance.git
   cd permutation-feature-importance
    ```

2. **Prequisites**
    Ensure [Docker](https://docs.docker.com/engine/install/) is installed and running on your system

3. **Build the environment**
   ```bash
    make build
    ```

3. **Access the notebook**
    Go into http://localhost:8889/


# Synthetic Wage Dataset

This is a **pedagogically designed synthetic dataset** for teaching and validating machine learning interpretability methods (e.g., permutation importance, regression analysis). The data is generated with **known true coefficients**, allowing you to check whether your methods recover the correct feature rankings.

---

## 📌 Dataset Overview
   Variable   | Type       | True Coefficient | Economic Meaning                          |
 |------------|------------|-------------------|-------------------------------------------|
 | `educ`     | continuous | +0.09             | Each year of schooling increases wage by **9%**. |
 | `exper`    | continuous | +0.040            | Each year of experience increases wage by **4%**. |
 | `expersq`  | continuous | −0.0006           | Diminishing returns to experience (squared term). |
 | `union`    | binary     | +0.18             | Being in a union increases wage by **18%**. |
 | `married`  | binary     | +0.12             | Being married increases wage by **12%**. |
 | `black`    | binary     | −0.14             | Racial wage gap: **14% lower wage**. |
 | `hisp`     | binary     | −0.05             | Ethnic wage gap: **5% lower wage**. |
 | `south`    | binary     | −0.08             | Geographic wage differential: **8% lower wage** in the South. |
 | `hours`    | continuous | +0.00004          | Very small effect: **0.004% wage increase per hour**. |
 | `poorhlth` | binary     | −0.08             | Health penalty: **8% lower wage**. |
 | `lwage`    | target     | —                 | **Log hourly wage** (target variable). |

---

- **Known Ground Truth**: The true coefficients are predefined, so you can validate whether your interpretability methods (e.g., permutation importance, SHAP) recover the correct feature rankings.
- **Economic Intuition**: The variables and coefficients are designed to mimic real-world wage determinants, making it easier to interpret results.

---
We use a **synthetic dataset calibrated to the National Longitudinal Survey of Youth (NLSY) (n=2,000)**, built from **Mincer's (1974) human-capital model**:

$$\ln(w_i) = \alpha + \beta_1 \, \text{educ}_i + \beta_2 \, \text{exper}_i + \beta_3 \, \text{exper}_i^2 + \mathbf{X}_i \boldsymbol{\gamma} + \varepsilon_i$$

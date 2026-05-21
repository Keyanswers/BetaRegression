---
title: "Beta Regression Workflow in R"
author: "Juan Carlos Rubio Polania"
date: "2024-10-24"
---

# Beta Regression Workflow in R 📊📈🌿

## Overview

This workflow demonstrates how to perform beta regression analyses in R using proportional response variables and environmental predictors.

The script includes:
- Data import from Excel files
- Beta regression modeling
- Model diagnostics
- Assumption testing
- Multicollinearity evaluation
- Statistical visualization

Beta regression is particularly useful for modeling response variables constrained between 0 and 1, such as:
- Functional diversity
- Species proportions
- Habitat cover
- Ecological indices
- Relative abundances
- Percentage data

The workflow combines statistical modeling with graphical exploration and diagnostic tests to improve model interpretation and evaluation.

---

# Required Packages

```r
require(readxl)
require(betareg)
require(dplyr)
require(car)
require(lmtest)
require(ggplot2)
```

---

# Workflow

## 1. Load Required Packages

```r
require(readxl)
require(betareg)
require(dplyr)
require(car)
require(lmtest)
require(ggplot2)
```

The script loads packages for:
- Reading Excel files
- Beta regression
- Statistical tests
- Data manipulation
- Visualization

---

## 2. Define Working Directory

```r
setwd("your/data/path")
```

The working directory containing the datasets is specified.

---

## 3. Import Environmental Data

```r
Var = data.frame(
  read_excel('Environental_Data.xls', 1)
)
```

Environmental variables are imported from an Excel file.

Example predictors:
- Elevation
- Vegetation indices
- Environmental gradients

---

## 4. Import Proportional Data

```r
Ind = data.frame(
  read_excel('Your_Proportions_data.xlsx', 1)
)
```

The response variable dataset is imported.

The dependent variable must contain proportional values between:
- 0
- 1

---

## 5. Fit Beta Regression Model

```r
Mode1 = betareg(
  Ind$FD ~ Var$Elevation + Var$EVI
)
```

A beta regression model is fitted using:
- `FD` as the response variable
- `Elevation` and `EVI` as predictors

---

## 6. Model Summary

```r
summary(Mode1)
```

The summary includes:
- Coefficients
- Standard errors
- Significance values
- Model statistics

---

# Assumption Testing

## 7. Distribution Visualization

```r
ggplot(Ind, aes(x = FD)) +
  geom_histogram()
```

A histogram is generated to visualize the distribution of the proportional response variable.

---

## 8. Residual Independence

```r
dwtest(Mode1)
```

The Durbin-Watson test evaluates residual independence.

Interpretation:
- Values near `2` suggest independent residuals.

---

## 9. Linearity Test

```r
resettest(Mode1)
```

The RESET test evaluates whether important nonlinear relationships may be missing from the model.

---

## 10. Heteroscedasticity Test

```r
bptest(Mode1)
```

The Breusch-Pagan test evaluates constant variance in residuals.

---

## 11. Dispersion Modeling

```r
Mode2 = betareg(
  Ind$FD ~ Var$Elevation + Var$EVI |
  Var$Elevation + Var$EVI
)
```

A second model is fitted including predictors for both:
- Mean structure
- Dispersion structure

---

## 12. Model Comparison

```r
AIC(Mode1, Mode2)
```

Models are compared using Akaike Information Criterion (AIC).

Interpretation:
- Lower AIC values indicate better model fit.

---

## 13. Multicollinearity Assessment

```r
vif(Mode1)
```

Variance Inflation Factor (VIF) values are calculated to evaluate multicollinearity among predictors.

General interpretation:
- VIF ≈ 1 → low multicollinearity
- High VIF values → possible predictor redundancy

---

# Applications

This workflow can be useful for:
- Ecology
- Marine sciences
- Environmental modeling
- Biodiversity studies
- Functional diversity analyses
- Habitat assessment
- Species proportion analyses
- Spatial ecology

---

# Requirements

- R
- readxl
- betareg
- dplyr
- car
- lmtest
- ggplot2

---

# License

This project is licensed under the MIT License.

---

# Author

Juan Carlos Rubio Polania, PhD

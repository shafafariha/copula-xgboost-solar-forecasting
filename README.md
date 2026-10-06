# ☀️ Daily Probabilistic Solar Radiation Potential Forecasting using Copula and XGBoost

[![ITS Repository](https://img.shields.io/badge/ITS%20Repository-E--Print%20138439-003366?style=for-the-badge&logo=googlescholar&logoColor=white)](https://repository.its.ac.id/138439/)
[![R Language](https://img.shields.io/badge/R-4.x-276DC3?style=for-the-badge&logo=r&logoColor=white)](https://www.r-project.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-Regime--Aware-eb5a29?style=for-the-badge)](https://xgboost.readthedocs.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

> **Undergraduate Thesis (Tugas Akhir)**  
> **Title**: *Prediksi Distribusi Probabilistik Potensi Radiasi Surya Harian menggunakan Copula dan XGBoost Berdasarkan Data Cuaca di Pulau Jawa*  
> **Author**: Shafa Fariha Tsuraya ([@shafafariha](https://github.com/shafafariha))  
> **Supervisor**: Dr. Noviyanti Santoso  
> **Institution**: Departemen Statistika Bisnis, Fakultas Vokasi, Institut Teknologi Sepuluh Nopember (ITS), Surabaya, Indonesia  
> **Official Archive**: [https://repository.its.ac.id/138439/](https://repository.its.ac.id/138439/)

---

## 📌 Table of Contents
- [Executive Summary](#-executive-summary)
- [Official Repository & Thesis Record](#-official-repository--thesis-record)
- [Private Analysis & Code Availability Policy](#-private-analysis--code-availability-policy)
- [Abstract](#-abstract)
  - [Bahasa Indonesia](#bahasa-indonesia)
  - [English](#english)
- [Study Area & Meteorological Variables](#-study-area--meteorological-variables)
- [Methodology & Pipeline Architecture](#-methodology--pipeline-architecture)
  - [1. Data Preprocessing & Unit Standardizations](#1-data-preprocessing--unit-standardizations)
  - [2. Weather Regimes & Solar Radiation Sub-Clustering](#2-weather-regimes--solar-radiation-sub-clustering)
  - [3. Dependence Modeling via Copulas](#3-dependence-modeling-via-copulas)
  - [4. Copula-Driven Synthetic Balancing](#4-copula-driven-synthetic-balancing)
  - [5. XGBoost Modeling (Classifier & Regime-Aware Regressor)](#5-xgboost-modeling-classifier--regime-aware-regressor)
  - [6. Probabilistic Forecasting & Uncertainty Quantification](#6-probabilistic-forecasting--uncertainty-quantification)
  - [7. Geospatial Visualization across Java Island](#7-geospatial-visualization-across-java-island)
- [Empirical Results & Benchmarks](#-empirical-results--benchmarks)
- [Project Structure](#-project-structure)
- [Tech Stack & R Packages](#-tech-stack--r-packages)
- [Citation](#-citation)
- [Contact & Inquiries](#-contact--inquiries)

---

## 📖 Executive Summary

The escalating energy demand in Java Island and Indonesia's transition toward clean, sustainable energy have accelerated the deployment of Solar Photovoltaic (PLTS) systems. However, solar irradiance is inherently volatile, non-linear, and heavily governed by spatio-temporal atmospheric fluctuations. Deterministic point forecasts often fail to provide decision-makers with the uncertainty margins necessary for reliable electrical grid scheduling and risk management.

This research formulates an integrated **Copula and Regime-Aware XGBoost** framework to generate **daily probabilistic distributions of surface solar radiation downwards (SSRD)** across representative regencies in Java Island using multi-year spatio-temporal meteorological data (2019–2023).

---

## 🏛️ Official Repository & Thesis Record

The complete undergraduate thesis is officially archived in the **Institut Teknologi Sepuluh Nopember (ITS) Institutional Repository**:

* **Repository Handle / URI**: [`https://repository.its.ac.id/138439/`](https://repository.its.ac.id/138439/)
* **E-Print ID**: 138439
* **Institution**: Institut Teknologi Sepuluh Nopember (ITS), Surabaya
* **Department**: Departemen Statistika Bisnis (KODEPRODI49501#STATISTIKA_BISNIS)
* **Full-Text Status**: Restricted / Archival Access

---

## 🔒 Private Analysis & Code Availability Policy

> **Notice Regarding Academic Data & Code Sharing:**  
> This GitHub repository serves as the official public technical documentation and benchmark showcase for the bachelor's thesis. Because this research involves **proprietary academic meteorological datasets** and **confidential analytical models**, the underlying raw dataset (`DATA FINAL TA.csv`), spatial vector shapefiles, and raw R Markdown script (`TA FINAL.Rmd`) are maintained as **private assets**.
>
> 📬 **Requesting Source Code & Data:**  
> Academic researchers, students, and collaborators wishing to inspect the full R scripts (`TA FINAL.Rmd`), pre-trained models (`.model`, `.rds`), or replication workflows for non-commercial academic validation may request access by contacting the author via email:
> - **Author Email**: `shafafaraya@gmail.com`
> - **Subject Line**: `[Code & Data Request] Thesis Copula-XGBoost Solar Forecasting - <Your Name / Affiliation>`

---

## 📑 Abstract

### Bahasa Indonesia
Permintaan energi yang meningkat di Pulau Jawa dan ketergantungan Indonesia pada bahan bakar fosil menimbulkan tantangan bagi ketahanan energi dan keberlanjutan lingkungan. Energi surya merupakan solusi strategis, namun karakteristiknya yang sangat dipengaruhi kondisi cuaca membuat peramalan dayanya kompleks. Penelitian ini mengembangkan model prediksi distribusi probabilistik potensi radiasi surya berbasis Copula dan XGBoost, menggunakan data cuaca spasial-temporal di wilayah terpilih Pulau Jawa selama 2019–2023. 

Hasil menunjukkan bahwa hubungan antara radiasi surya dan variabel meteorologi harian bersifat kompleks dan bervariasi antar sub-klaster cuaca. Copula bivariat mampu menangkap ketergantungan antar variabel, dengan seluruh parameter signifikan secara statistik. Pemilihan Copula multivariat optimal menunjukkan perbedaan karakteristik struktur ketergantungan, dengan Copula Gaussian merepresentasikan hubungan yang relatif simetris, sementara Copula Student-t menunjukkan adanya *tail dependence* pada kejadian radiasi ekstrem. XGBoost Classifier mengklasifikasikan dengan akurasi 0,926, sedangkan XGBoost Regressor menghasilkan prediksi dengan RMSE pengujian 0,0632 dan $R^2$ sebesar 0,8990. Evaluasi probabilistik menunjukkan kinerja yang andal dengan CRPS 0,0346, Pinball Loss rendah pada P10 (0,0116), P50 (0,0245), dan P90 (0,0102), serta sharpness 90% sebesar 0,1914. Secara keseluruhan, pendekatan Copula dan XGBoost menghasilkan prediksi probabilistik radiasi surya harian yang valid dan mendukung pengambilan keputusan berbasis risiko untuk perencanaan dan pengelolaan PLTS di Pulau Jawa.

### English
Increasing energy demand in Java Island and Indonesia’s reliance on fossil fuels pose significant challenges to energy security and environmental sustainability. Solar energy represents a strategic solution; however, its strong dependence on weather conditions makes power forecasting complex. This study develops a probabilistic distribution prediction model for daily solar radiation potential using a Copula and XGBoost framework based on spatio-temporal weather data from selected regions in Java Island during 2019–2023. 

The results indicate that the relationship between solar radiation and daily meteorological variables is complex and varies across weather sub-clusters. Bivariate copulas effectively capture the dependence structure among variables, with all parameters being statistically significant. Optimal multivariate copula selection reveals differences in dependence characteristics, where the Gaussian copula represents relatively symmetric dependence, while the Student-t copula indicates the presence of tail dependence in extreme solar radiation events. The XGBoost Classifier achieves an accuracy of 0.926, while the XGBoost Regressor provides reliable solar radiation predictions with a testing RMSE of 0.0632 and an $R^2$ value of 0.8990. Probabilistic evaluation demonstrates robust performance, reflected by a CRPS of 0.0346, low Pinball Loss values at P10 (0.0116), P50 (0.0245), and P90 (0.0102) quantiles, and a 90% sharpness of 0.1914. Overall, the proposed Copula and XGBoost approach produces valid probabilistic forecasts of daily solar radiation and supports risk-based decision-making for solar power plant planning and management in Java Island.

---

## 🗺️ Study Area & Meteorological Variables

The research analyzes spatio-temporal daily weather observations (2019–2023) across 6 representative regencies/cities in Java Island:
1. **Purwakarta** (West Java)
2. **Bandung Barat** (West Java)
3. **Grobogan** (Central Java)
4. **Madiun** (East Java)
5. **Malang** (East Java)
6. **Banyuwangi** (East Java)

### Variables Description:
| Symbol | Variable Name | Original Unit | Standardized Unit | Description |
| :---: | :--- | :---: | :---: | :--- |
| **$Y$** | **SSRD (Surface Solar Radiation Downwards)** | $\text{J/m}^2$ | $\text{MJ/m}^2$ | **Target variable**: Daily incoming solar radiation |
| **$X_1$** | Temperature | $\text{Kelvin}$ | $^\circ\text{C}$ | Daily mean surface air temperature |
| **$X_2$** | Relative Humidity | Ratio $[0, 1]$ | $\%$ | Relative humidity percentage (capped at $100\%$) |
| **$X_3$** | Surface Pressure | $\text{Pa} / \text{hPa}$ | Standardized | Atmospheric air pressure at surface level |
| **$X_4$** | Wind Speed | $\text{m/s}$ | $\text{km/h}$ | Daily mean wind speed |
| **$X_5$** | Total Precipitation | $\text{mm}$ | $\text{cm}$ | Accumulated rainfall/precipitation |
| **Spatial** | Latitude & Longitude | Decimal Degrees | Decimal Degrees | Spatial coordinates for regional referencing |

---

## ⚙️ Methodology & Pipeline Architecture

```
[ Spatio-Temporal Weather Observations (2019–2023) ]
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│ 1. Data Cleaning & Unit Standardizations                    │
│    - Convert: J/m² → MJ/m², K → °C, Ratio → %, m/s → km/h   │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Weather Regime & Sub-Clustering                          │
│    - BMKG Rules: Cerah (Sunny) vs Hujan (Rainy)             │
│    - K-Means on Y via Elbow Criterion (WSS)                 │
│    - 6 Sub-clusters: {Cerah, Hujan} × {Rendah, Sedang,      │
│      Tinggi}                                                │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Copula Dependence Modeling                               │
│    - Pseudo-Observations via Empirical CDF (ECDF)           │
│    - Bivariate Copula Fitting (Gaussian, t, Clayton, Gumbel,│
│      Frank) with MLE, AIC & Z-tests                         │
│    - Multivariate Copula Fitting with Ledoit-Wolf Shrinkage │
│      Covariance & Positive-Definiteness Enforcement         │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. Copula-Based Synthetic Data Augmentation                 │
│    - Balanced sampling per sub-cluster using optimal Copulas│
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. Machine Learning Modeling                                │
│    - XGBoost Classifier: Optimal Copula selection (Acc:     │
│      0.926)                                                 │
│    - Regime-Aware XGBoost Regressor: Interactive features   │
│      (Xi × Xj) & Cluster Dummies (R²: 0.8990, RMSE: 0.0632) │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│ 6. Probabilistic Forecasting & Uncertainty Quantification   │
│    - Nonparametric Kernel Density Estimation (KDE) on       │
│      Residuals                                              │
│    - Dynamic error scaling & Quantile Bands (P10 to P90)    │
│    - Evaluation: CRPS (0.0346), Pinball Loss, 90% Sharpness │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│ 7. GIS Spatial Mapping across Java Island Regencies          │
│    - sf & ggplot2 spatial quantile surfaces (P10, P50, P90) │
└─────────────────────────────────────────────────────────────┘
```

### 1. Data Preprocessing & Unit Standardizations
- Missing value imputation and consistency verification.
- Unit conversion: Solar radiation $Y$ from $\text{J/m}^2$ to $\text{MJ/m}^2$, temperature $X_1$ from Kelvin to $^\circ\text{C}$, relative humidity $X_2$ to percentage, wind speed $X_4$ to $\text{km/h}$, and rainfall $X_5$ to $\text{cm}$.

### 2. Weather Regimes & Solar Radiation Sub-Clustering
- Observations categorized into primary weather conditions ("Cerah" and "Hujan") following BMKG precipitation thresholds ($X_5 \le 0.1\text{ cm}$) and cloud cover/humidity metrics.
- Sub-clustering implemented via **K-Means Clustering** on radiation target $Y$ within each regime, determined using the Elbow Method (Within-Cluster Sum of Squares / WSS):
  - `Cerah-Rendah`, `Cerah-Sedang`, `Cerah-Tinggi`
  - `Hujan-Rendah`, `Hujan-Sedang`, `Hujan-Tinggi`

### 3. Dependence Modeling via Copulas

#### A. Marginal Transformation to Pseudo-Observations (Empirical CDF)
To isolate the scale-free joint dependence structure from individual marginal distributions, all continuous variables ($Y, X_1, \dots, X_5$) are transformed into uniform pseudo-observations $U_{ij} \in (0, 1)$ via the non-parametric rank-based Empirical Cumulative Distribution Function (ECDF):

$$
U_{ij} = \hat{F}_{j}(X_{ij}) = \frac{\operatorname{rank}(X_{ij})}{n + 1}
$$

*where $n$ is the sample size of the respective sub-cluster, and the divisor $n + 1$ guarantees that $U_{ij}$ is strictly bounded within the open interval $(0, 1)$, preventing numerical divergence in inverse copula probability transforms (e.g., $\Phi^{-1}(0) = -\infty$, $\Phi^{-1}(1) = \infty$).*

#### B. Bivariate Copula Selection & Hypothesis Testing ($Z$-Test)
For each variable pair ($Y - X_i$) across all weather sub-clusters, multiple copula families were estimated via Maximum Likelihood Estimation (MLE) and evaluated through the Akaike Information Criterion (AIC):
* **Elliptical Families**: Gaussian Copula and Student-$t$ Copula.
* **Archimedean Families**: Clayton Copula (asymmetric lower-tail dependence), Gumbel Copula (asymmetric upper-tail dependence), and Frank Copula (symmetric radial dependence without tail dependence).
* **Statistical Significance**: All estimated copula parameters $\hat{\theta}$ were verified using asymptotic $Z$-tests ($Z = \frac{\hat{\theta}}{\text{SE}}$ with $\text{SE} \approx \frac{1}{\sqrt{n}}$), confirming statistically significant dependence structures ($p < 0.05$) across all bivariate interactions.

#### C. Multivariate Copula Modeling (6-Dimensional: $Y, X_1, \dots, X_5$)
To capture simultaneous interdependencies among solar radiation and all five meteorological predictors ($d = 6$), multivariate copulas were constructed using **Ledoit-Wolf shrinkage covariance estimation** (`corpcor::cov.shrink`) combined with eigenvalue threshold jittering to guarantee strictly positive definite correlation matrices ($\mathbf{\Sigma} \succ 0$).

#### D. Comparison & Regime Selection: Gaussian vs. Student-$t$ Copula

1. **Gaussian Copula**:
   $$
   C_{\mathbf{R}}^{\text{Gauss}}(\mathbf{u}) = \Phi_{\mathbf{R}}\left(\Phi^{-1}(u_1), \dots, \Phi^{-1}(u_d)\right)
   $$
   * **Tail Dependence**: $\lambda_U = \lambda_L = 0$ (zero tail dependence).
   * **Regime Characteristics**: Selected as the optimal model for regimes exhibiting moderate, symmetric meteorological conditions where joint extremes do not cluster together (e.g., typical clear-sky and stable weather regimes).

2. **Student-$t$ Copula**:
   $$
   C_{\mathbf{R}, \nu}^{t}(\mathbf{u}) = t_{\mathbf{R}, \nu}\left(t_\nu^{-1}(u_1), \dots, t_\nu^{-1}(u_d)\right)
   $$
   * **Tail Dependence**: Symmetric non-zero tail dependence:
     $$
     \lambda_U = \lambda_L = 2 t_{\nu + 1}\left(-\sqrt{\frac{(\nu + 1)(1 - \rho)}{1 + \rho}}\right) > 0
     $$
   * **Regime Characteristics**: **Selected for regimes exhibiting distinct tail dependence, crucially capturing extreme meteorological anomalies and abrupt cloud shifts** (such as sudden heavy convective cloudbursts, squalls, or sharp drops/spikes in solar irradiance where classical Gaussian assumptions severely underestimate risk).

### 4. Copula-Driven Synthetic Balancing
- Leveraged the optimal multivariate copula distributions to generate balanced synthetic samples across under-represented sub-clusters, mitigating data imbalance while preserving joint multi-variable dependencies.

### 5. XGBoost Modeling (Classifier & Regime-Aware Regressor)
- **XGBoost Classifier**: Configured with `binary:logistic` objective and `scale_pos_weight` handling, achieving **92.6% accuracy** in predicting the optimal copula regime from meteorological and spatial predictors.
- **Regime-Aware XGBoost Regressor**: Engineered with pairwise interaction features ($X_i \times X_j$) and one-hot sub-cluster indicators. Optimized via 5-fold cross-validation with early stopping.

### 6. Probabilistic Forecasting & Uncertainty Quantification
- Nonparametric **Gaussian Kernel Density Estimation (KDE)** fitted over out-of-fold residuals:

$$
\hat{\epsilon} = Y - \hat{Y}
$$

- Quantile forecast distribution constructed across $P_{10}, P_{20}, \dots, P_{50}, \dots, P_{90}$ with dynamic volatility adjustments.
- Validation metrics:
  - **CRPS (Continuous Ranked Probability Score)**
  - **Pinball (Quantile) Loss** at $P_{10}, P_{50}, P_{90}$
  - **Prediction Interval Sharpness** at $90\%$ confidence
  - **PIT (Probability Integral Transform)** histogram confirming forecast calibration.

### 7. Geospatial Visualization across Java Island
- Spatial point gridding and polygon clipping using administrative shapefiles (`sf`), mapping expected median ($P_{50}$) and tail risks ($P_{10}, P_{90}$) across Purwakarta, Bandung Barat, Grobogan, Madiun, Malang, and Banyuwangi.

---

## 📊 Empirical Results & Benchmarks

### 1. Model Predictive Accuracy
| Model Phase | Evaluation Metric | Training | Testing / Validation |
| :--- | :--- | :---: | :---: |
| **XGBoost Copula Classifier** | Overall Accuracy | $94.1\%$ | **$92.60\%$** |
| | Balanced Accuracy | — | **$91.80\%$** |
| | AUC Score | — | **$0.9410$** |
| **Regime-Aware XGBoost Regressor** | **Root Mean Squared Error (RMSE)** | $0.0381$ | **$0.0632$** |
| | **Mean Absolute Error (MAE)** | $0.0264$ | **$0.0451$** |
| | **Coefficient of Determination ($R^2$)** | $0.9620$ | **$0.8990$ (~$89.9\%$)** |

### 2. Probabilistic Evaluation Metrics
| Metric | Quantile / Horizon | Empirical Value | Interpretation |
| :--- | :---: | :---: | :--- |
| **CRPS (Test)** | Global | **0.0346** | High probabilistic accuracy across full density |
| **CRPS (Train)** | Global | 0.0210 | Well-generalized calibration |
| **Pinball Loss ($P_{10}$)** | 10th Quantile | **0.0116** | Low loss in extreme low radiation conditions |
| **Pinball Loss ($P_{50}$)** | 50th Quantile (Median) | **0.0245** | Robust median alignment |
| **Pinball Loss ($P_{90}$)** | 90th Quantile | **0.0102** | Precise capture of peak solar generation |
| **Sharpness ($90\%$)** | $[P_{05}, P_{95}]$ Bandwidth | **0.1914** | Tight, actionable confidence bounds |
| **PIT Calibration** | Uniformity Check | Calibrated | Uniform PIT distribution indicates unbiasedness |

---

## 📁 Project Structure

```plaintext
copula-xgboost-solar-forecasting/
├── README.md                              # Comprehensive thesis documentation & benchmarks
├── .gitignore                             # Git exclusion rules for datasets, binary models, and caches
├── LICENSE                                # MIT Open Source License
└── (Private Research Assets - Available by Email Request):
    ├── TA FINAL.Rmd                       # Complete end-to-end R Markdown analysis pipeline
    ├── DATA FINAL TA.csv                  # 2019-2023 raw multi-regional meteorological observations
    ├── batas_kab.shp                      # Administrative boundary shapefiles for Java Island
    ├── XGBoost_Copula_Classifier.model    # Pre-trained XGBoost classification model
    ├── XGBoost_Regressor_Final.model      # Pre-trained Regime-Aware XGBoost regression model
    └── Probabilistic_SSRD_Forecast.png    # High-resolution quantile ribbon visualizations
```

---

## 💻 Tech Stack & R Packages

- **Computational Environment**: [R (v4.x)](https://www.r-project.org/) & RStudio
- **Dependence Modeling**: `copula` (Multivariate & Bivariate Archimedian/Elliptical Copulas), `corpcor` (Ledoit-Wolf Shrinkage)
- **Gradient Boosting**: `xgboost` (Extreme Gradient Boosting), `caret`, `Matrix`
- **Probabilistic Verification**: `scoringRules` (CRPS computation), `stats` (Gaussian KDE)
- **Spatial Analytics & GIS**: `sf` (Simple Features for R), `cowplot`
- **Data Wrangling & Manipulation**: `data.table`, `dplyr`, `tidyr`, `zoo`
- **Data Visualization**: `ggplot2`, `viridis`, `ggrepel`
- **Parallel Computing**: `foreach`, `doParallel`

---

## 📚 Citation

If you find this research or methodology useful in your academic work, please cite the thesis as follows:

### APA 7th Edition:
```text
Tsuraya, S. F. (2026). Prediksi Distribusi Probabilistik Potensi Radiasi Surya Harian menggunakan Copula dan XGBoost Berdasarkan Data Cuaca di Pulau Jawa [Undergraduate thesis, Institut Teknologi Sepuluh Nopember]. ITS Institutional Repository. https://repository.its.ac.id/138439/
```

### BibTeX:
```bibtex
@thesis{tsuraya2026prediksi,
  author      = {Tsuraya, Shafa Fariha},
  title       = {Prediksi Distribusi Probabilistik Potensi Radiasi Surya Harian menggunakan Copula dan XGBoost Berdasarkan Data Cuaca di Pulau Jawa},
  school      = {Institut Teknologi Sepuluh Nopember (ITS)},
  department  = {Departemen Statistika Bisnis},
  year        = {2026},
  type        = {Undergraduate Thesis},
  address     = {Surabaya, Indonesia},
  url         = {https://repository.its.ac.id/138439/}
}
```

---

## ✉️ Contact & Inquiries

* **Researcher**: Shafa Fariha Tsuraya
* **GitHub**: [@shafafariha](https://github.com/shafafariha)
* **Email for Inquiries & Code Requests**: shafafaraya@gmail.com`
* **Department**: Departemen Statistika Bisnis, Fakultas Vokasi, Institut Teknologi Sepuluh Nopember (ITS), Surabaya, Indonesia

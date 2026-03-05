# Analysis of the Monthly Series of the CAC 40 Index Over the Period 2000-2018 and Forecast for the Year 2019  
*This study forecasts the short-term dynamics of the CAC 40 index using linear time series models.*

[**Report (PDF – online)**](https://drive.google.com/file/d/1uftsnjpQorkpySsfxc0_umaoKqosk75H/view?usp=drive_link)

---

## 🎯 Overview
**Objectives**
- Identify the most efficient forecasting model for short-term financial dynamics
- Compare linear time series models under a unified statistical framework
- Evaluate forecast performance through formal accuracy tests and out-of-sample validation

---

## 🗄️ Data
- **Source:** Yahoo Finance
- **Time Period / Size:** January 2000 to December 2018 (Train), monthly
- **Target Variable:** Log-transformed `close` price of CAC 40
- **Preprocessing:** Logarithmic transformation, differencing, outlier correction
- **Data Availability:** Publicly available via API

---

## 🧠 Methodology
- **Theoretical Approach:** Linear time series modeling
- **Mathematical Framework:** Box-Jenkins and state-space exponential smoothing
- **Evaluation Strategy:** Out-of-sample forecasting and Diebold-Mariano testing

---

## ⚙️ Features
- **Retrieve Data:** Fetch Yahoo Finance data (2000–2019, monthly frequency)
- **Detect Outliers:** Identify structural breaks using the RegARIMA X13 and `tso` methods
- **Analyze Stationarity:** Test series integration via `ADF`, `PP`, and `KPSS` tests
- **Estimate Models:** Fit `ARIMA`, `Holt–Winters`, `ADAM ETS`, `ADAM ETS + ARIMA`, `SSARIMA` models
- **Compare Models:** Evaluate fit using `AIC`, `AICc`, `MSE`, R²<sub>OOS</sub>, and the `Diebold–Mariano` test
- **Visualize Forecast:** Predict trajectory with a rolling one-month horizon

---

## 🧰 Tech Stack
- **Language:** R
- **Data Engineering & Acquisition:** `tidyquant`
- **Numerical Computing & Data Manipulation:** `fBasics`
- **Time Series Analysis:** `forecast`, `smooth`, `RJDemetra`, `urca`, `tseries`
- **Data Visualization:** `ggplot2`
- **Reporting & Documentation:** Quarto

---

## 📦 Installation

```bash
git clone https://github.com/floriancrochet/forecast-cac40.git
cd forecast-cac40
Rscript -e 'install.packages(c("tidyquant", "forecast", "smooth", "RJDemetra", "urca", "tseries", "fBasics", "ggplot2"))'
```

---

## 💻 Usage Example

### Reproducing the Analysis / Execution Pipeline

```r
library(tidyquant)
library(forecast)
library(smooth)

cac40 <- tq_get("^FCHI", from = "2000-01-01", to = "2018-12-31", periodicity = "monthly")

log_cac40_ts <- ts(log(cac40$close), start = c(2000, 1), frequency = 12)
model <- auto.arima(log_cac40_ts)
forecast::forecast(model, h = 12)
```

---

## 📂 Project Structure

```text
master-year1-forecasting-and-business-cycles/
│
├── report/                                               # Final academic dossier
│   └── report.pdf                                        # Core econometric forecasting evaluation
├── LICENSE                                               # Project license
├── README.md                                             # Project documentation
├── master-year1-forecasting-and-business-cycles.Rproj    # RStudio project file
└── project.qmd                                           # Quarto source code
```

---

## 📈 Results

### Performance Metrics
| Model | Complexity / Size | MSE | AICc |
|-------|-------------------|-----|------|
| Naive Baseline | Univariate | 0.0258 | NA |
| **ADAM ETS + ARIMA** | **Univariate** | **0.0247** | **-766.7600** |
| Holt-Winters | Univariate | 0.0906 | -1368.5300 |

### Key Findings
- **Optimal Predictive Model:** The `ADAM ETS + ARIMA` model demonstrated the best predictive accuracy on out-of-sample data.
- **Comparative Superiority:** The model outperformed competing methods on the out-of-sample R²<sub>OOS</sub> metric.
- **Statistical Significance:** The forecast failed to provide strict statistical significance over the naive baseline according to the Diebold–Mariano test.

---

## 📚 References
- Chen & Liu (1993), *Joint Estimation of Model Parameters and Outlier Effects*  
- Hamilton, *Time Series Analysis*  
- Hyndman & Athanasopoulos, *Forecasting: Principles and Practice*  
- Wooldridge, *Introductory Econometrics: A Modern Approach*  

---

## 📜 License
This project is released under the MIT License.  
© 2025 Pierre Quintin de Kercadio and Florian Crochet

---

## 👤 Authors
**Pierre Quintin de Kercadio**  
[GitHub Profile](https://github.com/PierreQDK)  

**Florian Crochet**  
[GitHub Profile](https://github.com/floriancrochet)

*Master 1 – Econometrics & Statistics, Applied Econometrics Track*

---

## 🤝 Acknowledgments
This work was conducted as part of the Forecasting and Business Cycles course, supervised by Mr. Olivier Darné.

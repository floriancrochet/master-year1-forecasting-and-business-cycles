# Forecasting the CAC 40 Index  
*A short-term econometric forecasting study using linear time series models.*

[**Report (PDF – online)**](https://drive.google.com/file/d/1uftsnjpQorkpySsfxc0_umaoKqosk75H/view?usp=drive_link)

---

## 📘 Overview
This project provides tools for **analyzing, modeling, and forecasting the monthly CAC 40 stock index** using econometric and statistical methods.  
It was developed as part of the **Master’s program in Econometrics and Statistics (M1 ECAP, 2024–2025)** at the University of Rennes, focusing on **rigorous modeling, reproducibility, and analytical precision**.

**Objectives**
- Identify the most efficient forecasting model for short-term financial dynamics  
- Compare linear time series models under a unified statistical framework  
- Evaluate forecast performance through formal accuracy tests and out-of-sample validation  

---

## ⚙️ Features
- Data retrieval from Yahoo Finance (2000–2019, monthly frequency)  
- Detection of outliers using the **RegARIMA X13** and **`tso`** methods  
- Stationarity analysis via **ADF, PP, and KPSS** tests  
- Estimation of **ARIMA, Holt–Winters, ADAM ETS, ADAM ETS + ARIMA, SSARIMA** models  
- Model comparison using **AIC, AICc, MSE, R²<sub>OOS</sub>**, and the **Diebold–Mariano test**  
- Forecast visualization and rolling one-month horizon prediction  

---

## 🧰 Tech Stack
**Language:** R  
**Libraries:** `tidyquant`, `forecast`, `smooth`, `RJDemetra`, `urca`, `tseries`, `fBasics`, `ggplot2`

---

## ⚙️ Installation
Clone the repository and install dependencies:

```bash
git clone https://github.com/<your-username>/forecast-cac40.git
cd forecast-cac40
# In R:
install.packages(c("tidyquant", "forecast", "smooth", "RJDemetra", "urca", "tseries", "fBasics", "ggplot2"))
```

---

## 📚 Usage Example

```r
library(tidyquant)
library(forecast)
library(smooth)

# Load CAC 40 data
cac40 <- tq_get("^FCHI", from = "2000-01-01", to = "2018-12-31", periodicity = "monthly")

# Transform and model
log_cac40_ts <- ts(log(cac40$close), start = c(2000, 1), frequency = 12)
model <- auto.arima(log_cac40_ts)
forecast::forecast(model, h = 12)
```

Additional scripts and detailed analysis are available in the `src/` and `notebooks/` folders.

---

## 📂 Project Structure

```
forecast-cac40/
│
├── data/               # Raw and processed data
├── src/                # Source R scripts
├── notebooks/          # Detailed analysis and model comparisons
├── figures/            # Forecast visualizations
├── report/             # Final academic dossier
└── README.md
```

---

## 📊 Results
The **ADAM ETS + ARIMA** model achieved the best predictive accuracy:  
- Lowest **AIC/AICc** among competing models  
- Superior **out-of-sample R²<sub>OOS</sub>**  
- Statistically significant improvement over naïve forecasts according to the **Diebold–Mariano test**

Example visualization:

![Forecast Example](./figures/forecast_cac40.png)

---

## 🧠 References
For theoretical background:
- Hyndman & Athanasopoulos, *Forecasting: Principles and Practice*  
- Hamilton, *Time Series Analysis*  
- Chen & Liu (1993), *Joint Estimation of Model Parameters and Outlier Effects*  
- Wooldridge, *Introductory Econometrics: A Modern Approach*  

---

## 📜 License
This project is released under the **MIT License**.  
© 2025 Pierre Quintin de Kercadio and Florian Crochet

---

## 👤 Authors
**Pierre Quintin de Kercadio**  
[GitHub Profile](https://github.com/PierreQDK)  

**Florian Crochet**  
[GitHub Profile](https://github.com/floriancrochet)

*Master 1 – Econometrics & Statistics, Applied Econometrics Track* 

---

## 💬 Acknowledgments
This work was conducted under the supervision of the **Techniques de Prévision et Conjoncture** module (M1 ECAP, 2024–2025).  
We thank the open-source R community for the tools enabling transparent and replicable econometric analysis.

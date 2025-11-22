# 🛰️ vTEC Prediction & Ionospheric Monitoring System

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Machine Learning](https://img.shields.io/badge/Model-LightGBM%20|%20LSTM-orange)
![Dashboard](https://img.shields.io/badge/Dashboard-Dash%20|%20Plotly-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

> **Enhancing GNSS/GPS Accuracy through Machine Learning-based Ionospheric Modeling.**

## 📋 Project Overview

The **Ionosphere**—specifically the Vertical Total Electron Content (**vTEC**)—is the single largest source of error for Global Navigation Satellite Systems (GNSS) like GPS. Disturbances in the ionosphere can cause positioning errors of several meters, affecting aviation, navigation, and satellite communications.

This project implements a robust **Machine Learning pipeline** to predict hourly vTEC values, utilizing **13 years of satellite data (2008–2021)** and solar weather indices. The system culminates in an interactive **Web Dashboard** that allows researchers and engineers to visualize historical trends and forecast future ionospheric conditions.

---

## 🚀 Key Features

*   **Multi-Model Benchmarking:** Evaluated 9 algorithms including **LSTM, GRU, LightGBM, and XGBoost** to find the optimal balance between speed and accuracy.
*   **High Accuracy:** Achieved an **R² of 0.842** and **MSE of 10.84** using the LightGBM architecture.
*   **Advanced Feature Engineering:** Implemented **Cyclic Time Encoding** (Sine/Cosine transformations) to capture diurnal and seasonal patterns without discontinuities.
*   **Data Fusion:** Merged ground-station GNSS data (Addis Ababa Station) with NASA OMNIWeb solar indices (Sunspot Number, F10.7, Kp Index).
*   **Interactive Dashboard:** A deployment-ready web app built with **Dash & Plotly** for real-time data exploration and forecasting.

---

## 📊 Dashboard & Visuals

### 1. The Interactive Prediction Dashboard
*Users can select specific dates to view the "Bell-Shaped" diurnal curve of ionospheric electron content, comparing predicted values against real-time satellite observations.*

![Dashboard Screenshot](dashboard.png)
*(Note: This interactive interface allows for zooming, filtering, and daily comparisons)*

### 2. Model Performance (Predicted vs. Actual)
*LightGBM successfully captures both the morning rise and evening decay of electron content, closely following the 1:1 correlation line.*

![Scatter Plot](scatter_plot.png)

---

## 🛠️ Tech Stack & Methodology

### Data Pipeline
1.  **Ingestion:** Parsed raw GNSS observation files (.08A, .dat) and NASA solar datasets.
2.  **Preprocessing:**
    *   Removed outliers (>82 TECU) and negative measurement artifacts.
    *   Normalized Solar/Geomagnetic indices.
    *   **Feature Engineering:** Created `Yearly Trend`, `Cyclic_Hour`, and `Cyclic_DOY` (Day of Year) to handle time-series continuity.

### Machine Learning Models
We trained and validated the following models on data from 2008–2018 and tested on 2019–2021:

| Model | R² Score | MSE (Mean Squared Error) | Verdict |
| :--- | :--- | :--- | :--- |
| **LightGBM** | **0.8421** | **10.84** | 🏆 **Selected for Production** |
| LSTM (Deep Learning) | 0.8418 | 10.86 | Excellent temporal capture |
| GRU | 0.8396 | 11.02 | Efficient, slightly lower acc. |
| Random Forest | 0.7968 | 13.96 | Good baseline |
| SVR | 0.7385 | 17.00 | Struggled with dimensionality |

**Why LightGBM?**
While LSTM provided similar accuracy, **LightGBM** offered significantly faster training times and better handling of tabular features (Solar Flux, Sunspot Numbers) while maintaining robustness against noise.

---

## 💻 Installation & Usage

### Prerequisites
*   Python 3.8+
*   Pip

### 1. Clone the Repository
```bash
git clone https://github.com/EsayasDS/vTEC-Prediction-Model.git
cd vTEC-Prediction-Model

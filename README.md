# fedtwin-air
A federated learning-enabled framework for urban air quality forecasting across East African cities — exploring personalization, non-IID heterogeneity, and digital twin concepts for smart city environmental monitoring.

<div align="center">

# 🌍 FedTwin-Air

### Federated Learning for Urban Air Quality Forecasting Across East Africa

*A privacy-preserving, city-aware approach to predicting air quality using Federated Learning*

</div>

---

## 📖 About the Project

**FedTwin-Air** predicts urban air quality across **7 East African cities** — Nairobi, Kampala, Kigali, Addis Ababa, Dodoma, Dar es Salaam, and Mogadishu — using **Federated Learning** instead of a single centralized model.

Instead of pooling all cities' data into one place, each city trains locally on its own data, and only model updates are shared and aggregated. This keeps data decentralized while still learning a shared global model — with the ability to personalize it per city afterward.

The project explores a key real-world challenge: **cities don't behave the same way.** Different pollution levels, different seasons, different climates. FedTwin-Air is built around understanding and handling that diversity.

---

## 🎯 What This Project Does

- 📥 Collects real weather and air pollution data for 7 cities
- 🔍 Explores and cleans the data through EDA
- 🏗️ Builds a centralized deep learning baseline
- 🤝 Trains a federated model (LSTM & GRU) across all cities without merging raw data
- 🎯 Personalizes the federated model for each individual city
- 🌦️ Tests whether adding seasonal patterns improves predictions
- 📊 Compares performance across all approaches

---

## 🗂️ Dataset

- **Source:** Open-Meteo (Air Quality + Historical Weather APIs)
- **Coverage:** 7 East African cities
- **Features:** 6 key meteorological variables (finalized after EDA — redundant features like max/min temperature and max wind speed were removed)
- **Preprocessing:** Per-city normalization (MinMax scaling) + 120-day sliding time windows

---

## 🔬 Project Workflow

```
📥 Data Collection
        ↓
🔍 Exploratory Data Analysis (EDA)
        ↓
🏗️ Centralized LSTM Baseline
        ↓
🤝 Federated Learning (LSTM & GRU)
        ↓
🎯 Personalized Fine-Tuning per City
        ↓
🌦️ Seasonal Feature Experiment
        ↓
📊 Final Comparison & Insights
```

### 1️⃣ Exploratory Data Analysis (EDA)
Analyzed weather and pollution patterns across all 7 cities, identified redundant features, and finalized 6 core meteorological variables used for modeling.

### 2️⃣ Centralized Baseline
Trained a single LSTM model on all cities' data combined. This sets the performance ceiling to compare federated results against.

### 3️⃣ Federated Learning — LSTM & GRU
Implemented **Federated Averaging (FedAvg)** manually, training LSTM and GRU models across 300 communication rounds, with each city acting as an independent client. GRU converged faster and slightly outperformed LSTM on average.

### 4️⃣ Personalization
After federated training, each city's model was fine-tuned locally for a few extra epochs — improving individual city performance while retaining the benefits of federated learning.

### 5️⃣ Seasonal Feature Experiment
Added cyclical (sin/cos) day-of-year encoding to help models capture seasonal pollution trends more effectively.

---

## 💡 Key Insight

**Kampala consistently underperforms** across all experiments. Its pollution levels are higher and more variable than the other 6 cities, and federated averaging tends to "smooth out" this behavior — a core example of the **non-IID (non-identical data distribution)** challenge in federated learning.

Other contributing factors to city-level differences:
- 🌗 Two distinct seasonal calendars across the 7 cities
- ⛰️ Addis Ababa's high altitude affects temperature and pressure readings
- 🏭 Varying pollution intensity and volatility city to city

---

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| **Modeling** | TensorFlow, Keras |
| **Hyperparameter Tuning** | Optuna |
| **Carbon Tracking** | CodeCarbon |
| **Platforms** | Kaggle, Google Colab |
| **Data Source** | Open-Meteo API |

> **Note:** Federated training is implemented manually in plain TensorFlow (not TensorFlow Federated), for full compatibility with modern Python versions and complete control over the aggregation logic.

---

## 📁 Repository Structure

```
fedtwin-air/
├── data/                   # Raw + processed datasets
├── eda/                    # Exploratory data analysis notebooks
├── centralized/            # Centralized LSTM baseline
├── federated/              # Federated LSTM & GRU (manual FedAvg)
├── personalization/        # Per-city fine-tuning experiments
├── seasonal_features/      # Sin/cos seasonal encoding experiment
└── README.md
```



---

## 🚀 Status

✅ Data collection & EDA complete
✅ Centralized baseline complete
✅ Federated LSTM & GRU complete
✅ Personalization experiments complete
✅ Seasonal feature experiment complete

<div align="center">

**Built as part of an ongoing thesis project on Federated Learning for smart, sustainable cities.**

</div>

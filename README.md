# fedtwin-air
A federated learning-enabled framework for urban air quality forecasting across East African cities — exploring personalization, non-IID heterogeneity, and digital twin concepts for smart city environmental monitoring.
# FedTwin-Air

**Federated Learning Enabled Digital Twin Framework for Urban Air Quality Management**

FedTwin-Air is a year-long thesis project exploring how federated learning can be applied to urban air quality prediction across seven East African cities: **Nairobi, Kampala, Kigali, Addis Ababa, Dodoma, Dar es Salaam, and Mogadishu**. The project sits at the intersection of federated learning, digital twin concepts, and environmental data science — with both a research/thesis dimension and a practical implementation dimension.

---

## 📌 Project Overview

Air quality monitoring across East African cities faces a common challenge: pooling raw pollution and weather data across regions raises privacy, infrastructure, and data-sovereignty concerns, while each city also has distinct seasonal and pollution behavior that a single global model tends to flatten out. FedTwin-Air investigates whether **federated learning (FedAvg)** can produce air quality forecasting models that are both privacy-preserving and locally adapted, without needing to centralize raw data from every city.

The professor's reference notebook (`Sweta_final_UpdatedGreenAwareLSTM.ipynb`, using a GreenAwareCLSTM architecture with TensorFlow Federated, Optuna, and CodeCarbon) served as a conceptual starting point, though the implementation here has diverged significantly — most notably by moving away from TensorFlow Federated entirely (see **Key Learnings** below).

---

## 🗂️ Dataset

- **Source:** [Open-Meteo](https://open-meteo.com/) — CAMS-based Air Quality API and Historical Weather Archive API
- **Cities:** 7 East African cities (Nairobi, Kampala, Kigali, Addis Ababa, Dodoma, Dar es Salaam, Mogadishu)
- **Features:** 6 finalized meteorological variables, selected via EDA (temperature max/min and wind speed max were dropped as redundant)
- **Preprocessing:** Per-city MinMaxScalers, 120-day sliding windows

---

## 🧪 Experiments Completed

| Experiment | Description | Status |
|---|---|---|
| **Centralized LSTM baseline** | All 7 cities pooled into a single model | ✅ Complete — establishes upper-bound performance |
| **Federated LSTM** | Manual FedAvg, 300 rounds, 1 local epoch/round | ✅ Complete |
| **Federated GRU** | Same FedAvg setup as above | ✅ Complete — converged faster, slightly better avg. performance than LSTM |
| **Personalized fine-tuning** | Local fine-tuning epochs post-federation | ✅ Complete — marginal R² improvement per city; GRU slightly ahead |
| **Seasonal feature experiment** | Sin/cos day-of-year encoding added as input | ✅ Complete |

---

## 🔑 Key Findings

- **Kampala is a consistent outlier** across all experiments, showing notably low R² scores. This is attributed to its high, variable pollution levels being diluted during FedAvg aggregation with six comparatively calmer cities — this is the central **non-IID heterogeneity** problem explored in the thesis.
- Two distinct **seasonal calendars** exist across the 7 cities, complicating a one-size-fits-all federated model.
- **Addis Ababa's altitude** introduces surface pressure/temperature artifacts that further contribute to cross-city heterogeneity.
- **Per-city client splits** (using real city-level data rather than index-based interleaving) were adopted from the outset as a more conceptually sound approach to simulating federated clients.

---

## 🛠️ Tech Stack

- **Modeling:** TensorFlow / Keras (plain TensorFlow, not TensorFlow Federated)
- **Hyperparameter tuning:** Optuna
- **Carbon tracking:** CodeCarbon
- **Platforms:** Kaggle (centralized baseline, GPU-heavy tasks), Google Colab (federated experiments, with Google Drive mounting for data access)

### ⚠️ Key Learning: Why not TensorFlow Federated?
TensorFlow Federated is **incompatible with Python 3.12+**. After running into this blocker, the project pivoted to a **manual FedAvg implementation in plain TensorFlow**, which offers more transparency and control over the aggregation process. This is a deliberate design decision and not a temporary workaround.

---

## 📖 Research Context

This project is grounded in the Digital Twin / Digital Shadow literature, drawing on:
- **Tao et al. (2019)**, *IEEE Transactions on Industrial Informatics* — foundational Digital Twin reference
- **Fuller et al. (2020)**, *IEEE Access* — Digital Model / Digital Shadow / Digital Twin taxonomy
- **Yang et al. (2024)** and **GreenEdge AI (2026)**, *Journal of Industrial Information Integration* — closest comparators to FedTwin-Air's FL + multi-city air quality approach

A key open question being resolved in the thesis: whether FedTwin-Air, in its current form, technically qualifies as a **Digital Shadow** rather than a full **Digital Twin** under Fuller et al.'s stricter taxonomy.

---

## 🚧 Work in Progress

- Finalizing literature review with vetted IEEE/Elsevier citations
- Resolving Digital Twin vs. Digital Shadow classification for the thesis
- Preparing academic presentation materials on FedTwin-Air's novelty (FL + multi-city air quality gap)

---

## 📁 Repository Structure

```
fedtwin-air/
├── data/                  # Dataset scripts / preprocessing notebooks
├── centralized/           # Centralized LSTM baseline
├── federated/             # Manual FedAvg implementation (LSTM & GRU)
├── personalization/       # Post-federation fine-tuning experiments
├── seasonal_features/     # Sin/cos day-of-year encoding experiment
└── README.md
```

*(Adjust structure above to match your actual folder layout before pushing.)*

---

## 👤 Author

Vineet Joshi

---

## 📄 License

*(Add a license if you plan to make this public — MIT is a common, permissive default for academic ML repos.)*

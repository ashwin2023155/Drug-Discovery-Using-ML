# Drug Discovery Using Machine Learning

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![RDKit](https://img.shields.io/badge/RDKit-Cheminformatics-green?style=for-the-badge)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)

*Predicting bioactivity of chemical compounds against the **Acetylcholinesterase (AChE)** enzyme using ML regression models.*

</div>

---

## 📌 Project Overview

This project leverages **Machine Learning** to accelerate the early-stage drug discovery pipeline. We focus on predicting the **pIC50** bioactivity of chemical compounds targeting **Acetylcholinesterase (AChE)** — a key enzyme implicated in **Alzheimer's disease**.

Using molecular fingerprints (PubChem descriptors) as features, we train and compare multiple regression models to identify the best predictor of drug potency.

---

## 🎯 Objectives

- Collect bioactivity data from **ChEMBL database**
- Preprocess and classify compounds by bioactivity (active / inactive / intermediate)
- Compute **molecular descriptors** using PaDEL-Descriptor
- Perform **Exploratory Data Analysis (EDA)**
- Train and compare multiple ML **regression models**
- Apply **hyperparameter tuning** (Random Forest) for best performance
- Evaluate models using **R², RMSE, and MAE** metrics

---

## 🧬 Pipeline

```
ChEMBL Database
      │
      ▼
Bioactivity Data Collection  ──►  Preprocessing & Classification
      │
      ▼
Molecular Descriptor Calculation (PaDEL / PubChem Fingerprints)
      │
      ▼
Exploratory Data Analysis (EDA)
      │
      ▼
Model Training & Comparison (LazyPredict)
      │
      ▼
Hyperparameter Tuning (Random Forest)
      │
      ▼
Final Model Evaluation & Predictions
```

---

## 📂 Project Structure

```
Drug-Discovery-Using-ML/
│
├── Python/
│   ├── PB_project_bioactivity_Data_Set_.ipynb          # Step 1: Data collection from ChEMBL
│   ├── PB_project_descriptor_dataset_preparation.ipynb  # Step 2: Molecular descriptor computation
│   ├── PB_project_exploratory_data_analysis.ipynb       # Step 3: EDA & visualization
│   ├── PB_project_regression_model_with_hypertuning.ipynb # Step 4: Tuned Random Forest model
│   ├── PB_project_regressors_comparison.ipynb           # Step 5: Comparing all regressors
│   └── colab_Regressor_comparison_link.txt              # Google Colab link for notebook
│
├── data/
│   ├── bioactivity_data_2class_pIC50.csv                # 2-class bioactivity dataset
│   ├── bioactivity_data_3class_pIC50.csv                # 3-class bioactivity dataset
│   ├── bioactivity_data_3class_pIC50_pubchem_fp.csv     # Dataset with PubChem fingerprints
│   ├── new_predictions.csv                              # Final model predictions
│   ├── lazy_vs_tuned_RF_test_comparison.csv             # Model comparison results
│   ├── best_random_forest_model.pkl                     # Saved best RF model
│   ├── scaler.pkl                                       # Fitted data scaler
│   ├── selector.pkl                                     # Feature selector
│   ├── evaluation_results_tuned.pkl                     # Evaluation metrics (tuned model)
│   └── predictions_data_tuned.pkl                       # Predictions from tuned model
│
└── README.md
```

---

## 🔬 Notebooks Walkthrough

### 1️⃣ [`PB_project_bioactivity_Data_Set_.ipynb`](./Python/PB_project_bioactivity_Data_Set_.ipynb)
- Fetches bioactivity data for **Acetylcholinesterase** from the [ChEMBL database](https://www.ebi.ac.uk/chembl/)
- Filters compounds with standard IC50 activity values
- Labels compounds as **active**, **inactive**, or **intermediate** based on IC50 thresholds
- Converts IC50 to **pIC50** (negative log scale) for better distribution

### 2️⃣ [`PB_project_descriptor_dataset_preparation.ipynb`](./Python/PB_project_descriptor_dataset_preparation.ipynb)
- Uses **PaDEL-Descriptor** to compute molecular fingerprints (PubChem)
- Cleans and merges descriptor data with bioactivity labels
- Prepares the final feature matrix `X` and target vector `y` (pIC50)

### 3️⃣ [`PB_project_exploratory_data_analysis.ipynb`](./Python/PB_project_exploratory_data_analysis.ipynb)
- Statistical analysis of bioactivity distribution
- **Mann-Whitney U Test** for statistical significance
- Visualization: frequency plots, scatter plots, box plots, heatmaps
- Lipinski's Rule of Five analysis (MW, LogP, NumHDonors, NumHAcceptors)

### 4️⃣ [`PB_project_regression_model_with_hypertuning.ipynb`](./Python/PB_project_regression_model_with_hypertuning.ipynb)
- Trains a **Random Forest Regressor** with hyperparameter tuning via `RandomizedSearchCV`
- Evaluates model using R², RMSE, MAE
- Saves the trained model, scaler, and feature selector as `.pkl` files

### 5️⃣ [`PB_project_regressors_comparison.ipynb`](./Python/PB_project_regressors_comparison.ipynb)
- Uses **LazyPredict** to benchmark 40+ regression models simultaneously
- Compares tuned Random Forest against all baseline regressors
- Produces a comparison table and visualization

> 🔗 **Google Colab Link** (Regressor Comparison): [Open in Colab](https://colab.research.google.com/drive/1k2YeQQvYB_rQnS_2TY7v1dq821g_MKAv?usp=sharing)

---

## 📊 Results

| Model | R² Score | RMSE | MAE |
|-------|----------|------|-----|
| Tuned Random Forest | *Best* | ✅ | ✅ |
| LazyPredict Baseline Models | Varied | — | — |

> Detailed metrics are stored in [`data/evaluation_results_tuned.pkl`](./data/evaluation_results_tuned.pkl) and the model comparison in [`data/lazy_vs_tuned_RF_test_comparison.csv`](./data/lazy_vs_tuned_RF_test_comparison.csv).

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Python 3.8+** | Core programming language |
| **Pandas / NumPy** | Data manipulation |
| **Scikit-Learn** | ML models, preprocessing, evaluation |
| **RDKit** | Cheminformatics & molecular processing |
| **PaDEL-Descriptor** | Molecular fingerprint generation |
| **LazyPredict** | Rapid multi-model benchmarking |
| **Matplotlib / Seaborn** | Data visualization |
| **ChEMBL API** | Bioactivity data source |
| **Google Colab** | Cloud notebook execution |
| **Jupyter Notebook** | Local development environment |

---

## ⚙️ Installation & Setup

### Prerequisites
- Python 3.8 or higher
- Java (required for PaDEL-Descriptor)

### 1. Clone the repository
```bash
git clone https://github.com/ashwin2023155/Drug-Discovery-Using-ML.git
cd Drug-Discovery-Using-ML
```

### 2. Install dependencies
```bash
pip install pandas numpy scikit-learn matplotlib seaborn rdkit-pypi lazypredict chembl-webresource-client
```

### 3. Run the notebooks in order
Open Jupyter Notebook or use Google Colab and run the notebooks in the sequence listed above (1 → 5).

---

## 🧪 Target: Acetylcholinesterase (AChE)

> **Acetylcholinesterase (AChE)** is an enzyme responsible for the breakdown of acetylcholine in the synaptic cleft. Inhibition of AChE leads to increased acetylcholine levels, which can help alleviate symptoms of **Alzheimer's disease**. This makes AChE an important drug target in neurological disease research.

---

## 📈 Key Concepts

- **IC50** → Half maximal inhibitory concentration (potency measure)
- **pIC50** → `-log10(IC50)`, normalized for better ML model performance
- **Lipinski's Rule of Five** → Drug-likeness filter for oral bioavailability
- **PubChem Fingerprints** → Binary vectors encoding molecular substructure presence
- **Mann-Whitney U Test** → Non-parametric statistical test for bioactivity comparison

---

## 🙏 Acknowledgements

- [ChEMBL Database](https://www.ebi.ac.uk/chembl/) — Bioactivity data source
- [PaDEL-Descriptor](http://www.yapcwsoft.com/dd/padeldescriptor/) — Molecular descriptor software
- [Data Professor (YouTube)](https://www.youtube.com/c/DataProfessor) — Tutorial inspiration
- [RDKit](https://www.rdkit.org/) — Open-source cheminformatics library

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

<div align="center">
  Made with ❤️ for computational drug discovery
</div>

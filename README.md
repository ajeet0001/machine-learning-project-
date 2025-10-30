# machine-learning-project
# 🧠 EEG-Based Mental Workload Classification using Machine Learning

## 📘 Project Overview
This project focuses on classifying **mental workload levels (Low vs. High)** using **EEG (Electroencephalogram)** signals with **machine learning algorithms**.  
By analyzing brainwave patterns during rest and mental tasks, we aim to detect cognitive load in real-time.

Applications include:
- 🧩 Cognitive ergonomics  
- 🎓 Adaptive learning systems  
- 🦾 Brain–Computer Interfaces (BCI)  
- 🚗 Fatigue monitoring in drivers/pilots  

---

## 📊 Dataset: PhysioNet EEG During Mental Arithmetic Tasks (EEGMAT)

**Dataset Link:**  
🔗 [https://physionet.org/content/eegmat/1.0.0/](https://physionet.org/content/eegmat/1.0.0/)

**Description:**
- EEG signals collected from participants during **baseline (rest)** and **mental arithmetic (task)** sessions.  
- Each subject has two `.edf` files:
  - `_1.edf` → Baseline (Low workload)
  - `_2.edf` → Task (High workload)
- Sampling rate: 128–256 Hz  
- 14–32 EEG channels (10–20 system)

---

## ⚙️ Methodology

### 1️⃣ Data Loading & Preprocessing
- Loaded `.edf` EEG files using **MNE-Python**.
- Resampled all signals to **128 Hz** for consistency.
- Applied **bandpass filter (1–45 Hz)** to remove artifacts and noise.
- Normalized features to ensure equal scaling across channels.

### 2️⃣ Feature Extraction
Extracted features from 4-second EEG windows:
- **Time-domain:** Mean, Standard Deviation, RMS  
- **Frequency-domain:** Band power in Delta, Theta, Alpha, Beta, Gamma bands (via Welch’s method)

### 3️⃣ Labeling
- Class 0 → Baseline (Low workload)  
- Class 1 → Task (High workload)

### 4️⃣ Model Training
Trained and compared 3 machine learning models:
| Algorithm | Description | Key Strength |
|------------|--------------|---------------|
| **SVM** | Finds max-margin separating boundary | Works well on small datasets |
| **Random Forest** | Ensemble of decision trees | Handles non-linearity & noise |
| **XGBoost** | Boosted trees with gradient optimization | Best accuracy & speed |

### 5️⃣ Model Evaluation
Metrics used:
- Accuracy  
- Precision, Recall, F1-score  
- AUC (Area Under ROC Curve)  
- Confusion Matrix visualization  

---

## 🧮 Results

| Model | Accuracy | AUC  | Observation |
|--------|-----------|------|--------------|
| SVM | 86.9 % | 0.93 | Missed some high workload cases |
| Random Forest | 90.6 % | 0.98 | More stable classification |
| **XGBoost** | **95.3 %** | **0.99** | Best performing model ✅ |

**Conclusion:**  
EEG features (statistical + spectral) effectively distinguish between low and high mental workload states.  
XGBoost achieved the highest overall performance.

---

## 🧠 Insights
- High workload → ↑ Beta/Gamma, ↓ Alpha band power.  
- EEG can reveal subtle brain-state changes with simple ML models.  
- Ensemble learning (Random Forest, XGBoost) is robust for EEG analysis.

---

## 🚀 How to Run the Project (Google Colab)

### Step 1. Clone the repository
```bash
!git clone https://github.com/<your-username>/EEG-Workload-Classification.git
cd EEG-Workload-Classification

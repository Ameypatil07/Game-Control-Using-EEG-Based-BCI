# Game-Control-Using-EEG-Based-BCI
Real-time EEG-based Brain-Computer Interface (BCI) system to control game actions using cognitive states like attention and relaxation

## 🧠 Project Overview

- **Type:** Non-invasive EEG-based BCI system  
- **Input:** Live EEG signals (2-channel setup)  
- **Output:** Real-time game control (e.g., accelerate and brake using only mental states)  
- **Key Model:** XGBoost classifier  
- **Hardware:** DIY Neuroscience Kit by Upside Down Labs + Arduino

---

## 🗃️ Dataset

A **custom EEG dataset** was created using real-time recordings from 5 subjects:
- 20 minutes of **attentive** mental activity (e.g., solving math problems)
- 20 minutes of **relaxed** mental activity (e.g., listening to calming music)

The raw EEG data was collected using the `collect.py` script and saved in `.csv` format.

---

## ⚙️ How It Works

### 1. **Signal Acquisition**
- Hardware: BioAmp EXG Pill + Maker UNO board
- Placement: IN+, IN, and REF electrodes based on modified 10-20 system

### 2. **Preprocessing**
- **Bandpass Filter:** 0.5–30 Hz  
- **Notch Filter:** 50 Hz  
- Removes noise, retains alpha/beta wave features

### 3. **Feature Extraction**
- Power Spectral Density (PSD): Delta, Theta, Alpha, Beta bands  
- Statistical features: Mean, Std, Skewness, Kurtosis  
- Concatenated into a single feature vector

### 4. **Model Training**
- Model: XGBoost (Best performance: **89.15% accuracy**)  
- Hyperparameter Tuning: Optuna  
- Model stored using `joblib` for real-time inference

### 5. **Real-Time Game Control**
- EEG data streamed via serial port
- `pred.py` uses live data to predict mental state every 512 samples
- **"W" key** pressed for attentive state (accelerate)  
- **"Space" key** pressed for relaxed state (brake)

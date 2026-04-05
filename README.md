# 🌍 Episode-Aware PM2.5 Forecasting

This repository contains our solution for the **AISE Hack Kaggle Competition** on **air pollution forecasting (PM2.5 prediction)**.  
The baseline model provided was **FNO2D (Fourier Neural Operator in 2D)**, which we extended with several innovations to improve accuracy, robustness, and episode-awareness.

---

## 📌 Problem Statement
Air pollution, especially **PM2.5 concentration**, poses severe health risks.  
The challenge was to forecast PM2.5 levels using atmospheric datasets, with a focus on **episode-aware forecasting** — i.e., capturing sudden spikes and pollution episodes rather than just smooth averages.

---

## ⚙️ Baseline: FNO2D
- **Fourier Neural Operator (2D)** was the starting point.
- Strengths: Efficient handling of spatio-temporal data, strong baseline for PDE-like problems.
- Limitations: Struggled with **sharp pollution episodes**, leading to underestimation during extreme events.

---

## 🚀 Innovations Introduced
We built upon FNO2D with the following changes:

### 1. **Hybrid Architectures**
- Integrated **ConvLSTM**, **SimVP**, and **PredSRNN** alongside FNO2D.
- Allowed the model to capture both **global atmospheric dynamics (FNO)** and **local temporal dependencies (RNN/ConvLSTM)**.

### 2. **Episode-Aware Loss Functions**
- Modified loss to penalize **underprediction of spikes**.
- Weighted errors more heavily during high PM2.5 episodes → improved sensitivity to extreme pollution events.

### 3. **Data Augmentation & Preprocessing**
- Normalized meteorological variables for stability.
- Added **episode tagging** (labels for high-pollution events) to guide training.
- Applied rolling-window sampling to ensure balanced representation of normal vs. episode data.

### 4. **Resource-Constrained Optimization**
- Adapted models to **Kaggle’s compute/storage limits**:
  - Reduced parameter counts without losing accuracy.
  - Efficient checkpointing and memory management.
  - Batch size tuning for GPU constraints.

---

## 📊 Results & Impact
| Model Variant         | Key Change                        | Effect |
|-----------------------|-----------------------------------|--------|
| FNO2D (baseline)      | Pure Fourier Neural Operator      | Good average accuracy, poor episode capture |
| FNO2D + ConvLSTM      | Added temporal recurrence         | Better short-term episode prediction |
| FNO2D + SimVP         | Video-prediction inspired module  | Improved spatio-temporal consistency |
| FNO2D + PredSRNN      | Sequential recurrent spatio model | Stronger episode-aware forecasting |
| Episode-Aware Loss    | Weighted spike errors             | Reduced underestimation of pollution peaks |

**Overall Impact:**  
- Episode-aware models showed **significant improvement in RMSE during high-pollution events**.  
- Hybrid approaches balanced **global dynamics** with **local temporal accuracy**.  
- Resource-optimized training ensured reproducibility within Kaggle constraints.

---

## 📂 Repository Structure
├── README.md               
├── LICENSE                         
├── notebooks/              


---

## 🧑‍💻 Contributors
- **Darshit Garg**
- **Deekshita Singh**
- **Brijeshwar Reddy.S**
- **Nishant Venkat**
- **Vansh M Rajwani**
---

## 📈 Future Work
- Explore **transformer-based spatio-temporal models** for further gains.
- Extend to **multi-pollutant forecasting** (NO2, SO2, O3).
- Deploy lightweight versions for **real-time monitoring systems**.

---

## 🔗 References
- [Fourier Neural Operator (FNO)](https://arxiv.org/abs/2010.08895)
- Kaggle Competition Dataset: Atmospheric PM2.5 Forecasting

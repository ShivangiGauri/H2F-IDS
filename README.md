# H2F-IDS: Hybrid Fusion Intrusion Detection System

A precision-first hybrid intrusion detection system designed for **zero-shot generalization** across modern network traffic datasets.

This project combines **supervised learning (Random Forest)**, **unsupervised anomaly detection (Isolation Forest)**, and a **gated decision mechanism** to achieve high recall while maintaining controlled false positive rates.

---

## 📌 Key Features

- Hybrid IDS architecture (RF + Isolation Forest + Gated Logic)
- Precision-first design (focus on minimizing false negatives)
- Strict **zero-shot evaluation** (no retraining across datasets)
- Cross-dataset testing:
  - CICIDS2017 (training)
  - CICIDS2018 (zero-shot)
  - Unified NIDS (zero-shot)
- Threshold tuning for optimal performance
- Batch inference simulation (realistic deployment scenario)

---

## 🧠 System Architecture

The system operates in three levels:

1. **Supervised Layer (Random Forest)**
   - Predicts class label and confidence score

2. **Anomaly Detection Layer (Isolation Forest)**
   - Trained only on benign traffic
   - Detects deviations from normal behavior

3. **Gated Decision Logic**
   - High confidence → accept RF prediction  
   - Low confidence → use anomaly detection + rules  

---

## ⚙️ Workflow

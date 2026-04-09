# H2F-IDS: Hybrid Fusion Intrusion Detection System

A precision-first hybrid intrusion detection system designed for **zero-shot generalization** across modern network traffic datasets.

This project combines **supervised learning (Random Forest)**, **unsupervised anomaly detection (Isolation Forest)**, and a **gated decision mechanism** to achieve high recall while maintaining controlled false positive rates.


## Key Features

- Hybrid IDS architecture (RF + Isolation Forest + Gated Logic)
- Precision-first design (focus on minimizing false negatives)
- Strict **zero-shot evaluation** (no retraining across datasets)
- Cross-dataset testing:
  - CICIDS2017 (training)
  - CICIDS2018 (zero-shot)
  - Unified NIDS (zero-shot)
- Threshold tuning for optimal performance
- Batch inference simulation (realistic deployment scenario)


## System Architecture

The system operates in three levels:

1. **Supervised Layer (Random Forest)**
   - Predicts class label and confidence score

2. **Anomaly Detection Layer (Isolation Forest)**
   - Trained only on benign traffic
   - Detects deviations from normal behavior

3. **Gated Decision Logic**
   - High confidence → accept RF prediction  
   - Low confidence → use anomaly detection + rules  


## Workflow

Data → Preprocessing → Random Forest → Confidence Check
↓                               ↓
Feature Selection            High Confidence → Final Output
↓
Low Confidence → Isolation Forest → Final Decision


## Datasets Used

| Dataset       | Purpose             |
|---------------|---------------------|
| CICIDS2017    | Training + Testing  |
| CICIDS2018    | Zero-shot Testing   |
| Unified NIDS  | Zero-shot Testing   |


## Evaluation Metrics

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion Matrix

> Special focus: Minimizing **False Negatives (FN)** while controlling **False Positives (FP)**


## Key Results

- High recall (>99%) on training dataset  
- Strong generalization under zero-shot conditions  
- Recovery of up to **93.7% missed attacks** using hybrid logic  
- **False Positive Rate maintained around ~1.1%**  
- Stable performance across dataset shifts  

## Comparative Analysis

The proposed H2F-IDS system is evaluated against individual models to highlight the benefits of hybrid fusion.

| Model               | Precision | Recall | F1 Score | Key Observation |
|--------------------|----------|--------|----------|----------------|
| Random Forest      | High     | Very High | High  | Strong baseline performance |
| Isolation Forest   | Moderate | Low     | Low      | High false positives, weak standalone detection |
| Hybrid (H2F-IDS)   | High     | Very High | Best Balance | Improved detection with controlled false positives |

**Key Insight:**  
The hybrid system significantly improves detection performance by recovering missed attacks from the Random Forest while avoiding the instability of standalone anomaly detection.


## Ultra-Low False Positive Rate (FPR)

One of the primary design goals of H2F-IDS is to maintain a **low false positive rate while maximizing attack detection**.

- False Positive Rate (FPR) ≈ **1.1%** on CICIDS2017  
- Controlled increase under zero-shot evaluation  
- Gated logic prevents unnecessary anomaly-triggered alerts  

### Why This Matters

In real-world Security Operations Centers (SOC):
- High FPR → alert fatigue  
- Low FPR → better trust and usability  

The H2F-IDS system achieves a **balanced trade-off**, ensuring:
- Minimal missed attacks (low FN)  
- Manageable alert volume (low FP)  

This makes the system suitable for **practical deployment scenarios**.

## Threshold Tuning

| Threshold | Precision | Recall    | F1 Score     | FPR      |
|-----------|-----------|-----------|--------------|----------|
| 0.3       | High      | Very High | High         | Higher   |
| 0.4       | Balanced  | High      | High         | Moderate |
| 0.5       | Optimal   | High      | Best Balance | Low      |

Final chosen threshold: **0.5**


## Batch Inference Performance

- 10,000 flows processed
- Low false negatives
- Manageable false positives
- CPU-based execution
- Realistic deployment simulation


## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/your-username/H2F-IDS.git
cd H2F-IDS
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the notebook

```bash
jupyter notebook notebooks/H2F_IDS.ipynb
```


## Requirements

- Python 3.8+
- scikit-learn
- pandas
- numpy
- matplotlib
- seaborn

## Limitations

- Focuses on binary classification (benign vs attack)
- Uses flow-based features (no packet-level inspection)
- Limited adversarial robustness analysis
- Classical ML models (no deep learning integration)

## Future Work

- Multi-class attack classification
- Real-time deployment
- Deep learning integration (CNN, LSTM, Transformers)
- Adversarial robustness testing
- Cross-domain generalization improvements

## License

This project is for academic and research purposes.

# 📧 NLP Phishing Email Detection

Detecting phishing emails using Natural Language Processing (NLP) and Deep Learning. Unlike traditional spam filters that rely on keyword frequency, this system analyzes the **intent and meaning** of emails — detecting impersonation, urgency tactics, and suspicious patterns.

---

## 👥 Team
- Max 2 students per project
- Deadline: 15 May 2026

---

## 📌 Problem Statement

Phishing emails are a major cybersecurity threat. They are designed to look legitimate and manipulate users into revealing sensitive information such as passwords or financial data. This project builds an intelligent system that classifies emails as **Phishing** or **Safe** using NLP and deep learning techniques.

---

## 📂 Project Structure

```
NLP_phishing_email_filtering/
├── data/               → Dataset not pushed (too large). See download link below.
├── notebooks/          → Main Colab notebook (phishing_detection_complete_bgd.ipynb)
├── models/             → Saved tokenizer and LR pipeline
│                         (LSTM model excluded due to GitHub 25MB file limit)
├── results/            → All evaluation plots and charts
└── README.md
```

---

## 📊 Dataset

- **Source:** Kaggle — [Phishing Email Detection by subhajournal](https://www.kaggle.com/datasets/subhajournal/phishingemails)
- **Size:** ~18,600 emails
- **Labels:** Binary — `Phishing Email` / `Safe Email`
- **Split:** 80% training / 20% testing (stratified)

> Dataset is not included in the repo due to large file size. Download from the link above and place as `Phishing_Email.csv` in the `/data` folder or upload directly in Colab.

---

## ⚙️ Methodology

### 1. Preprocessing
- Lowercasing
- URL replacement (replaced with token `url`)
- HTML tag removal
- Symbol and number removal
- Whitespace normalization

### 2. Feature Engineering
Six hand-crafted features extracted per email:
| Feature | Description |
|---|---|
| `url_count` | Number of URLs in the email |
| `email_length` | Total character count |
| `urgency_count` | Count of urgency keywords (e.g. "click here", "verify", "suspend") |
| `html_tags` | Number of HTML tags present |
| `exclamations` | Number of exclamation marks |
| `dollar_signs` | Number of dollar signs |

### 3. Models Trained

| Model | Type | Accuracy |
|---|---|---|
| Naive Bayes | Baseline (TF-IDF) | 96.16% |
| Logistic Regression | Baseline (TF-IDF) | 96.73% |
| **Bidirectional LSTM** | **Deep Learning** | **97.16%** |

The Bidirectional LSTM is the main model, chosen as it reads email text both forwards and backwards — capturing context that simpler models miss.

---

## 📈 Results

### Confusion Matrix (LSTM)
- **True Positives:** 1,446 phishing correctly detected
- **True Negatives:** 2,175 safe emails correctly classified
- **False Negatives:** Only 16 phishing emails missed
- **False Positives:** 90 safe emails wrongly flagged

### Classification Report (LSTM)
| Class | Precision | Recall | F1-Score |
|---|---|---|---|
| Safe Email | 0.99 | 0.96 | 0.98 |
| Phishing Email | 0.94 | 0.99 | 0.96 |
| **Overall Accuracy** | | | **97.16%** |

### Key Finding — Feature Importance
Top words signaling **PHISHING**: `your`, `http`, `click here`, `free`, `money`, `verify`, `viagra`

Top words signaling **SAFE**: `enron`, `wrote`, `thanks`, `university`, `linguistics`

---

## 🗂️ Saved Files

| File | Description |
|---|---|
| `tokenizer.pkl` | Fitted Keras tokenizer for text sequences |
| `lr_pipeline.pkl` | Trained Logistic Regression + TF-IDF pipeline |
| `lstm_phishing_model.keras` | Trained LSTM model *(not pushed — too large. Run notebook to regenerate)* |

---

## 🚀 How to Run

1. Open `notebooks/phishing_detection_complete_bgd.ipynb` in [Google Colab](https://colab.research.google.com)
2. Run the upload cell and select your `Phishing_Email.csv` file
3. Go to `Runtime` → `Run all`
4. For faster training: `Runtime` → `Change runtime type` → **T4 GPU**

---

## 📦 Requirements

All libraries are pre-installed in Google Colab. For local use:

```
tensorflow
pandas
numpy
scikit-learn
matplotlib
seaborn
```

---

## 📉 Evaluation Plots

All plots are saved in the `/results` folder:
- `class_distribution.png` — Phishing vs Safe email counts
- `feature_comparison.png` — Engineered features comparison
- `training_history.png` — LSTM accuracy and loss curves
- `confusion_matrix.png` — LSTM confusion matrix
- `model_comparison.png` — All 3 models compared
- `feature_importance.png` — Top words driving predictions

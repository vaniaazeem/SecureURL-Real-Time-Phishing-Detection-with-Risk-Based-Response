# SecureURL: Explainable Phishing vs Legitimate URL Classifier with SOC Workflow

> A lightweight, explainable machine learning tool for classifying phishing URLs, built with SOC-style risk scoring and triage logging.

---

## Overview

**SecureURL** is a 2-class URL classification project that identifies whether a given URL is **phishing** or **legitimate** using traditional machine learning techniques. Designed with cybersecurity operations in mind, this tool offers:

* Real-time URL classification
* Risk-based scoring
* Actionable response suggestions
* Explainability without SHAP
* SOC-friendly logging and triage support

It uses a **TF-IDF + SGDClassifier (log loss)** pipeline and is intended for use in research labs, training environments, SOC simulations, or lightweight threat detection systems.

---

## Features

* Binary classification: Phishing vs Legitimate
* Character-level TF-IDF vectorizer for URL features
* Explainability: Highlights top influencing tokens for each prediction
* SOC Workflow Simulation:

  * Risk scoring (Informational, Low, Medium, High)
  * Recommended actions (Allow, Block, Quarantine, Review)
  * CSV logs for predictions and analyst triage
* Interactive URL testing
* Lightweight and fast: No deep learning, no SHAP/LIME required

---

## Model Architecture

* **Vectorizer**: `TfidfVectorizer(analyzer='char_wb', ngram_range=(2,6))`
* **Classifier**: `SGDClassifier(loss='log_loss', class_weight='balanced')`
* **Explainability**: Based on model coefficients (most influential n-grams)

---

## File Structure

| File/Folder               | Description                                 |
| ------------------------- | ------------------------------------------- |
| `phish_legit_model.pkl`   | Trained model file                          |
| `label_encoder.pkl`       | Label encoder for mapping class names       |
| `url_predictions_log.csv` | Log of all predictions made during runtime  |
| `triage_review.csv`       | SOC-style triage file for analyst follow-up |
| `colab_notebook.ipynb`    | Full Google Colab implementation            |

---

## Example Output

```
Enter a URL: secure-login.paypa1.com

Predicted: Phishing (confidence: 94.23%)
Risk: High
Action: Block, alert user, hunt IOCs

Top Indicators Toward 'Phishing':
  + login  (0.3241)
  + secure  (0.3123)
  + .com  (0.2897)

Counter-signals:
  - paypal (-0.1342)
```

---

## Usage (Google Colab)

1. Clone this repository or open the notebook in Google Colab.
2. Upload a labeled CSV dataset (with columns like `url`, `label`).
3. Train the model using the notebook cells.
4. Use the interactive prompt to classify URLs.
5. View saved predictions in `url_predictions_log.csv` and `triage_review.csv`.

---

## Dataset Format

You can upload your own dataset with the following structure:

| url                                                          | label      |
| ------------------------------------------------------------ | ---------- |
| [http://secure-update.com](http://secure-update.com)         | phishing   |
| [https://www.google.com](https://www.google.com)             | legitimate |
| [http://paypal.login-check.ru](http://paypal.login-check.ru) | phishing   |

Column names are case-insensitive and auto-detected.

---

## Requirements

These are automatically installed in Colab:

* `scikit-learn`
* `seaborn`
* `matplotlib`
* `pandas`
* `numpy`

---

## Ideal For

* Cybersecurity students and researchers
* SOC analysts-in-training
* CTF challenge developers
* ML enthusiasts exploring security applications
* Lightweight detection integrations

---

## Disclaimer

This project is for educational and research purposes only. Do not use it for malicious purposes. Ensure ethical practices when testing live URLs or deploying in production environments.

---

## Contact

For questions or collaboration, feel free to open an issue or connect via GitHub.

---

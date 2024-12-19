
# **Decoding Emotions: A Multi-Approach Sentiment Classification of Tweets**

## **Overview**
This project aims to classify tweets based on their sentiment, identifying whether they convey positive :) or negative :( emotions. Multiple approaches were explored, from traditional methods using TF-IDF and GloVe embeddings to more advanced methods like FastText and transformer-based architectures, including DistilBERT and RoBERTa.

The project includes hyperparameter tuning using **Optuna**, efficient model training on large datasets, and a systematic approach to evaluating performance.

---

## **Repository Structure**

```
├── data/                     # Directory for dataset files
│   ├── train_pos.txt         # Positive sentiment tweets (small dataset)
│   ├── train_neg.txt         # Negative sentiment tweets (small dataset)
│   ├── train_pos_full.txt    # Positive sentiment tweets (full dataset)
│   ├── train_neg_full.txt    # Negative sentiment tweets (full dataset)
│   ├── test_data.txt         # Test dataset
├── notebooks/                # Jupyter notebooks for analysis
│   ├── EDA.ipynb             # Exploratory Data Analysis notebook
│   ├── Ethical_Risk.ipynb    # Ethical risk analysis notebook
├── src/                      # Source code for model training and evaluation
│   ├── preprocess.py         # Preprocessing scripts
│   ├── train.py              # Training scripts
│   ├── evaluate.py           # Evaluation scripts
├── fasttext_train_full.txt   # FastText training data (full dataset)
├── fasttext_train_optuna.txt # FastText training data (Optuna-tuned)
├── submission.csv            # Final submission file
├── run.py                    # Main script to run the project
├── requirements.txt          # Python dependencies
```

---

## **Models and Methods**

### **1. TF-IDF + Logistic Regression**
- **Features**: Used TF-IDF vectors with n-grams (up to bigrams or trigrams) as features.
- **Classifier**: Trained a Logistic Regression model with GridSearchCV for hyperparameter tuning.
- **Validation Accuracy**: Achieved **82.1%**.

### **2. GloVe + Logistic Regression**
- **Features**: Pre-trained GloVe embeddings (100-dimensional) were used to represent tweets as averaged word embeddings.
- **Classifier**: Trained Logistic Regression with hyperparameter tuning.
- **Validation Accuracy**: Achieved **83.0%**.

### **3. FastText**
- **Model**: FastText, a subword-based text classifier, was tuned using Optuna to optimize hyperparameters like learning rate, number of epochs, and word n-grams.
- **Hyperparameter Tuning**:
  - Learning Rate: 0.0109
  - Epochs: 10
  - Word N-grams: 3
  - Embedding Dimensions: 100
  - Loss Function: Negative Sampling (NS)
- **Validation Accuracy**: Achieved **83.9%**.
- **Best F1 Score**: **84.0%**.

### **4. DistilBERT**
- **Model**: Pre-trained DistilBERT (`distilbert-base-uncased`), fine-tuned for sentiment classification.
- **Hyperparameter Tuning**:
  - Learning Rate: $2 \times 10^{-5}$
  - Batch Size: 16
  - Number of Epochs: 5
  - Weight Decay: 0.01
- **Validation Accuracy**: Achieved **88.7%**.
- **Best F1 Score**: **88.9%**.

### **5. RoBERTa**
- **Model**: Pre-trained RoBERTa (`roberta-base`), fine-tuned for sentiment classification.
- **Validation Accuracy**: Achieved **88.4%**.
- **Best F1 Score**: **88.7%**.

---

## **Installation**

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/sentiment-classification.git
   cd sentiment-classification
   ```

2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Download and place the dataset files in the `data/` directory.

---

## **Usage**

### **Training and Evaluation**
The `run.py` script provides a unified interface to train and evaluate models.

1. Choose the desired method in the `method` variable (`glove`, `tfidf`, `fasttext`, `distilbert`, or `roberta`).
2. Execute the script:
   ```bash
   python run.py
   ```

### **Preprocessing**
The `src/preprocess.py` script includes utility functions for:
- Removing irrelevant tokens like URLs, mentions, and placeholders.
- Converting tweets to GloVe embeddings or TF-IDF features.

### **Evaluation**
The `src/evaluate.py` script evaluates models on validation data and predicts sentiment labels for the test dataset.

### **Hyperparameter Tuning**
The project leverages **Optuna** for efficient hyperparameter optimization. Adjust the number of trials and search spaces in `src/train.py`.

---

## **Results**

| **Model**        | **Validation Accuracy** | **Validation F1 Score** | **Submission ID** |
|-------------------|--------------------------|--------------------------|--------------------|
| Logistic Regression (TF-IDF) | 82.1%                   | 82.3%                   | 277001             |
| Logistic Regression (GloVe)  | 83.0%                   | 83.2%                   | 276950             |
| FastText         | 83.9%                   | 84.0%                   | 276771             |
| DistilBERT       | 88.7%                   | 88.9%                   | 277867             |
| RoBERTa          | 88.4%                   | 88.7%                   | 277552             |

---

## **Ethical Concerns**

1. **Contextual Misclassification**: Sarcasm and irony, such as "Oh great, everything's ruined :)," may lead to incorrect predictions.
2. **Bias Mitigation**:
   - Incorporated **DistilBERT** to capture context better.
   - Evaluated performance on ambiguous examples.

---

## **Contributors**
- **Bakiri Ayman**
- **Ben Mohamed Nizar**
- **Chahed Ouazzani Adam**


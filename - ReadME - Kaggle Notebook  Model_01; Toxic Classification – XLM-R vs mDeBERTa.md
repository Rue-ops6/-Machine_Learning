# to HTML this jupitar; https://nbviewer.org/

**🛡️ AI for Digital Safety — Toxicity Classification

 ```python–``` Solution
**
Model:

- XLM-RoBERTa / mDeBERTa (choose your best model)

How to run:

1. Install requirements:
   pip install transformers torch scikit-learn pandas numpy

2. Run notebook or script:
   main.ipynb OR main.py

3. Output:
   submission.csv will be generated

Preprocessing:

- Tokenization with HuggingFace tokenizer
- Max length = 64
- Train/validaation split = 90/10

Training:

- Trainer API (PyTorch backend)
- Epochs = 1
- Batch size = 4
- Batch size = 4

                                          ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

📌 Overview

This project implements a multi-class text classification system to detect harmful or unsafe language. It was developed for the AI for Digital Safety Datathon 2026.

The pipeline compares two transformer models:

XLM-RoBERTa — multilingual baseline
mDeBERTa-v3 — enhanced contextual understanding

The objective is to maximise macro F1-score, ensuring balanced performance across all classes.

🧠 Problem Definition

Given a dataset of text samples, classify each into:

Label ID Class
0 Toxic
1 Mid
2 Neutral
⚙️ How to Run

1. Install requirements
pip install transformers torch scikit-learn pandas numpy
2. Run the project
main.ipynb

# or

main.py
3. Output
submission.csv
🧹 Preprocessing
HuggingFace tokenization
Max sequence length: 64
Train/validation split: 90 / 10 (stratified)
🏗️ Pipeline Architecture

1. Data Preparation
Stratified split to preserve label distribution
train_test_split(..., stratify=train["y"])
2. Tokenization

Separate tokenizers per model:

xlm-roberta-base
microsoft/mdeberta-v3-base

Settings:

Padding: max_length
Truncation: enabled
Max length: 64
3. Custom Dataset

PyTorch dataset wrapper:

Converts inputs to tensors
Ensures label–input alignment via assertion
4. Handling Class Imbalance
compute_class_weight(class_weight="balanced")

✔ Applied inside loss function to prevent bias

1. Custom Trainer (Core Feature)

Custom HuggingFace Trainer:

loss = CrossEntropyLoss(
    weight=class_weights,
    label_smoothing=0.1
)

✔ Benefits:

Reduces overconfidence
Improves generalisation
Stabilises training
6. Training Configuration
Parameter Value
Learning Rate 3e-5
Scheduler Cosine
Warmup Steps 500
Batch Size 4
Gradient Accumulation 8
Epochs 1
Weight Decay 0.01
Precision BF16

✔ Optimised for Kaggle Tesla T4

📊 Evaluation

Metric: Macro F1 Score

Why:

Handles imbalance
Treats all classes equally
🏁 Training
trainer_xlmr = train_model(...)
trainer_mdeberta = train_model(...)
📊 Model Selection

Best model selected based on:

Highest validation F1 score

Output:

🏆 Best model: <XLM-R or mDeBERTa>
🔥 Best F1: XXXX
🔮 Prediction Pipeline
Uses best-performing model
Runs inference on test set
Converts logits → class labels
📁 Outputs

1. Human-readable predictions
predictions.xlsx

Contains:

Text
Predicted ID
Predicted label
2. Kaggle submission
submission.csv

Format:

y_pred
🚀 Submission
kaggle competitions submit \
-c her-will-ai-for-digital-safety-datathon-2026 \
-f submission.csv \
-m "baseline mDeBERTa (F1 ~0.48)"
🧪 Environment
Python 3.14
PyTorch (CUDA)
Transformers
Scikit-learn
NumPy / Pandas

GPU: NVIDIA Tesla T4

💡 Key Strengths
Dual-model comparison
Class imbalance handling
Label smoothing integration
Efficient GPU training
Modular pipeline
Kaggle-ready outputs
🔧 Future Improvements
Hyperparameter tuning (Optuna)
Longer training (≥3 epochs)
Larger sequence length (128–256)
Model ensembling
Data augmentation
Cross-validation
👩‍💻 Author
⠀⠀⠀⣤⣤⣀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀     ⠀⣀⣤⣤⠀⠀⠀
⠀⠀⢸⣿⣿⣿⣿⣦⣀⣀⣤⣤⣤⣤⣤⣤⣄⣠⣶⣿⣿⣿⣿⡇⠀⠀
⠀⠀⢸⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⠀⠀
⠀⠀⣤⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣦⠀⠀
⠀⣼⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣧⠀
⢠⣿⣿⣿⣿⣿⠿⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠛⠿⣿⣿⣿⣿⣿⡄
⢸⣿⣿⣿⡟⠁⠀⢀⡀⠀⠀⠀⠀⠀⠀⠀⠀⢀⡀⠀⠈⢻⣿⣿⣿⡇
⠘⣿⣿⣿⡇⠀⢠⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⡄⠀⢸⣿⣿⣿⠃
⠀⢿⣿⣿⡇⠀⠀⠛⠟⠀⠀⠀⠀⠀⠀⠀⠀⠻⠛⠀⠀⢸⣿⣿⡟⠀
⠀⠀⠻⣿⣿⣆⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣠⣾⣿⠟⠀⠀
⠀⠀⠀⠀⠙⠛⠿⣷⣶⣤⣤⣤⣤⣤⣤⣤⣤⣴⣶⠿⠛⠋⠀⠀⠀⠀   ~ Rue | GitHub-ish cat

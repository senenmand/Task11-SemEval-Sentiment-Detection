# 🎭 SemEval Task 11: Bridging the Gap in Text-Based Emotion Detection

## 📖 Overview

This project addresses **Task 11 of SemEval: Bridging the Gap in Text-Based Emotion Detection**.

The challenge is divided into three subtasks:

### Track 1 — Multi-label Emotion Detection

Predict one or more emotions expressed in a text.

### Track 2 — Emotion Intensity Prediction

Estimate the intensity of the emotions present in a text.

### Track 3 — Cross-lingual Emotion Detection

Detect emotions across different languages.

Due to the limited time available for the competition, this project focuses exclusively on **Track 1: Multi-label Emotion Detection**.

Each text can be assigned one or more of the following emotions:

* 😊 Joy
* 😢 Sadness
* 😲 Surprise
* 😨 Fear
* 😡 Anger

---

# 🏗️ Methodology

The proposed solution is based on **TFDistilBERT**, combining contextual Transformer embeddings with additional TF-IDF features.

Several architectures and training strategies were evaluated to determine the most effective approach for multi-label emotion classification.

---

# 🔬 Experiments

## Experiment 1 — Baseline

Standard TFDistilBERT architecture using TF-IDF features.

---

## Experiment 2 — Without TF-IDF

Evaluates the contribution of handcrafted TF-IDF features by removing them from the architecture.

---

## Experiment 3 — Focal Loss

Replaces Binary Cross-Entropy with Focal Loss to address class imbalance and improve learning on difficult samples.

---

## Experiment 4 — Class Weights

Introduces class weights during training to compensate for imbalanced emotion distributions.

---

## Experiment 5 — Attention Layer

Modifies the baseline architecture by incorporating an attention mechanism over token embeddings.

---

## Experiment 6 — Multi-Head Attention

Introduces a Multi-Head Self-Attention layer on top of DistilBERT outputs.

---

## Experiment 7 — Multi-Head Attention + Class Weights

Combines Multi-Head Attention with class weighting.

---

## Experiment 8 — Multi-Head Attention + Focal Loss

Combines Multi-Head Attention with Focal Loss.

---

# 📊 Experimental Results

## Overall Comparison

| Experiment                           | Label Accuracy | Precision  | Recall     | Macro F1   |
| ------------------------------------ | -------------- | ---------- | ---------- | ---------- |
| Baseline                             | 80.35%         | 80.05%     | 48.03%     | 56.81%     |
| Without TF-IDF                       | 80.87%         | 72.50%     | 60.82%     | 64.96%     |
| Focal Loss                           | —              | 85.00%     | 42.00%     | 56.00%     |
| Class Weights                        | 81.74%         | 72.27%     | 67.42%     | **68.15%** |
| Attention Layer                      | **83.83%**     | 81.73%     | 56.61%     | 65.54%     |
| Multi-Head Attention                 | 83.48%         | 83.38%     | 59.53%     | 67.51%     |
| Multi-Head Attention + Class Weights | 77.91%         | 63.09%     | **72.64%** | 64.75%     |
| Multi-Head Attention + Focal Loss    | 79.83%         | **84.71%** | 40.52%     | 53.48%     |

---

# 🏆 Best Models

## Best Overall Performance

### 🥇 Experiment 4 — Class Weights

| Metric         | Value      |
| -------------- | ---------- |
| Macro F1       | **68.15%** |
| Precision      | 72.27%     |
| Recall         | 67.42%     |
| Label Accuracy | 81.74%     |

This experiment achieved the highest Macro F1 score while maintaining a strong balance between precision and recall across all emotion categories.

---

## Best Precision

### 🥈 Experiment 6 — Multi-Head Attention

| Metric    | Value      |
| --------- | ---------- |
| Precision | **83.38%** |
| Macro F1  | 67.51%     |
| Recall    | 59.53%     |

This architecture produces fewer false positives while maintaining competitive overall performance.

---

## Best Recall

### 🥉 Experiment 7 — Multi-Head Attention + Class Weights

| Metric    | Value      |
| --------- | ---------- |
| Recall    | **72.64%** |
| Precision | 63.09%     |
| Macro F1  | 64.75%     |

Suitable for applications where missing emotional signals is more critical than generating false positives.

---

## Highest Label Accuracy

### 🏅 Experiment 5 — Attention Layer

| Metric         | Value      |
| -------------- | ---------- |
| Label Accuracy | **83.83%** |
| Macro F1       | 65.54%     |

This model achieved the highest label-level accuracy among all experiments.

---

# 📈 Per-Class Performance Analysis

## Fear

Fear is the most stable emotion across all experiments.

F1 scores consistently range between:

* 0.63 and 0.75

This suggests that fear-related linguistic patterns are easier for the models to identify.

---

## Anger

Anger is the most challenging emotion due to the limited number of training examples.

Recall varies significantly:

* 31% → 88%

Performance is highly sensitive to architectural and training modifications.

---

## Sadness

Sadness exhibits substantial variability across experiments:

| Experiment | Recall |
| ---------- | ------ |
| 3          | 26%    |
| 4          | 71%    |
| 6          | 76%    |
| 7          | 82%    |

This indicates that sadness detection benefits considerably from architecture design choices.

---

## Joy

Joy demonstrates relatively stable performance across experiments, typically achieving:

* F1 ≈ 0.64–0.67

---

## Surprise

Surprise remains one of the most difficult emotions to classify accurately.

F1 scores generally range between:

* 0.48 and 0.67

Future improvements could focus on reducing confusion between surprise and other emotions.

---

# 🎯 Conclusions

The experiments reveal a clear trade-off between **precision** and **recall** in multi-label emotion classification.

Key findings include:

* Removing TF-IDF features improved recall considerably.
* Focal Loss increased precision but severely reduced recall.
* Class weighting provided the best balance between precision and recall.
* Multi-Head Attention significantly improved precision while maintaining strong overall performance.
* Combining Multi-Head Attention with Class Weights maximized recall but introduced more false positives.

Overall, **Experiment 4 (Class Weights)** achieved the best balance between precision and recall and obtained the highest Macro F1 score, making it the most suitable model for deployment.

---

# 🚀 Technologies

* Python
* TensorFlow
* Hugging Face Transformers
* DistilBERT
* Scikit-Learn
* TF-IDF
* Gradio

---

# 📚 References

* SemEval Task 11: Bridging the Gap in Text-Based Emotion Detection
* DistilBERT: A distilled version of BERT
* Hugging Face Transformers
* TensorFlow

# Cross-Domain Opinion Mining — BERT Fine-Tuning & NLP

**Program:** MSc Data Science & Business Analytics — Bologna Business School  
**Team:** Team 4  
**Supervisors:** Prof. Gianluca Moro & Dr. Giacomo Frisoni — DISI, University of Bologna  
**Dataset:** Amazon Gift Cards Reviews + Amazon Magazine Subscription Reviews (~150K reviews)

---

## Overview

This project investigates **cross-domain opinion mining** — the challenge of training a sentiment classifier in one product domain and deploying it accurately in a completely different domain. Using Amazon review datasets, the project benchmarks classical NLP approaches against transformer-based models (BERT), with a focus on domain transfer robustness.

The core research question: *Can a fine-tuned BERT model generalize sentiment analysis across product domains where vocabulary, style, and context differ significantly?*

---

## Business Problem

Sentiment analysis systems trained on one domain (e.g., electronics reviews) often fail when applied to another domain (e.g., insurance feedback, financial reports). This is a critical limitation for enterprise NLP pipelines. This project explores whether fine-tuned transformers offer a viable path to domain-agnostic opinion mining.

---

## Dataset

Two Amazon review domains were used for cross-domain evaluation:

| Domain | Source | Volume |
|---|---|---|
| **Gift Cards** | Amazon Gift Card product reviews | ~75K reviews |
| **Magazines** | Amazon Magazine Subscription reviews | ~75K reviews |

Reviews were pre-processed for:
- Tokenization & lowercasing
- Stopword removal (classical pipeline)
- Subword tokenization via BERT WordPiece tokenizer (transformer pipeline)
- Label binarization: positive (≥4 stars) vs negative (≤2 stars)

---

## Models Benchmarked

Three approaches were systematically compared:

### 1. TF-IDF + Logistic Regression (Classical Baseline)
- TF-IDF vectorization (unigrams + bigrams, max_features=50,000)
- L2-regularized Logistic Regression classifier
- Fast, interpretable, no transfer learning

### 2. Frozen BERT (Feature Extractor)
- Pre-trained `bert-base-uncased` loaded from HuggingFace Transformers
- BERT weights frozen — used as static feature extractor
- Only the classification head trained on task data
- Tests whether pre-trained BERT representations transfer without fine-tuning

### 3. Fine-Tuned BERT (Full Training)
- End-to-end fine-tuning of `bert-base-uncased` on task data
- All BERT layers unfrozen and updated during training
- Optimized with AdamW, linear learning rate warmup scheduler
- Best-performing configuration

---

## Experiment Tracking — Weights & Biases

All experiments tracked in WandB:  
🔗 [wandb.ai/sukhdeepsinghsaini-bologna-business-school/cross-domain-opinion-mining](https://wandb.ai/sukhdeepsinghsaini-bologna-business-school/cross-domain-opinion-mining)

Tracked metrics per run:
- Training & validation loss curves
- Accuracy, Precision, Recall, F1 per epoch
- Hyperparameter configurations (learning rate, batch size, warmup steps, max sequence length)
- WandB Sweeps used for hyperparameter optimization

---

## Results

| Model | In-Domain Accuracy | Cross-Domain Accuracy |
|---|---|---|
| TF-IDF + LR | ~88% | ~74% |
| Frozen BERT | ~85% | ~79% |
| **Fine-Tuned BERT** | **92.15%** | **~87%** |

Fine-tuned BERT achieved **92.15% accuracy** and demonstrated substantially better cross-domain generalization compared to both the classical baseline and the feature-extraction approach. The performance gap between frozen and fine-tuned BERT underscores the importance of task-specific adaptation.

---

## Key Findings

- Fine-tuning BERT on the source domain and evaluating on the target domain shows strong transfer — the model learns generalizable sentiment representations, not domain-specific surface patterns
- TF-IDF + LR degrades sharply on cross-domain tasks due to vocabulary mismatch
- BERT's attention mechanism captures semantic sentiment signals that transfer across domains
- WandB hyperparameter sweeps identified optimal config: LR=2e-5, batch_size=32, max_seq_len=128, warmup_ratio=0.1

---

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.x |
| Deep Learning | PyTorch, HuggingFace Transformers |
| Pre-trained Model | `bert-base-uncased` |
| Classical NLP | Scikit-learn (TF-IDF, LogReg) |
| Experiment Tracking | Weights & Biases (WandB) |
| Data Processing | Pandas, NumPy, NLTK |
| Visualization | Matplotlib, Seaborn |

---

## Files

```
NLP_Opinion_Mining/
├── WandB_BERT_Opinion_Mining.ipynb    # Full analysis & training notebook
└── README.md
```

---

## Academic Context

**Course:** Natural Language Processing & Text Analytics  
**School:** Bologna Business School — MSc Data Science & Business Analytics  
**Academic Supervision:** Prof. Gianluca Moro & Dr. Giacomo Frisoni — Department of Computer Science and Engineering (DISI), University of Bologna  
**WandB Project:** [cross-domain-opinion-mining](https://wandb.ai/sukhdeepsinghsaini-bologna-business-school/cross-domain-opinion-mining)

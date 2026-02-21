# Step 2b: Training and Evaluation

## Overview

Uses **80% of train-v2.0.json** (random split, seed=42) for training and **20%** for held-out evaluation. Model: `deepset/roberta-base-squad2`.

## How to Run

### Full training (80% of 130k questions)

```bash
pip install -r requirements.txt
python train_step2b.py
```

### Quick validation (5k samples, ~55 min)

```bash
python train_step2b.py --quick
```

## Outputs

- **Model saved to:** `step2b_output/model/`
- **Metrics saved to:** `step2b_output/metrics.json`
- **Console:** KPI summary printed at the end

## Evaluation Metrics (KPIs)

### KPI 1: Correctly answering when answerable

| Metric | Description |
|--------|-------------|
| **Exact Match (EM)** | % of answerable questions with exact string match |
| **F1** | Token-overlap F1 score on answerable questions |

*Higher is better – we want correct answers when the context contains them.*

### KPI 2: Abstention when unanswerable

| Metric | Description |
|--------|-------------|
| **Recall** | Of unanswerable questions, % we correctly abstained ("I don't have the answer") |
| **Precision** | Of all abstentions, % that were correct (question was actually unanswerable) |

*Higher recall = fewer false positives (fewer wrong answers on unanswerable Qs).*

## Example Output

```
==================================================
STEP 2B EVALUATION METRICS
==================================================

KPI 1: Correctly answering when answerable (n=...)
  Exact Match:     XX.XX%
  F1:              XX.XX%

KPI 2: Abstention when unanswerable (n=...)
  Recall:          XX.XX% (abstained correctly)
  Precision:       XX.XX% (abstentions that were correct)
==================================================
```

## Data Split

- **Random seed:** 42
- **Split:** 80% train / 20% eval
- **Train size:** ~104,255 questions
- **Eval size:** ~26,064 questions

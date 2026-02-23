# Conversational AI for SQuAD

A conversational AI agent that answers questions from the [SQuAD 2.0](https://rajpurkar.github.io/SQuAD-explorer/) dataset, with a strong emphasis on **reducing false positives** by saying *"I don't have the answer"* when no answer is available.

> **Design principle:** It is more important to not give the wrong answer than it is to give the answer.

---

## Approach

This project follows a three-step iterative workflow:

### Step 1: Understand the Dataset
- Preview the train-v2 data structure
- Calculate the percentage of questions that have answers vs. no answer

### Step 2: Iterative Training
- Train the model and tune weights
- Optimize for abstention on unanswerable questions

### Step 3: Evaluation
- Evaluate against the dev-v2 file
- Measure performance with focus on minimizing false positives

---

## Step 2b: Initial Training Results

Using `deepset/roberta-base-squad2` fine-tuned on **350 training examples** with a small held-out set:

- **Answerable questions (n = 65)**
  - **Exact Match / Accuracy**: ~69.2%
  - **F1 score**: ~83.3%
- **Unanswerable questions (n = 35)**
  - **Abstain recall** (correctly said “I don’t know”): ~85.7%
  - **Abstain precision** (when it abstained, it was right): ~93.8%

These early results show the model is already strongly biased toward **safe abstention** on unanswerable questions while still answering a majority of answerable questions correctly.

---

## Dataset

Uses **SQuAD 2.0** (`train-v2.0.json`, `dev-v2.0.json`):
- Reading comprehension with unanswerable (adversarial) questions
- Each question has `is_impossible: true` (no answer) or `false` (answerable)

---

## Results

==================================================
STEP 2B EVALUATION METRICS
==================================================

KPI 1: Correctly answering when answerable (n=65)
  Exact Match:     69.23%
  F1:              83.26%

KPI 2: Abstention when unanswerable (n=35)
  Recall:          85.71% (abstained correctly)
  Precision:       93.75% (abstentions that were correct)

---

## Repository

[github.com/RujutaGandhi/ConversationalAI_SQUAD](https://github.com/RujutaGandhi/ConversationalAI_SQUAD)

---

## Key Learnings

The purpose of this exercise was exposure to Cursor and conversational AI. Through this, I learned a few key lessons:
1. Plan for token use in advance: Since I am using the free version of Cursor, I am limited to what I can run. I will include token usage limitations in the prompt in the future.
2. Plan for memory usage: Since I am using my local machine, there are limits to running the full dataset on my machine. For this analysis, I limited to just 350 examples and another 87 for the holdout set so that I can run my analysis. I selected this based on memory and time scenarios  provided by Cursor. 

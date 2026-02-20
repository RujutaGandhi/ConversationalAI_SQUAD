# Conversational AI for SQuAD

A conversational AI agent that answers questions from the [SQuAD 2.0](https://rajpurkar.github.io/SQuAD-explorer/) dataset, with a strong emphasis on **reducing false positives** by saying *"I don't have the answer"* when no answer is available.

> **Design principle:** It is more important to not give the wrong answer than it is to give the answer.
> **Personal Goal:** Use Cursor for the end to end project. 

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

## Dataset

Uses **SQuAD 2.0** (`train-v2.0.json`, `dev-v2.0.json`):
- Reading comprehension with unanswerable (adversarial) questions
- Each question has `is_impossible: true` (no answer) or `false` (answerable)

---

## Repository

[github.com/RujutaGandhi/ConversationalAI_SQUAD](https://github.com/RujutaGandhi/ConversationalAI_SQUAD)

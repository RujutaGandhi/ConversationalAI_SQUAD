# Step 1: Train-v2 Dataset Analysis

## Dataset Overview

**Format:** SQuAD 2.0 (Reading Comprehension with Unanswerable Questions)

### Structure

- **Version:** v2.0
- **Articles:** 442 Wikipedia articles
- **Schema:**
  - `data[]` → articles
  - Each article: `title`, `paragraphs[]`
  - Each paragraph: `context` (passage text), `qas[]` (question-answer pairs)
  - Each QA: `question`, `id`, `answers[]` (if answerable), **`is_impossible`** (boolean)

### Answer Statistics

| Metric | Count | Percentage |
|--------|-------|------------|
| **Total questions** | 130,319 | 100% |
| **Answerable (has answer)** | 86,821 | **66.6%** |
| **Unanswerable (no answer)** | 43,498 | **33.4%** |

---

## Example: Answerable Question

**Question:** When did Beyonce start becoming popular?  
**Answer:** in the late 1990s  

*The model should extract and return the answer from the context.*

---

## Example: Unanswerable Question

**Context:** *The Legend of Zelda: Twilight Princess... is an action-adventure game developed and published by Nintendo for the GameCube and Wii...*

**Question:** What category of game is Legend of Zelda: **Australia** Twilight?

*The question references "Australia Twilight" which does not exist in the context (the game is "Twilight Princess"). The model should respond "I don't have the answer."*

---

## Key Insight

Unanswerable questions are **adversarial**: they look plausible but reference entities or facts not present in the context. Training must emphasize abstention on these cases to minimize false positives.

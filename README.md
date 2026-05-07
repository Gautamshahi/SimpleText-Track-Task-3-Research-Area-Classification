# SimpleText Track — Task 3: Research Area Classification

## Overview

This pilot task focuses on the identification of research areas from scientific text. Participants are expected to develop models that classify scientific publications according to a predefined taxonomy.

The task aims to support automatic subject classification for scientific repositories and digital libraries, helping improve metadata consistency across collections such as arXiv and OpenAIRE.

The classification scheme is based on the DFG (German Research Foundation) classification system.

---

## Dataset

The dataset consists of scientific publication records stored in CSV format.

### Dataset Columns

| Column | Description |
|---|---|
| `id` | Unique identifier of the publication |
| `title` | Title of the publication |
| `abstract` | Abstract of the publication |
| `field_area` | Broad research field label |
| `discipline_area` | Fine-grained research discipline label |

### Label Structure

The dataset contains two hierarchical labels:

- `field_area`
- `discipline_area`

Both labels are derived from the DFG classification system.

> **Note:**  
> `discipline_area` is a subset of `field_area`.  
> Therefore, each discipline belongs to a corresponding research field.

---

## Data Splits

### Training Set

The training set contains:
- Input data
- Ground-truth labels (`field_area` and `discipline_area`)

### Test Set

The test set contains:
- Input data only

Ground-truth labels for the test set are hidden and used exclusively for evaluation.

---

## Evaluation

Submissions will be evaluated using three complementary metrics:

### 1. Exact Match (EM)

A binary metric that checks whether the predicted output exactly matches the ground truth.

### 2. String Distance (SD)

A normalized Levenshtein distance measuring textual similarity between the prediction and the reference.

### 3. Embedding Distance (ED)

A semantic similarity metric computed using BERT embeddings of the prediction and the reference.

---

## Submission Format

Participants must generate a prediction file named:

```text
submission.csv
```

The file must contain the following columns:

| Column Name | Description |
|---|---|
| `id` | Unique sample identifier |
| `label_em` | Prediction optimized for Exact Match |
| `label_sd` | Prediction optimized for String Distance |
| `label_ed` | Prediction optimized for Embedding Distance |

### Example

```csv
id,label_em,label_sd,label_ed
1,Engineering,Engineering,Engineering
2,Computer Science,Computer Science,Computer Science
```

---

## Submission Workflow

```text
submission.csv → submission.zip → Codabench
```

Participants must compress `submission.csv` into a `.zip` archive before uploading it to Codabench.

---

## Important Notes

- Ensure that column names exactly match the required submission format.
- Submissions must be uploaded as a `.zip` archive.
- Incorrect formatting may result in evaluation failure.

---

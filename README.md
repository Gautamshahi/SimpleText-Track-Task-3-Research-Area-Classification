# SimpleText Track — Task 3: Research Area Classification

## Overview
This pilot task focuses on identifying research areas from scientific texts. Participants are expected to develop models that classify scientific publications according to a predefined taxonomy based on the [DFG classification system](https://github.com/Gautamshahi/SimpleText-Track-Task-3-Research-Area-Classification/blob/main/classification_taxonomy.csv). The task may be approached either as a hierarchical classification problem or through the use of large language models (LLMs) for research area prediction.

The goal of the task is to support automatic subject classification in scientific repositories and digital libraries, thereby improving metadata consistency across collections such as arXiv and OpenAIRE.

The classification scheme used in this task is derived from the DFG (German Research Foundation) classification system. The task aims to identify only two labels of the research area, i.e., field and discipline

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

### Example
```csv
id,ltitle, abstract,field_area,discipline_area
train_1,	Finding Complex Biological Relationships in Recent PubMed Articles Using Bio-LDA,  The overwhelming amount of available scholarly literature in the life sciences poses significant challenges to scientists ..., Life Sciences, Biology
```

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

The training set contains (12301 records):
- Input data
- Ground-truth labels (`field_area` and `discipline_area`)

### Test Set

The test set contains (3106 records):
- Input data only

Ground-truth labels for the test set are hidden and used exclusively for evaluation.

---

## Evaluation

To evaluate the quality of the predicted research areas, submissions will be evaluated using  **Accuracy** using multiple evaluation measures, including **Exact Match(EM)**, **String Distance (SD)**, and **Embedding Distance (ED)**.


- Exact Match (EM) 
In an exact match, we compare the output of the model directly with the ground truth data. It is a binary measure for comparing the result; if it matches, then 1, else 0. For instance, if the LLM returns “Social” and the actual research area is “Social Science”, then the EM returns 0.

- String Distance (SD) For the string distance measure, we compute the similarity between the predicted and actual research areas using the normalized Levenshtein distance. This metric captures partially correct answers where the wording may differ slightly but still remains close to the expected result. The normalized Levenshtein similarity is computed as: 
<p align="center">
  <img src="https://github.com/Gautamshahi/SimpleText-Track-Task-3-Research-Area-Classification/blob/main/e1.png" alt="Evaluation Metrics" width="700"/>
</p>

- Embedding Distance (ED) For semantic similarity evaluation, we use BERT sentence embeddings to compare the predicted research area with the actual research area. Both texts are transformed into vector embeddings, and cosine similarity is computed between them.

<p align="center">
  <img src="https://github.com/Gautamshahi/SimpleText-Track-Task-3-Research-Area-Classification/blob/main/e2.png" alt="Evaluation Metrics" width="700"/>
</p>

This measure helps identify semantically equivalent predictions even when different wording is used.

### Accuracy

The accuracy metric is computed as:
Accuracy = Number of Correct Predictions/Total Number of Predictions

where:
- **Number of Correct Predictions** refers to the total number of correctly classified samples.
- **Total Number of Predictions** refers to the total number of evaluated samples.

## Submission Format

Participants must generate a prediction file named:

```text
submission.csv
```

The file must contain the following columns:

| Column Name | Description |
|---|---|
| `id` | Unique sample identifier |
| `field_area` | Prediction optimized for Exact Match |
| `displicine_area` | Prediction optimized for String Distance |


The task is based on the hierarchical classification of research area ([Journal Paper](https://arxiv.org/pdf/2604.23430)):
```
@article{shahi2026automating,
  title={Automating Categorization of Scientific Texts with In-Context Learning and Prompt-Chaining in Large Language Models},
  author={Shahi, Gautam Kishore and Hummel, Oliver},
  journal={arXiv preprint arXiv:2604.23430},
  year={2026}
}
```

---

## Submission Workflow

```text
submission.csv → submission.zip → Google Form 
```

Submission files need 3106 entries with IDs, field_area, and displicine_area, and Participants must compress `submission.csv` into a `.zip` archive before uploading it to ([Google Form](https://forms.gle/HpSPiHjtzpW3yHFu6)).

---

## Important Notes

- Ensure that column names exactly match the required submission format.
- Submissions must be uploaded as a `.zip` archive.
- Incorrect formatting may result in evaluation failure.

---
## Leaderboard
Ranking is based on exact matches between the field and discipline, and an entry matches the test data when both fields and disciplines match.

| Rank | Team Name | Rows | Field EM | Field SD | Field ED | Discipline EM | Discipline SD | Discipline ED | Exact Both Fields |
|------|------------|------|-----------|-----------|-----------|----------------|----------------|----------------|-------------------|
| 1 | Ella Hawkins | 3106 | 0.9559 | 0.9801 | 0.9824 | 0.8902 | 0.9147 | 0.9386 | 0.8899 |
| 2 | Edwin Thuma | 3106 | 0.9549 | 0.9798 | 0.9828 | 0.8947 | 0.9171 | 0.9411 | 0.8947 |
| 3 | gemini-3.5-flash - Jaap Kamps | 3106 | 0.8606 | 0.9373 | 0.9379 | 0.7888 | 0.8350 | 0.8807 | 0.7888 |
| 4 | David Condrey | 3106 | 0.8117 | 0.9171 | 0.9180 | 0.6645 | 0.7303 | 0.7980 | 0.6645 |
| 5 | st26-Task3-dummy - Jaap Kamps | 3106 | 0.7675 | 0.8993 | 0.9070 | 0.4127 | 0.5745 | 0.6712 | 0.4127 |

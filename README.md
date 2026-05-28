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


| Team Name | Discipline Area |  |  | Field Area |  |  |
|------------|-----------------|--|--|------------|--|--|
|            | EM | SD | ED | EM | SD | ED |
| UBCS_2 | 0.5915 | 0.6877 | 0.7738 | 0.7684 | 0.8538 | 0.8912 |
| AIIRLab_2 | 0.6539 | 0.7356 | 0.8068 | 0.7353 | 0.8270 | 0.8695 |
| Data Dumplings | 0.5983 | 0.6909 | 0.7836 | 0.8448 | 0.9080 | 0.9242 |
| SRH-Reliable AI | 0.6056 | 0.7003 | 0.7780 | 0.7390 | 0.8284 | 0.8689 |
| UBCS_1 | 0.5518 | 0.6483 | 0.7533 | 0.7573 | 0.8481 | 0.8804 |
| AIIRLab_1 | 0.5838 | 0.6746 | 0.7696 | 0.7288 | 0.8244 | 0.8698 |
| UAmsterdam_2 | 0.6122 | 0.7035 | 0.7759 | 0.7033 | 0.8279 | 0.8472 |
| Writerslogic Inc | 0.4439 | 0.5676 | 0.6571 | 0.5561 | 0.7471 | 0.7924 |
| UAmsterdam_1 | 0.0625 | 0.2281 | 0.4099 | 0.2000 | 0.6225 | 0.6659 |


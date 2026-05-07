# SimpleText Track — Task 3: Research Area Classification

## Overview
This pilot task focuses on identifying research areas from scientific texts. Participants are expected to develop models that classify scientific publications according to a predefined taxonomy based on the [DFG classification system](https://github.com/Gautamshahi/SimpleText-Track-Task-3-Research-Area-Classification/blob/main/classification_taxonomy.csv). The task may be approached either as a hierarchical classification problem or through the use of large language models (LLMs) for research area prediction.

The goal of the task is to support automatic subject classification in scientific repositories and digital libraries, thereby improving metadata consistency across collections such as arXiv and OpenAIRE.

The classification scheme used in this task is derived from the DFG (German Research Foundation) classification system. The task aims to identify only two labels of the research area i.e, filed and discipline


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

The training set contains:
- Input data
- Ground-truth labels (`field_area` and `discipline_area`)

### Test Set

The test set contains:
- Input data only

Ground-truth labels for the test set are hidden and used exclusively for evaluation.

---

## Evaluation

To evaluate the quality of the predicted research areas, submissions will be evaluated using accuracy using multiple evaluation measures, including **String Distance (SD)**, **Embedding Distance (ED)**, and **Accuracy**.

### String Distance (SD)

For the string distance measure, we compute the similarity between the predicted research areas and the actual research areas using the normalized Levenshtein distance. This metric captures partially correct answers where the wording may differ slightly but still remains close to the expected result.

The normalized Levenshtein distance is computed as:
\[
SD(s_1, s_2) = 1 - \frac{\text{lev}(s_1, s_2)}{\max(|s_1|, |s_2|)}
\]

where:
- \(s_1, s_2\) are the two strings being compared,
- \(\text{lev}(s_1, s_2)\) is the Levenshtein distance between the strings,
- \(|s_1|, |s_2|\) represent the lengths of the strings,
- \(\max(|s_1|, |s_2|)\) normalizes the score between 0 and 1.

If the resulting similarity score exceeds **0.7**, the prediction is considered a match.

### Embedding Distance (ED)

For semantic similarity evaluation, we use BERT sentence embeddings to compare the predicted research area with the actual research area. Both texts are transformed into vector embeddings, and cosine similarity is computed between them.

Let \(v_{\text{model}}\) and \(v_{\text{actual}}\) represent the sentence embeddings for the predicted and actual research areas, respectively. The embedding distance is defined as:

\[
ED = \cos(v_{\text{model}}, v_{\text{actual}}) =
\frac{v_{\text{model}} \cdot v_{\text{actual}}}
{\|v_{\text{model}}\| \, \|v_{\text{actual}}\|}
\]

A prediction is considered a match if:

\[
\text{Match} =
\begin{cases}
1, & \text{if } ED > 0.7 \\
0, & \text{otherwise}
\end{cases}
\]

This measure helps identify semantically equivalent predictions even when different wording is used.

### Accuracy

After computing all evaluation measures, we used accuracy to report the final results obtained from different prompt engineering strategies and parameter settings.

Accuracy is defined as:

\[
\text{Accuracy} =
\frac{\text{Number of Correct Predictions}}
{\text{Total Number of Predictions}}
\]

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
submission.csv → submission.zip → Codabench
```

Participants must compress `submission.csv` into a `.zip` archive before uploading it to Codabench.

---

## Important Notes

- Ensure that column names exactly match the required submission format.
- Submissions must be uploaded as a `.zip` archive.
- Incorrect formatting may result in evaluation failure.

---

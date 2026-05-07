# SimpleText-Track-Task-3-Research-Area-Classification


The pilot task proposal is on Identification of research areas from scientific text. The task aims to develop a novel approach to classify scientific articles using a given taxonomy. Traditional subject classification in libraries is a solvable problem, and can accelerate consistent metadata across collections (arXiv, Openaire)


---

## Dataset
The data is organized as follows
-ID: Label
-Title: Title of the publication
-Abstract: Title of the publication
-Labels:  
  -Field_area: field of the publication
  -Discipline_area: discipline of the publication

Field and Discipline are derviced form DFG classification system. 

Field and Discipline are hierarchically related, so Discipline will always be a subset of Field. 


The competition dataset includes:

- **Training Set**
  - Input data
  - Ground-truth labels

- **Test Set**
  - Input data only
  - Ground-truth labels are hidden and used exclusively for evaluation
    

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

# Embedding-Based Search and Evaluation Across Multi-Domain Datasets

This repository demonstrates the use of machine learning techniques, particularly Sentence Transformers, to embed and search datasets using similarity metrics. It explores multiple datasets, evaluates search performance, and calculates key metrics.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Dataset Usage](#dataset-usage)
4. [Code Workflow](#code-workflow)
    - [NTCIR-18 AEOLLM Dataset](#ntcir-18-aeollm-dataset)
    - [ImageCLEF Dataset](#imageclef-dataset)
    - [TREC Clinical Trials Dataset](#trec-clinical-trials-dataset)
5. [Evaluation Metrics](#evaluation-metrics)
6. [Running the Code](#running-the-code)
7. [Contributions](#contributions)

---

## Introduction

This project applies semantic search techniques to three datasets:
1. **NTCIR-18 AEOLLM**: A dataset designed for evaluating QA systems.
2. **ImageCLEF**: Contains annotated image descriptions.
3. **TREC Clinical Trials**: A collection of clinical trial descriptions.

Using Sentence Transformers for embedding text and cosine similarity for search and ranking.

---

## Dependencies

Install the required Python libraries using:

```bash
pip install datasets pandas sentence-transformers sklearn lxml
```

Ensure that your environment has access to tools like `wget` and `tar` for downloading and extracting datasets.

---

## Dataset Usage

### 1. NTCIR-18 AEOLLM
- Source: [Hugging Face](https://huggingface.co/datasets/THUIR/AEOLLM)
- Fields: `question`, `answer`, `score`.
- Search Functionality: Retrieves the most relevant Q&A pairs based on cosine similarity.

### 2. ImageCLEF
- Source: [RWTH Aachen](http://www-i6.informatik.rwth-aachen.de/imageclef/resources/iaprtc12.tgz)
- Fields: `title`, `description`, `image_path`.
- Search Functionality: Displays top matching annotations alongside images.

### 3. TREC Clinical Trials
- Source: [TREC Clinical Trials](https://www.trec-cds.org/2021.html#documents)
- Fields: `brief_title`, `brief_summary`, `detailed_description`.
- Search Functionality: Retrieves clinical trials matching a given query.

---

## Code Workflow

### NTCIR-18 AEOLLM Dataset

1. **Load Dataset**:
   ```python
   dataset = load_dataset("THUIR/AEOLLM", split='train')
   ```
   Convert to a DataFrame and create a `Combined_Text` column by merging `question` and `answer`.

2. **Embedding and Search**:
   - Use Sentence Transformers (`all-MiniLM-L6-v2`) to generate embeddings.
   - Define a function to search for the top-N most relevant Q&A pairs based on cosine similarity.

3. **Evaluation**:
   - Calculate Precision@30, Recall@30, F1-Score, and Mean Average Precision (mAP).

---

### ImageCLEF Dataset

1. **Download and Parse**:
   Download and extract the ImageCLEF dataset using:
   ```bash
   wget http://www-i6.informatik.rwth-aachen.de/imageclef/resources/iaprtc12.tgz -O iaprtc12.tgz
   tar -xvzf iaprtc12.tgz -C /content/
   ```

   Extract annotations using a custom parser.

2. **Embedding and Search**:
   - Generate embeddings for combined `title` and `description`.
   - Search results include matching annotations and corresponding images.

3. **Evaluation**:
   - Metrics are calculated based on cosine similarity thresholds.

---

### TREC Clinical Trials Dataset

1. **Download and Parse**:
   Download the dataset:
   ```bash
   wget https://www.trec-cds.org/2021_data/ClinicalTrials.2021-04-27.part1.zip -O ClinicalTrials.zip
   unzip -o ClinicalTrials.zip -d /content/
   ```

   Parse XML files to extract fields (`brief_title`, `brief_summary`, etc.).

2. **Embedding and Search**:
   - Embed combined trial information.
   - Retrieve the top-N most relevant trials for a given query.

3. **Evaluation**:
   - Calculate Precision@30, Recall@30, F1-Score, and MAP for relevance.

---

## Evaluation Metrics

### Key Metrics:
1. **Precision@K**:
   \( \text{Precision@K} = \frac{\text{Relevant retrieved documents}}{\text{K}} \)

2. **Recall@K**:
   \( \text{Recall@K} = \frac{\text{Relevant retrieved documents}}{\text{Total relevant documents}} \)

3. **F1-Score**:
   Harmonic mean of Precision and Recall.

4. **Mean Average Precision (MAP)**:
   Average precision across all relevant documents.

---

## Running the Code

1. Clone this repository and install dependencies.
2. Run the scripts corresponding to each dataset:
   - **NTCIR-18 AEOLLM**:
     ```bash
     python proj_ntcir.py
     ```
   - **ImageCLEF**:
     ```bash
     python proj_imageclef.py
     ```
   - **TREC Clinical Trials**:
     ```bash
     python proj_trec_trials.py
     ```
3. Modify queries as needed in the respective scripts.

---

## Contributions

Contributions are welcome! Feel free to submit a pull request or open an issue for improvements or questions.

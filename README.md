# Semantic-Preserving Transformations as Mutation Operators  
### A Study on Their Effectiveness in Defect Detection

This repository accompanies the research paper:

> **Semantic-Preserving Transformations as Mutation Operators: A Study on Their Effectiveness in Defect Detection**  
> *IEEE International Conference on Software Testing Workshops (ICSTW), 2025*  
> DOI: https://doi.org/10.1109/ICSTW64639.2025.10962512  
> IEEE Xplore: https://ieeexplore.ieee.org/abstract/document/10962512

---

## 📌 Overview

Recent advances in defect detection increasingly rely on large language models (LLMs). Prior work has shown that augmenting training data with *semantically identical code* can improve model robustness. However, the potential of such transformations **during the testing stage**—a concept closely related to *metamorphic testing*—has not been thoroughly investigated.

In this work, we study whether **semantic-preserving transformations**, used analogously to mutation operators, can improve defect detection performance at inference time. We:

- Survey existing literature on semantic-preserving transformations
- Collect and reuse published implementations
- Apply these transformations to the **Devign** vulnerability dataset
- Evaluate their effectiveness using two fine-tuned LLMs: **VulBERTa** and **PLBART**
- Investigate multiple ensemble strategies

### Key Findings

- We identified **28 publications** proposing **94 transformations**
- Implemented **39 transformations** from four representative tools
- Manual inspection revealed that **23/39 transformations break semantics**
- Using the remaining **16 valid transformations**, none of the evaluated ensemble strategies improved model accuracy
- Reusing semantic-preserving transformations is **non-trivial** and often unsafe

---

## 📊 Repository Purpose

This repository provides:
- Manual evaluation results
- Ealuation scripts
- Jupyter notebooks to replicate all figures and analyses from the paper

For large dataset artifacts, see the Figshare repository:

🔗 **Figshare**: https://figshare.com/s/f9b93d9d549f316b1e5d?file=46143666

---

## 🗂️ Repository Contents

### Transformation Metadata & Reports

- **`Transformation-Information.xlsx`**  
  Examples and descriptions of each implemented transformation.

- **`Manual-evaluation-report.pdf`**  
  Results of a manual inspection of up to 20 transformed examples per transformation.  
  Each transformation is labeled as:
  - **GOOD**: semantics preserved  
  - **BAD**: semantics changed

---

### Transformed Datasets

- **`Devign-Transformed-TEST.json`**  
  Transformed functions from the Devign test set.

- **`Devign-Transformed-VALID.json`**  
  Transformed functions from the Devign validation set.

- **`TransformationDetails-TEST.txt`**  
- **`TransformationDetails-VALID.txt`**  

  One line per transformed function, containing:
repository_name, transformation_name, function_id, ground_truth_label


---

### Evaluation & Analysis Notebooks

- **`Evaluation-RQ1.ipynb`**  
Replicates **Figure 2** and **Figure 3** from the paper.

- **`Evaluation-Corrective.ipynb`**  
Replicates **Figure 4**.

- **`Ensemble.ipynb`**  
Ensemble computation using voting and averaging.

- **`Ensemble-Weighted-Labels.ipynb`**  
Weighted ensemble based on predicted labels.

- **`Ensemble-Weighted-Probabilities.ipynb`**  
Weighted ensemble based on predicted probabilities.

---

## 📁 Devign Dataset

- **`/devign/`**  
Contains the original Devign dataset and scripts defining the train/validation/test splits.

### Dataset Source

- Devign dataset:  
https://drive.google.com/file/d/1x6hoF7G-tSYxg8AFybggypLZgMGDNHfF/view

- Processing & splitting scripts:  
https://github.com/microsoft/CodeXGLUE/tree/main/Code-Code/Defect-detection

---

## 📁 Model Results

The **`/Results/`** folder contains prediction outputs from both LLMs:

**PLBART**
- `plbart-TEST.txt`
- `plbart-VALID.txt`
- `plbart-transformed-TEST.txt`
- `plbart-transformed-VALID.txt`

**VulBERTa**
- `vulberta-TEST.txt`
- `vulberta-VALID.txt`
- `vulberta-transformed-TEST.txt`
- `vulberta-transformed-VALID.txt`



### Prediction File Format

Each of the eight prediction files shares the same structure:

- One row per transformed function
- Values separated by tabs: predicted_label ground_truth_label

---

## 📁 Transformed Code Artifacts

- **`/Devign-transformations/`**  
Contains transformed versions of each function in the test and validation sets.
- Folder name: applied transformation
- File name: function ID (matching the Devign dataset)

---

## 🤖 Large Language Models Used

We evaluate two fine-tuned defect detection models:

- **PLBART**  
https://github.com/wasiahmad/PLBART  
Evaluation scripts:  
https://github.com/wasiahmad/PLBART/blob/main/scripts/code_to_code/defect_prediction/

- **VulBERTa**  
https://github.com/ICL-ml4csec/VulBERTa  
Evaluation notebook:  
https://github.com/ICL-ml4csec/VulBERTa/blob/main/Evaluation_VulBERTa-MLP.ipynb

---

## 🔧 Semantic-Preserving Transformations

Transformations were implemented based on the following tools:

- **NatGen**  
https://github.com/saikat107/NatGen

- **CodeImitator**  
https://github.com/saikat107/NatGen

- **LimitsOfML4Vuln**  
https://github.com/niklasrisse/LimitsOfML4Vuln

- **RoPGen**  
https://github.com/RoPGen/RoPGen

> ⚠️ Our study shows that many published transformations do **not** reliably preserve semantics when reused outside their original context.

---

## 📖 Citation

If you use this repository or dataset, please cite:

```bibtex
@INPROCEEDINGS{10962512,
  author={Hort, Max and Vidziunas, Linas and Moonen, Leon},
  booktitle={2025 IEEE International Conference on Software Testing, Verification and Validation Workshops (ICSTW)}, 
  title={Semantic-Preserving Transformations as Mutation Operators: A Study on Their Effectiveness in Defect Detection}, 
  year={2025},
  volume={},
  number={},
  pages={337-346},
  keywords={Software testing;Computer languages;Codes;Accuracy;Source coding;Semantics;Training data;Predictive models;Robustness;Defect detection;defect detection;language model;semantic-preserving transformation;ensemble},
  doi={10.1109/ICSTW64639.2025.10962512}}

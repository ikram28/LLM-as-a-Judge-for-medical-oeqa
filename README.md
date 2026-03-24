# 🩺 Who Judges the Judge?

### Evaluating LLM-as-a-Judge for French Medical Open-Ended QA

📄 Paper: [Who Judges the Judge? Evaluating LLM-as-a-Judge for French Medical OEQA](https://arxiv.org/abs/2603.04033)

---

## 🔍 Overview

Evaluating open-ended medical question answering (OEQA) is difficult because it requires expert judgment rather than simple lexical matching. This project investigates whether **Large Language Models (LLMs)** can act as reliable evaluators (*LLM-as-a-Judge*) for **French medical QA**.

We study:

* How well LLM judges align with **clinical expert annotations**
* Whether judgments are **biased by the answer-generating model**
* How to **adapt small models** into reliable evaluators with limited data

---

## 🧠 Key Contributions

* 📊 **First evaluation of LLM-as-a-Judge for French medical OEQA**
* ⚠️ **Generator bias analysis**: LLM judges are not invariant to answer sources
* 🧪 **Lightweight alignment study**:

  * Supervised Fine-Tuning (SFT)
  * Group Relative Policy Optimization (GRPO)
* 🚀 Demonstration that **small models (Phi-3.5-mini)** can become competitive judges after adaptation

---

## 🏗️ Pipeline Overview

The evaluation framework follows three main steps:

1. **Answer Generation**

   * 100 medical questions
   * 5 LLM generators → 500 answers

2. **Human Annotation**

   * Clinician labels **semantic equivalence (0/1)**

3. **LLM-as-a-Judge Evaluation**

   * Multiple LLM judges predict equivalence
   * Compared against expert labels

➡️ Then:

* A small model is aligned via **SFT + GRPO**
* Performance is evaluated with statistical testing

---

## 📦 Dataset

### Training Set

* 100 French medical OEQA samples
* Augmented with:

  * Paraphrases (positive examples)
  * Swapped answers (negative examples)

### Evaluation Set

* 500 (question, reference, generated answer) triplets
* Annotated by a **board-certified clinician**
* 90% inter-annotator agreement (subset)

---

## ⚙️ Models

### 🧾 Answer Generators

* Gemma-3-4B
* MedGemma-4B
* Qwen3-4B
* SFT-Qwen-4B
* SFT-LLaMA-13B

### ⚖️ LLM Judges

* GPT-5.1
* Gemini-2.5-Pro
* Qwen3-Next-80B
* MedGemma-27B
* Phi-3.5-mini (Base / SFT / GRPO)

---

## 📏 Evaluation Metrics

* **Accuracy**
* **F1-score**
* **Pearson Correlation**
* **Statistical significance tests**:

  * McNemar (accuracy)
  * Bootstrap & permutation (F1, correlation)

---

## 📊 Key Findings

### ❌ Standard metrics fail

ROUGE, BLEU, and BERTScore show **weak correlation with expert judgments**.

### ⚠️ LLM judges are biased

Performance varies depending on:

* Answer verbosity
* Model family
* Domain adaptation

### 🧠 Domain matters

* **MedGemma-27B** show best alignment with clinicians
* General models (e.g., GPT-5.1) are more conservative

### 🚀 Small models can compete

* Phi-3.5-mini + **SFT + GRPO**:

  * Large accuracy gains (+24%)
  * Reduced bias across generators
  * Comparable to larger models

---

## 🧪 Training Details (Phi-3.5-mini)

* SFT: 5 epochs
* GRPO: 2 epochs
* Dataset: 184 labeled examples
* Reward:

  * +1 / -1 (correctness)
  * +0.5 (format compliance)


---

## ⚠️ Limitations

* Small dataset size
* Binary equivalence only (no nuanced scoring)
* Bias not fully explored across all models
* Limited to French medical domain

---

## 🧭 Future Work

* Larger annotated datasets
* Multi-dimensional evaluation (safety, reasoning, completeness)
* Multilingual generalization
* Advanced alignment methods

---

## ⚖️ Ethical Considerations

* Not intended for clinical decision-making
* LLM judges show **moderate agreement only**
* Must not replace expert evaluation in medical contexts

---

## 📜 Citation

```bibtex
@inproceedings{belmadani-etal-2026-judges,
    title = "Who Judges the Judge? Evaluating {LLM}-as-a-Judge for {F}rench Medical open-ended {QA}",
    author = "Belmadani, Ikram  and
      El Khettari, Oumaima  and
      Constant dit Beaufils, Pac{\^o}me  and
      Dufour, Richard  and
      Favre, Benoit",
    editor = {Danilova, Vera  and
      Kurfal{\i}, Murathan  and
      S{\"o}derfeldt, Ylva  and
      Reed, Julia  and
      Burchell, Andrew},
    booktitle = "Proceedings of the 1st Workshop on Linguistic Analysis for Health ({H}ea{L}ing 2026)",
    month = mar,
    year = "2026",
    address = "Rabat, Morocco",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2026.healing-1.12/",
    pages = "142--157",
    ISBN = "979-8-89176-367-8",
    abstract = "Automatic evaluation of open-ended question answering in specialized domains remains challenging mainly because it relies on manual annotations from domain experts. In this work, we assess the ability of several large language models (LLMs), including closed-access (GPT-5.1, Gemini-2.5-Pro), open-source general-purpose (Qwen-80B), and biomedical domain-adapted models (MedGemma-27B, Phi-3.5-mini variants), to act as automatic evaluators of semantic equivalence in French medical open-ended QA. Our analysis reveals that LLM-based judgments are sensitive to the source of answer generation: judgement correlation varies substantially across different generator models. Among the judges, MedGemma-27B and Qwen-80B achieve the highest agreement with expert annotations in terms of F1 score and Pearson correlation. We further explore lightweight adaptation strategies on Phi-3.5-mini using supervised fine-tuning (SFT) and Group Relative Policy Optimization (GRPO). Even with 184 training instances, these adaptations significantly improve Phi-3.5{'}s results and reduce variability across answer generators, achieving performance comparable to larger domain-adapted models. Our results highlight the importance of generator-aware evaluation, the limitations of general-purpose LLMs in domain-specific settings, and the effectiveness of lightweight adaptation for compact models in low-resource scenarios."
}
```

---

## 💬 Contact

For questions or collaboration:

* [Ikram Belmadani](mailto:ikram.belmadani@lis-lab.fr) 
* [Oumaima El Khettari](mailto:oumaima.el-khettari@univ-nantes.fr)

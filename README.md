# Collaborative-Reasoning

This notebook compares **Qwen‑2.5‑3B‑Instruct** and **Llama‑3‑3B‑Instruct** on three
multiple‑choice QA datasets, using a three‑stage collaborative‑reasoning protocol.

## 1 What happens?

| Stage (dict key)                                | Description                                                                                                   |
|-------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| `individual_answers_with_explanations_*`        | Each model answers the question **alone** and explains every option.                                          |
| `disagreement_resolution_*`                     | If the two models disagree, a *two‑choice debate* prompt is built from their step‑1 explanations; each picks again.  (If they already agreed or a JSON error occurs, the stage‑1 score is reused.) |
| `Explanation_Based_Answer_selection_*`          | Each model now sees the original question **plus** both full step‑1 JSON answers and chooses once more.       |

For every dataset the code returns six accuracy lists (`qwen`/`llama` × three stages) and prints their means.

Datasets used:

* **OpenBookQA** – 500 test items  
* **ARC‑Easy**   – 500 test items  
* **ARC‑Challenge** – 500 test items

---

## 2 Requirements

* GPU runtime (Colab **GPU** or local CUDA GPU)  
* Python 3.9+  
* Packages installed in the notebook:
* Hugging Face access token with permission for the two models.


## 3 Quick start

```bash
pip install transformers datasets

# 1.  (only once)  log in so the models can be loaded
huggingface-cli login      # paste your HF token

# 2.  open/run the notebook (or execute evaluate.py if you saved it as a script)
#     make sure the runtime has a GPU

Running all cells evaluates 1 500 questions and prints output like for all three datasets:
individual_answers_with_explanations_qwen : 0.740
individual_answers_with_explanations_llama: 0.712
disagreement_resolution_qwen              : 0.780
disagreement_resolution_llama             : 0.768
Explanation_Based_Answer_selection_qwen   : 0.792
Explanation_Based_Answer_selection_llama  : 0.781

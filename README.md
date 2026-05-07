<div align="center">

# From Architecture to Output

### Structural Origins of Hallucination in Large Language Models and the Amplifying Role of Data

<p>
  <img src="https://img.shields.io/badge/Paper-R1%20v2.0-2980B9?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Status-Under%20Review-C0392B?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Format-IEEE%20Conference-27AE60?style=for-the-badge" />
</p>

<p>
  <img src="https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white" />
  <img src="https://img.shields.io/badge/HuggingFace-Transformers-yellow?logo=huggingface&logoColor=black" />
  <img src="https://img.shields.io/badge/LaTeX-Overleaf-008080?logo=latex&logoColor=white" />
  <img src="https://img.shields.io/badge/License-MIT-lightgrey" />
</p>

<p><em>
"Hallucination is not a surface phenomenon. It is a structural consequence of three architectural decisions that together form a compound failure system."
</em></p>

</div>

---

## 📖 Abstract

Large language models hallucinate—producing flu ent, confident, factually wrong outputs—with a consistency that persists across generations and scales. Existing taxonomies clas sify hallucination by output type, distinguishing intrinsic from extrinsic failures and faithfulness from factuality divergence. These frameworks are descriptively rigorous but do not identify which internal mechanism produced a given instance. This paper analyses hallucination as a structural consequence of three architectural decisions that together form a compound failure sys tem. Self-attention’s co-occurrence learning substitutes statistical proximity for semantic meaning and produces entity confusion, fact misattribution, and semantic drift. The maximum likelihood estimation training objective optimises next-token probability without factual constraint, rewarding statistically plausible out puts regardless of their truth value. Autoregressive decoding’s permanent left-to-right commitment under exposure bias ensures that a single wrong token cascades forward through the entire output sequence without revision. Dataset pathologies—long-tail deficiencies, training bias, and synthetic pollution—amplify these vulnerabilities but do not independently cause them. We make three contributions. First, we map each mechanism to a specific output category in the Alansari and Luqman taxonomy, locating intrinsic hallucination in self-attention, extrinsic hallucination in MLE, and logical inconsistency in autoregressive decoding. Second, we show that each commonly cited dataset pathology exploits one of these mechanisms rather than originating halluci nation independently. Third, we identify the diagnostic limitation of output-type-only classification and contrast it with inference layer mitigation approaches.

Keywords: Large Language Models, Hallucination, Transformer Architecture, Self-Attention, Maximum Likelihood Estimation, Autoregressive Decoding, Mechanistic Analysis, AI Safety, Self-Attention, FROM ARCHITECTURE TO OUTPUT, FROMARCHITECTURETOOUTPUT, STRUCTURAL ORIGINS, MD REJAUL KORIM SADI, SADI, Sadi et al, REJAUL KORIM, MD REJAUL KORIM, KORIM SADI, LLM, ML, NLP, NATURAL LANGUAGE PROCESSING, GENERATIVE MODEL, DATA SCIENCE, CHATGPT, ARTIFICIAL INTELLIGENCE, RESEARCHGATE, IEEE, SSRN ELSEVIER

This paper analyses hallucination as a **structural consequence of three architectural decisions** that together form a compound failure system:

1. **Self-attention's co-occurrence learning** — substitutes statistical proximity for semantic meaning
2. **The Maximum Likelihood Estimation (MLE) objective** — rewards statistical plausibility without factual constraint
3. **Autoregressive decoding under exposure bias** — commits permanently to one wrong token and cascades it forward

Dataset pathologies — long-tail deficiency, training bias, synthetic pollution — amplify these vulnerabilities but **do not independently cause them**. Architecture is the necessary condition. Dataset is the amplifier.

---

## 🧠 The Central Argument

<div align="center">

```
┌───────────────────┐   ┌───────────────────┐   ┌───────────────────┐
│   SELF-ATTENTION  │   │   MLE  OBJECTIVE  │   │   AUTOREGRESSIVE  │
│  co-occurrence    │   │  plausibility ≠   │   │  no revision path │
│   ≠ meaning       │   │      truth        │   │                   │
└─────────┬─────────┘   └─────────┬─────────┘   └─────────┬─────────┘
          │                       │                       │
          ▼                       ▼                       ▼
     Intrinsic               Extrinsic              Logical
   Hallucination           Hallucination        Inconsistency
          │                       │                       │
          └───────────────────────┼───────────────────────┘
                                  ▼
                    FLUENT · CONFIDENT · WRONG
```

</div>

---

## 🔬 Empirical Validation (Section VI)

We validated each mechanism empirically on **GPT-2** using controlled prompting experiments. All three mechanisms exhibit their theoretically predicted failure modes:

| Mechanism | Experiment | Result |
|:---|:---|:---:|
| **M1 — Self-Attention** | 15 co-occurrence misfire prompts | **86.7% misfire rate** |
| **M1 — Self-Attention** | Positional bias replication | Strong recency dominance |
| **M2 — MLE** | 5 truth-vs-falsehood matched pairs | **3/5 falsehoods preferred** |
| **M3 — Autoregressive** | 5 one-token-corruption cascade tests | **4/5 cascade failures** |

### Representative Findings

<details>
<summary><b>▸ Mechanism 1 — Co-occurrence misfire examples</b></summary>

```text
Prompt:  "Shakespeare was born in"
Output:  "1829 in the village of Bury St."
→ Confident, fluent, entirely fabricated.

Prompt:  "Python programming language was created by"
Output:  "the late Paul Graham."
→ Co-occurrence ("Python + programmer name") overrides factual grounding.
```
</details>

<details>
<summary><b>▸ Mechanism 2 — MLE prefers common falsehoods</b></summary>

```text
"We only use 10% of our brains."         ← falsehood preferred by 0.56
"Lightning never strikes the same place." ← falsehood preferred by 0.93
```
Near-equivalent scoring across pairs confirms MLE's structural indifference to factual accuracy.
</details>

<details>
<summary><b>▸ Mechanism 3 — Cascade under exposure bias</b></summary>

```text
CORRECT prefix: "The capital of France is Paris, which..."
Continuation:   "...is home to the French capital's largest city, the Louvre."

WRONG prefix:   "The capital of France is Berlin, which..."
Continuation:   "...is home to the world's largest concentration of German Jews."

→ A single token corruption redirects the entire generation trajectory.
```
</details>

---

## 📁 Repository Structure

```
📦 r1-hallucination-architecture/
├── 📄 main.tex                          # Full LaTeX manuscript
├── 📄 bibliography.bib                  # BibTeX references
├── 📂 figures/                          # All 11 paper figures
│   ├── fig1_causal_chain.pdf
│   ├── fig2_compound_failure.pdf
│   ├── fig3_self_attention.pdf
│   ├── fig4_autoregressive.pdf
│   ├── fig5_mle_chart.pdf
│   ├── fig6_inverse_scaling.pdf
│   ├── fig7_taxonomy.pdf
│   ├── fig_mechanism1_attention_heatmap.pdf
│   ├── fig_mechanism1_positional_bias.pdf
│   ├── fig_mechanism2_mle_bias.pdf
│   └── fig_mechanism3_cascade.pdf
├── 📂 empirical/                        # Reproducibility materials
│   ├── Self_Attention_Diffusion.ipynb   # Milestone 1 notebook
│   ├── MLE_Objective_Validation.ipynb   # Milestone 2 notebook
│   ├── Autoregressive_Decoding_Cascade.ipynb # Milestone 3 notebook
│   ├── mechanism1_outputs.csv           # M1 results (15 queries)
│   ├── mechanism2_outputs.csv           # M2 results (5 pairs)
│   └── mechanism3_outputs.csv           # M3 results (5 pairs)
└── 📄 README.md
```

---

## 🚀 Reproducing the Experiments

### Environment Setup

```bash
# Clone the repository
git clone https://github.com/<your-username>/r1-hallucination-architecture.git
cd r1-hallucination-architecture

# Create virtual environment
python -m venv venv
source venv/bin/activate          # macOS / Linux
venv\Scripts\activate             # Windows

# Install dependencies
pip install torch transformers bertviz matplotlib numpy pandas jupyter seaborn
```

### Run the Three Milestones

```bash
cd empirical
jupyter notebook
```

Then execute the notebooks in order:

| # | Notebook | Validates |
|:-:|:---|:---|
| 1 | `Self_Attention_Diffusion.ipynb` | Co-occurrence misfires + positional bias |
| 2 | `MLE_Objective_Validation.ipynb` | Fluency-over-factuality |
| 3 | `Autoregressive_Decoding_Cascade.ipynb` | Single-token cascade under exposure bias |

Each notebook writes its results to a CSV and generates the corresponding figure used in Section VI of the paper.

---

## 📊 Paper Map

| Section | Focus |
|:---:|:---|
| I | Prior hallucination surveys and their shared diagnostic limitation |
| II | Three architectural mechanisms as a compound failure system |
| III | Self-attention diffusion — intrinsic hallucination |
| IV | Autoregressive decoding — logical inconsistency |
| V | MLE objective — extrinsic hallucination |
| **VI** | **Empirical validation on GPT-2** |
| VII | Long-tail deficiency exploits MLE |
| VIII | Training bias exploits attention |
| IX | Synthetic pollution exploits all three |
| X | Discussion — mapping mechanisms to taxonomy |
| XI | Conclusion and future work |

---

## ✍️ Authors

<table>
  <tr>
    <td align="center">
      <b>Md. Rejaul Korim Sadi</b><br/>
      <sub>Dept. of CSE, Metropolitan University</sub><br/>
      <sub>Sylhet, Bangladesh</sub><br/>
      <sub><code>rejaulkorimsadi@gmail.com</code></sub>
    </td>
    <td align="center">
      <b>Toufiqur Rahman Tasin</b><br/>
      <sub>Dept. of CSE, Metropolitan University</sub><br/>
      <sub>Sylhet, Bangladesh</sub><br/>
      <sub><code>toufiqur.rahman.tasin@gmail.com</code></sub>
    </td>
    <td align="center">
      <b>Golam Mostofa Naeem</b><br/>
      <sub>Dept. of CSE, Metropolitan University</sub><br/>
      <sub>Sylhet, Bangladesh</sub><br/>
      <sub><code>gmnaeem7@gmail.com</code></sub>
    </td>
  </tr>
</table>

---

## 📚 Citation

If this work informs your research, please cite:

```bibtex
@article{sadi2026architecture,
  title={From Architecture to Output: Structural Origins of Hallucination in Large Language Models and the Amplifying Role of Data},
  author={Sadi, Md Rejaul Korim and Tasin, Toufiqur Rahman and Naeem, Golam Mostofa},
  journal={Available at SSRN 6604798},
  year={2026}
}
```

---

## 🔑 Key References

This paper engages with foundational work across the LLM hallucination literature:

- **Vaswani et al. (2017)** — Attention Is All You Need
- **Brown et al. (2020)** — Language Models are Few-Shot Learners (GPT-3)
- **Ranzato et al. (2016)** — Sequence-Level Training (exposure bias)
- **Lin et al. (2022)** — TruthfulQA (inverse scaling on truth)
- **Liu et al. (2024)** — Lost in the Middle (positional bias)
- **Shumailov et al. (2024)** — Model Collapse (*Nature*)
- **Bender et al. (2021)** — Stochastic Parrots
- **Alansari & Luqman (2025)** — Hallucination Survey
- **Huang et al. (2023)** — Hallucination Taxonomy
- **Elhage et al. (2021)** — Transformer Circuits

Full bibliography in [`bibliography.bib`](bibliography.bib).

---

## 🧭 Research Direction

This paper's framework points toward a concrete engineering goal:

> Future LLM architectures should treat **module-level observability** as a first-class design criterion — surfacing, at runtime, which of the three architectural operators produced a given error, so that intervention can be targeted at the structural source rather than the surface symptom.

---

<div align="center">

### ⭐ If this work helps you, a star helps us.

<sub>Made in Sylhet · Built for reproducibility · Open to collaboration</sub>


</div>

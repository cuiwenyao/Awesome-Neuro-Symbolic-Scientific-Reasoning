<a id="readme-top"></a>

<div align="center">

# 🧠🔣 Awesome Neuro-Symbolic Scientific Reasoning [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

**A curated list of papers & resources on Neuro-Symbolic reasoning for _trustworthy AI for science_**

[![Awesome](https://img.shields.io/badge/Awesome-NeSy_SciReason-7B68EE?logo=awesomelists&logoColor=white)](https://github.com/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![Stars](https://img.shields.io/github/stars/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning?style=social)](https://github.com/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning?color=blue)](https://github.com/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning/commits)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](./LICENSE)
[![arXiv](https://img.shields.io/badge/arXiv-coming_soon-b31b1b.svg)](https://github.com/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning)

[**中文**](./README_zh.md) ｜ **290+** references · **143** classified neuro-symbolic methods

</div>

---

> **This repository** accompanies our survey *Toward Trustworthy AI for Science through Neuro-Symbolic Reasoning: A Survey and Research Agenda*. It curates work that turns large-model reasoning from **fluent-but-unverifiable** into **traceable, diagnosable and repairable**, organised around a **three-layer trust pipeline** — **Knowledge → Reasoning → Verification** — that closes into a **loop**: a verified claim re-enters as new knowledge the next claim can build on.
>
> **Central claim.** The bottleneck of trustworthy AI for science is **not generation but verification** — the gate that turns each candidate into verified knowledge. No science yet owns a complete, executable, low-cost and diagnosable verifier, and neuro-symbolic reasoning is the principal means of constructing and completing it: **a Lean for science, in aspiration.**

## 🗺️ The Framework at a Glance

The pipeline builds a trustworthy scientific claim along a backbone, and each layer earns exactly **one trust dimension** (one-to-one). A verified claim is itself new traceable, checkable, updatable knowledge, so the pipeline closes **epistemically — through verification, not automation** — and only as far as verification is trustworthy.

```
            epistemic            inferential             empirical
        ┌───────────────┐   ┌───────────────────┐   ┌─────────────────┐
   ┌───►│   KNOWLEDGE    ├──►│     REASONING     ├──►│  VERIFICATION   ├──┐
   │    │   grounding    │   │ formalize+execute │   │ diagnose/repair │  │
   │    └───────────────┘   └───────────────────┘   └─────────────────┘  │
   │      K · grounder       R · representation        V · verifier       │
   │                         G · generator                                │
   │                         E · engine                  A · actuator     │
   │                                                                      │
   └──────────  verified claim written back: Kₜ → Kₜ₊₁  ◄─────────────────┘
                  (certificate · counterexample · measurement · uncertainty)

    Enactment (acting in the world) is a practice-closure property of this
    loop — examined science by science — not a fourth trust dimension.
```

**Six cross-cutting symbolic roles** (multi-label): **K** knowledge-grounder · **R** representation · **G** generator · **E** engine · **V** verifier · **A** actuator. Methods are also tagged by **Kautz integration depth** (T1 loosest → T6 tightest).

**Verification-maturity is the organizing variable.** Sciences differ in the verifier each admits, rated on two axes — **verifiability** (how much a mechanical check can certify) and **cost** per verdict. The prize is the cheap, fully-rigorous corner; today only formalizable claims (code, mathematics) reach it. See [the map](#vmap).

## 📢 News

- **2026-06** ｜ 🔁 Major restructure to match the survey rewrite: from a tool-centric three-layer view to the **Knowledge–Reasoning–Verification trust pipeline + loop**, a new **Applications across the Sciences** chapter, a **verification-maturity map**, and trust-aligned benchmarks.
- **2026-06** ｜ 🎉 Repository launched with a curated corpus of **290+** references and **143** classified neuro-symbolic methods.
- ⭐ The companion survey is in preparation; arXiv link coming soon.

## 📑 Table of Contents

<details open>

- [🧱 Foundations of Neuro-Symbolic AI](#foundations)
- [📚 Related Surveys & Position Papers](#surveys)
- [🧪 AI for Science Milestones](#milestones)
- [🧩 Layer 1 — Knowledge Grounding `epistemic`](#l1)
  - [Retrieval, Knowledge Graphs & Editing](#l1-rag)
  - [Symbolic Domain Knowledge, Rules & Causal Priors](#l1-rules)
  - [Knowledge Update & Memory](#l1-mem)
  - [Pure-Neural Baselines](#l1-base)
- [🔣 Layer 2 — Formalization & Executable Reasoning `inferential`](#l2)
  - [Chain-of-Thought & Inference-Time Reasoning (substrate)](#l2-cot)
  - [Symbolic Formalization & Autoformalization](#l2-form)
  - [Program, Algorithm & Law Synthesis](#l2-synth)
  - [Program- & Logic-Aided Execution + Symbolic Back-ends](#l2-exec)
  - [Formal Theorem Proving](#l2-proof)
  - [Differentiable & Abductive Neuro-Symbolic ⭐](#l2-diff)
- [✅ Layer 3 — Verification, Diagnosis & Adaptive Control `empirical`](#l3)
  - [Step-Level Diagnosis & Process Reward](#l3-prm)
  - [Verifier-Guided Learning & Verifiable Rewards (RLVR)](#l3-rlvr)
  - [Tool Selection, Routing & Cross-Verification](#l3-route)
  - [Feedback-Driven Repair](#l3-repair)
- [🔬 Applications across the Sciences — Closing the Loop](#apps)
  - [Formal Mathematics & Theorem Proving — *closure within the formal boundary*](#app-math)
  - [Algorithm & Code Discovery — *deterministic evaluators*](#app-algo)
  - [Chemistry & Autonomous Synthesis — *the loop reaches the bench*](#app-chem)
  - [Materials Discovery — *when the verifier is itself uncertain*](#app-mat)
  - [The Life Sciences — *prediction without closure*](#app-bio)
- [📊 Benchmarks & Trust-Aligned Evaluation](#bench)
- [🧭 Open Challenges & Research Agenda](#agenda)
- [🗺️ Verification-Maturity Map](#vmap)
- [🤝 Contributing](#contributing)
- [📌 Citation](#citation)

</details>

<a id="foundations"></a>
## 🧱 Foundations of Neuro-Symbolic AI

Classic symbolic engines, cognitive architectures and the differentiable neuro-symbolic lineage that today's large-model pipelines still build on as verifiers, solvers and reasoning back-ends.

| Title | Venue | Year | Links |
| :-- | :-- | :--: | :-- |
| DENDRAL: a case study of the first expert system | Book (Stanford) | 1980 | [Scholar](https://scholar.google.com/scholar?q=DENDRAL%20case%20study%20expert%20system) |
| MYCIN: computer-based medical consultations | Elsevier | 1976 | [Scholar](https://scholar.google.com/scholar?q=MYCIN%20computer-based%20medical%20consultations) |
| A framework for representing knowledge (frames) | MIT AI Memo | 1974 | [Scholar](https://scholar.google.com/scholar?q=Minsky%20framework%20for%20representing%20knowledge) |
| CYC: a large-scale investment in knowledge infrastructure | CACM | 1995 | [Scholar](https://scholar.google.com/scholar?q=CYC%20large-scale%20investment%20knowledge%20infrastructure) |
| SOAR: an architecture for general intelligence | Artificial Intelligence | 1987 | [Scholar](https://scholar.google.com/scholar?q=SOAR%20architecture%20for%20general%20intelligence) |
| An integrated theory of the mind (ACT-R) | Psychological Review | 2004 | [Scholar](https://scholar.google.com/scholar?q=integrated%20theory%20of%20the%20mind%20ACT-R) |
| Predicate logic as a programming language | IFIP | 1974 | [Scholar](https://scholar.google.com/scholar?q=Kowalski%20predicate%20logic%20as%20programming%20language) |
| Z3: an efficient SMT solver | TACAS | 2008 | [DOI](https://doi.org/10.1007/978-3-540-78800-3_24) |
| SWI-Prolog | Theory and Practice of Logic Programming | 2012 | [DOI](https://doi.org/10.1017/S1471068411000494) |
| Multi-shot ASP solving with clingo | Theory and Practice of Logic Programming | 2019 | [DOI](https://doi.org/10.1017/S1471068418000054) |
| Distilling free-form natural laws from experimental data | Science | 2009 | [DOI](https://doi.org/10.1126/science.1165893) |
| The third wave of neuro-symbolic AI (Kautz taxonomy) | AI Magazine / survey | 2023 | [Scholar](https://scholar.google.com/scholar?q=neurosymbolic%20AI%20third%20wave%20Garcez%20Lamb) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="surveys"></a>
## 📚 Related Surveys & Position Papers

The neuro-symbolic, RAG, knowledge-graph, agent, reasoning-model and AI-for-science literatures each have a mature survey, but each fixes a single axis and treats verification, feedback and the closed experimental loop only in passing. **None occupies the neuro-symbolic-reasoning × science intersection together with verification, the closed loop, trust dimensions and cross-domain transfer.** The closest neighbour reads AI for *mathematical* reasoning through a comprehension–generation–verification triad — the special case of our pipeline restricted to the one science whose verifier is already complete.

| Survey | Venue | Year | Links |
| :-- | :-- | :--: | :-- |
| Neuro-symbolic AI for LLM reasoning | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=neuro-symbolic%20AI%20for%20LLM%20reasoning%20survey) |
| LLM symbolic reasoning | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=large%20language%20model%20symbolic%20reasoning%20survey) |
| Design patterns for neuro-symbolic systems | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=design%20patterns%20neuro-symbolic%20systems) |
| Integrative vs. hybrid neuro-symbolic AI | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=integrative%20hybrid%20neuro-symbolic%20comparative) |
| From System 1 to System 2: a survey of reasoning LLMs | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=System%201%20to%20System%202%20reasoning%20LLM%20survey) |
| From automation to autonomy in scientific discovery | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=automation%20to%20autonomy%20scientific%20discovery%20LLM) |
| Towards scientific intelligence: LLM-based scientific agents | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=LLM-based%20scientific%20agents%20survey%20scientific%20intelligence) |
| Agentic AI for scientific discovery | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=agentic%20AI%20scientific%20discovery%20survey) |
| Towards large reasoning models: reinforced reasoning | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=towards%20large%20reasoning%20models%20reinforced%20survey) |
| The hitchhiker's guide to scientific agents | survey | 2025 | [Scholar](https://scholar.google.com/scholar?q=hitchhiker%20guide%20scientific%20agents%20survey) |
| Artificial intelligence for mathematical reasoning (triad + supervision ladder) | survey | 2026 | [Scholar](https://scholar.google.com/scholar?q=artificial%20intelligence%20for%20mathematical%20reasoning%20survey%202026) |
| Scientific discovery in the age of artificial intelligence | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06221-2) |
| Survey of hallucination in natural language generation | ACM Computing Surveys | 2023 | [DOI](https://doi.org/10.1145/3571730) |
| Unifying large language models and knowledge graphs: a roadmap | IEEE TKDE | 2024 | [DOI](https://doi.org/10.1109/TKDE.2024.3352100) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="milestones"></a>
## 🧪 AI for Science Milestones

Landmark systems where learning meets search, symbolic structure or formal verification to cross the *answerable* threshold in real science. Many are powerful **pure-neural predictors** — included here as the AI-for-science backdrop the survey bridges *toward* a verifiable loop.

| Title | Venue | Year | Links |
| :-- | :-- | :--: | :-- |
| Mastering the game of Go with deep neural networks and tree search | Nature | 2016 | [DOI](https://doi.org/10.1038/nature16961) |
| Mastering the game of Go without human knowledge | Nature | 2017 | [DOI](https://doi.org/10.1038/nature24270) |
| Highly accurate protein structure prediction with AlphaFold | Nature | 2021 | [DOI](https://doi.org/10.1038/s41586-021-03819-2) |
| Accurate structure prediction of biomolecular interactions with AlphaFold 3 | Nature | 2024 | [DOI](https://doi.org/10.1038/s41586-024-07487-w) |
| Boltz-1: open-source structure prediction at AlphaFold-3 quality | Nature Methods | 2025 | [arXiv](https://arxiv.org/abs/2411.13408) |
| Solving olympiad geometry without human demonstrations (AlphaGeometry) | Nature | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06747-5) |
| Mathematical discoveries from program search (FunSearch) | Nature | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06924-6) |
| AlphaEvolve: a coding agent for scientific and algorithmic discovery | arXiv | 2025 | [arXiv](https://arxiv.org/abs/2506.13131) |
| Discovering faster matrix multiplication with RL (AlphaTensor) | Nature | 2022 | [DOI](https://doi.org/10.1038/s41586-022-05172-4) |
| Faster sorting algorithms discovered using deep RL (AlphaDev) | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06004-9) |
| Olympiad-level formal mathematical reasoning with RL (AlphaProof) | Nature | 2026 | [DOI](https://doi.org/10.1038/s41586-025-09833-y) |
| Scaling deep learning for materials discovery (GNoME) | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06735-9) |
| A generative model for inorganic materials design (MatterGen) | Nature | 2025 | [DOI](https://doi.org/10.1038/s41586-025-08628-5) |
| Simulating 500 million years of evolution with a language model (ESM3) | Science | 2025 | [DOI](https://doi.org/10.1126/science.ads0018) |
| Autonomous chemical research with large language models (Coscientist) | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06792-0) |
| An autonomous laboratory for accelerated synthesis (A-Lab) | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06734-w) |
| A deep learning approach to antibiotic discovery | Cell | 2020 | [DOI](https://doi.org/10.1016/j.cell.2020.01.021) |
| Discovery of a structural class of antibiotics with explainable deep learning | Nature | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06887-8) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l1"></a>
## 🧩 Layer 1 — Knowledge Grounding `epistemic trust`

**Does the knowledge a model reasons from carry provenance, currency and a confidence it can be checked against?** The loop opens by externalizing evidence into provenance-aware symbolic form a back-end can inspect — and closes here, as verified results (certificates, counterexamples, measured values with uncertainty) are written back, growing the base from Kₜ to Kₜ₊₁. Symbolic role: **K** (grounder). The split that matters: either the externalized knowledge carries a **symbolic limb** a verifier can later inspect, or it only changes which text the model sees (a baseline).

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l1-rag"></a>
### Retrieval, Knowledge Graphs & Editing

Graph-structured retrieval and KG/rule grounding that add a symbolic limb — the methods the taxonomy retains.

| Title | Roles | T | Year | Links |
| :-- | :--: | :--: | :--: | :-- |
| GraphRAG: from local to global graph-based summarization | K·R | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=From%20local%20to%20global%20graph%20RAG%20query-focused%20summarization) |
| HippoRAG: neurobiologically inspired long-term memory | K·R·G | T3 | 2024 | [arXiv](https://arxiv.org/abs/2405.14831) |
| LightRAG: simple and fast retrieval-augmented generation | K·R | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=LightRAG%20simple%20fast%20retrieval-augmented%20generation) |
| Neuro-symbolic retrievers for retrieval-augmented generation | K·R | T3 | 2026 | [Scholar](https://scholar.google.com/scholar?q=neuro-symbolic%20retrievers%20retrieval-augmented%20generation) |
| QA-GNN: reasoning with LMs and knowledge graphs | K·E | T5 | 2021 | [Scholar](https://scholar.google.com/scholar?q=QA-GNN%20reasoning%20language%20models%20knowledge%20graphs) |
| K-Adapter: infusing knowledge into pre-trained models | K·R | T5 | 2021 | [Scholar](https://scholar.google.com/scholar?q=K-Adapter%20infusing%20knowledge%20pre-trained%20models%20adapters) |
| Think-on-Graph: deep and responsible reasoning on KGs | K·R·E | T3 | 2024 | [arXiv](https://arxiv.org/abs/2307.07697) |
| Unifying LLMs and KGs: a roadmap | — | — | 2024 | [DOI](https://doi.org/10.1109/TKDE.2024.3352100) |
| Unified neuro-symbolic reasoning over knowledge graphs | K·R·E | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=unified%20neurosymbolic%20reasoning%20knowledge%20graphs) |
| Neuro-symbolic methods for dynamic knowledge graphs (survey) | K·R | — | 2024 | [Scholar](https://scholar.google.com/scholar?q=neurosymbolic%20methods%20dynamic%20knowledge%20graphs%20survey) |
| NeuSTIP: neuro-symbolic model for temporal KG completion | K·R·E | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=NeuSTIP%20neuro-symbolic%20temporal%20knowledge%20graph) |
| CLAUSE: agentic neuro-symbolic KG context engineering | K·R·E | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=CLAUSE%20agentic%20neurosymbolic%20knowledge%20graph) |
| R2-KG: dual-agent reliable KG reasoning | K·R·V | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=R2-KG%20dual-agent%20reliable%20knowledge%20graph%20reasoning) |
| SymAgent: neural-symbolic self-learning KG agent | K·R·G·E | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=SymAgent%20neural-symbolic%20self-learning%20agent%20knowledge%20graph) |
| Logic Query of Thoughts (LQoT): KG-grounded logic queries | K·R·E | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=Logic%20Query%20of%20Thoughts%20knowledge%20graph) |
| Logic-aware curriculum tuning for KG reasoning | K·R | T4 | 2024 | [Scholar](https://scholar.google.com/scholar?q=logic-aware%20curriculum%20tuning%20knowledge%20graph%20reasoning) |
| OneEdit: neural-symbolic collaborative knowledge editing | K·R | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=OneEdit%20neural-symbolic%20collaborative%20knowledge%20editing) |
| Knowledge editing on dynamic KGs for multi-hop QA | K·R | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=knowledge%20editing%20dynamic%20knowledge%20graphs%20multi-hop) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l1-rules"></a>
### Symbolic Domain Knowledge, Rules & Causal Priors

Scientific knowledge entering reasoning as **executable feature functions, rules and constraints** — what later lets a solver *check*, not merely echo, a claim.

| Title | Roles | T | Year | Links |
| :-- | :--: | :--: | :--: | :-- |
| LLM4SD: large language models as scientific discoverers (literature+data rules) | K·R·G | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=LLM4SD%20large%20language%20models%20scientific%20discovery%20rules) |
| Ontology-guided neuro-symbolic math RAG | K | T3 | 2026 | [Scholar](https://scholar.google.com/scholar?q=ontology-guided%20neuro-symbolic%20mathematics%20RAG) |
| Enhancing LLMs with ontological reasoning (OWL + reasoner) | K·R·E·V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=enhancing%20large%20language%20models%20ontological%20reasoning%20OWL) |
| ChatRule: mining logical rules with LLMs for KG reasoning | K·R·G | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=ChatRule%20mining%20logical%20rules%20knowledge%20graph) |
| Simple augmentations of logical rules for NS-KGC | R·E | T5 | 2024 | [Scholar](https://scholar.google.com/scholar?q=simple%20augmentations%20logical%20rules%20neuro-symbolic%20knowledge%20graph) |
| LogicMP: FOL constraints as a differentiable neural layer | R·E | T6 | 2023 | [Scholar](https://scholar.google.com/scholar?q=LogicMP%20neurosymbolic%20encoding%20first-order%20constraints) |
| Neural-symbolic models for logical queries on KGs | R·E | T6 | 2022 | [Scholar](https://scholar.google.com/scholar?q=neural%20symbolic%20models%20logical%20queries%20knowledge%20graph) |
| Uni-Mol: a universal 3D molecular representation framework | R | T5 | 2023 | [Scholar](https://scholar.google.com/scholar?q=Uni-Mol%20universal%203D%20molecular%20representation) |
| MolCLR: molecular contrastive learning via GNNs | R | T5 | 2022 | [DOI](https://doi.org/10.1038/s42256-022-00447-x) |
| Molecular Transformer: reaction outcome prediction on SMILES | R·G | T5 | 2019 | [DOI](https://doi.org/10.1021/acscentsci.9b00576) |
| MoleculeNet: a benchmark for molecular machine learning | — | — | 2018 | [DOI](https://doi.org/10.1039/C7SC02664A) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l1-mem"></a>
### Knowledge Update & Memory

A trustworthy base must **change over time** — grounding is an update operator on Kₜ, and the place the loop returns its verification products. Weight editing alone carries no symbolic limb to keep the base consistent.

| Title | Roles | T | Year | Links |
| :-- | :--: | :--: | :--: | :-- |
| Symbolic working memory for rule reasoning | K·R·E | T4 | 2024 | [Scholar](https://scholar.google.com/scholar?q=symbolic%20working%20memory%20large%20language%20model%20rule%20reasoning) |
| AriGraph: knowledge-graph world-model memory for agents | K·R | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=AriGraph%20knowledge%20graph%20world%20model%20memory) |
| RecallM: adaptable temporal-graph memory | K·R | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=RecallM%20adaptable%20memory%20temporal%20understanding) |
| Rule-level knowledge editing (RuleEdit benchmark) | — | — | 2026 | [Scholar](https://scholar.google.com/scholar?q=RuleEdit%20benchmarking%20rule-level%20knowledge%20editing) |
| MemoryBank: long-term memory for LLMs | K | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=MemoryBank%20long-term%20memory%20large%20language%20models) |
| Towards continual knowledge learning of language models | K | — | 2022 | [Scholar](https://scholar.google.com/scholar?q=towards%20continual%20knowledge%20learning%20language%20models) |
| Evaluating the ripple effects of knowledge editing | — | — | 2023 | [Scholar](https://scholar.google.com/scholar?q=evaluating%20ripple%20effects%20knowledge%20editing) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l1-base"></a>
### Pure-Neural Baselines

Retrieval and weight-editing that change which text/fact the model sees but add **no symbolic limb** — documented as baselines, outside the neuro-symbolic taxonomy tree.

| Title | Venue | Year | Links |
| :-- | :-- | :--: | :-- |
| Retrieval-augmented generation for knowledge-intensive NLP (RAG) | NeurIPS | 2020 | [Scholar](https://scholar.google.com/scholar?q=Retrieval-augmented%20generation%20knowledge-intensive%20NLP) |
| REALM: retrieval-augmented LM pre-training | ICML | 2020 | [Scholar](https://scholar.google.com/scholar?q=REALM%20retrieval-augmented%20language%20model%20pre-training) |
| Self-RAG: retrieve, critique, generate via self-reflection | ICLR | 2024 | [arXiv](https://arxiv.org/abs/2310.11511) |
| When not to trust language models (parametric vs. non-parametric) | ACL | 2023 | [Scholar](https://scholar.google.com/scholar?q=When%20not%20to%20trust%20language%20models%20parametric%20non-parametric) |
| ROME: locating and editing factual associations in GPT | NeurIPS | 2022 | [Scholar](https://scholar.google.com/scholar?q=locating%20editing%20factual%20associations%20GPT%20ROME) |
| MEMIT: mass-editing memory in a transformer | ICLR | 2023 | [Scholar](https://scholar.google.com/scholar?q=mass-editing%20memory%20transformer%20MEMIT) |
| MEND: fast model editing at scale | ICLR | 2022 | [Scholar](https://scholar.google.com/scholar?q=fast%20model%20editing%20at%20scale%20MEND) |
| Editing factual knowledge in language models (De Cao et al.) | EMNLP | 2021 | [Scholar](https://scholar.google.com/scholar?q=editing%20factual%20knowledge%20language%20models%20De%20Cao) |
| EasyEdit: a knowledge-editing framework | ACL | 2024 | [Scholar](https://scholar.google.com/scholar?q=EasyEdit%20knowledge%20editing%20framework) |
| WISE: lifelong model editing with dual memory | NeurIPS | 2024 | [Scholar](https://scholar.google.com/scholar?q=WISE%20lifelong%20model%20editing) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l2"></a>
## 🔣 Layer 2 — Formalization & Executable Reasoning `inferential trust`

**Does the conclusion *follow* — can a back-end execute or refute it?** The output is not a free-standing answer but a candidate carrying a **verification contract**: a proof state asks for a kernel-checkable proof, a program for passing tests, an equation for a dimensional/data fit. Symbolic roles: **R** representation, **G** generator, **E** engine. This is the one layer where the neuro-symbolic criterion is **saturated** — every classified mechanism couples a neural proposer to a symbolic engine.

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l2-cot"></a>
### Chain-of-Thought & Inference-Time Reasoning (substrate)

Natural-language reasoning and its search / refinement extensions. Readable text **does not entail faithful reasoning** and cannot be examined by a solver, prover or experiment — the weakness the formalization mechanisms below address.

| Title | Venue | Year | Links |
| :-- | :-- | :--: | :-- |
| Chain-of-thought prompting elicits reasoning in LLMs | NeurIPS | 2022 | [Scholar](https://scholar.google.com/scholar?q=Chain-of-thought%20prompting%20elicits%20reasoning) |
| Large language models are zero-shot reasoners | NeurIPS | 2022 | [Scholar](https://scholar.google.com/scholar?q=Large%20language%20models%20are%20zero-shot%20reasoners) |
| Self-consistency improves chain-of-thought reasoning | ICLR | 2023 | [Scholar](https://scholar.google.com/scholar?q=Self-consistency%20improves%20chain%20of%20thought%20reasoning) |
| Tree of Thoughts: deliberate problem solving | NeurIPS | 2023 | [Scholar](https://scholar.google.com/scholar?q=Tree%20of%20thoughts%20deliberate%20problem%20solving) |
| Graph of Thoughts: solving elaborate problems | AAAI | 2024 | [Scholar](https://scholar.google.com/scholar?q=Graph%20of%20thoughts%20solving%20elaborate%20problems) |
| Least-to-most prompting enables complex reasoning | ICLR | 2023 | [Scholar](https://scholar.google.com/scholar?q=Least-to-most%20prompting%20complex%20reasoning) |
| Self-Refine: iterative refinement with self-feedback | NeurIPS | 2023 | [Scholar](https://scholar.google.com/scholar?q=Self-Refine%20iterative%20refinement%20self-feedback) |
| STaR: bootstrapping reasoning with reasoning | NeurIPS | 2022 | [Scholar](https://scholar.google.com/scholar?q=STaR%20bootstrapping%20reasoning%20with%20reasoning) |
| Quiet-STaR: think before speaking | COLM | 2024 | [arXiv](https://arxiv.org/abs/2403.09629) |
| Scaling LLM test-time compute optimally | arXiv | 2024 | [Scholar](https://scholar.google.com/scholar?q=Scaling%20LLM%20test-time%20compute%20optimally) |
| Large language monkeys: scaling inference with repeated sampling | arXiv | 2024 | [Scholar](https://scholar.google.com/scholar?q=Large%20language%20monkeys%20scaling%20inference%20repeated%20sampling) |
| s1: simple test-time scaling | arXiv | 2025 | [Scholar](https://scholar.google.com/scholar?q=s1%20simple%20test-time%20scaling) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l2-form"></a>
### Symbolic Formalization & Autoformalization

Committing the reasoning state to a **persistent symbolic representation** a solver/prover can inspect, and the fast-growing **autoformalization** line that carries informal statements into formal languages — the open problem at the top of mathematics' supervision ladder.

| Title | Roles | T | Year | Links |
| :-- | :--: | :--: | :--: | :-- |
| PAL: program-aided language models | R·G·E | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=PAL%20program-aided%20language%20models) |
| Program of Thoughts (PoT) prompting | R·G·E | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=Program%20of%20thoughts%20prompting%20numerical%20reasoning) |
| CodeAct: executable code actions for LLM agents | R·G·E | T3 | 2024 | [arXiv](https://arxiv.org/abs/2402.01030) |
| Logic-LM: LLMs with symbolic solvers for faithful reasoning | R·E·V | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=Logic-LM%20symbolic%20solvers%20faithful%20logical%20reasoning) |
| LINC: LM + first-order-logic provers | R·E·V | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=LINC%20neurosymbolic%20first-order%20logic%20provers) |
| SatLM: satisfiability-aided language models | R·E·V | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=SatLM%20satisfiability-aided%20language%20models) |
| Faithful chain-of-thought reasoning | R·G | T3 | 2023 | [arXiv](https://arxiv.org/abs/2301.13379) |
| SymbCoT: symbolic chain-of-thought | R·G | T3 | 2024 | [arXiv](https://arxiv.org/abs/2305.13160) |
| SymCode: neuro-symbolic approach to mathematical reasoning | R·G·E | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=SymCode%20neurosymbolic%20mathematical%20reasoning) |
| Autoformalization with large language models | R·G | T4 | 2022 | [Scholar](https://scholar.google.com/scholar?q=autoformalization%20with%20large%20language%20models) |
| StepFun-Formalizer: unlocking autoformalization | R·G | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=StepFun-Formalizer%20autoformalization) |
| Mathesis: formal theorem proving from informal statements | R·G | T4 | 2026 | [Scholar](https://scholar.google.com/scholar?q=Mathesis%20formal%20theorem%20proving%20informal) |
| ATLAS: autoformalizing theorems by lifting | R·G | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=ATLAS%20autoformalizing%20theorems%20lifting) |
| FormaRL: RL for autoformalization with minimal supervision | R·G·V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=FormaRL%20autoformalization%20reinforcement%20learning) |
| M2F: automated formalization of mathematics | R·G | T4 | 2026 | [Scholar](https://scholar.google.com/scholar?q=automated%20formalization%20mathematical%20statements) |
| ReForm: reflective autoformalization | R·G·V | T4 | 2026 | [Scholar](https://scholar.google.com/scholar?q=ReForm%20reflective%20autoformalization) |
| MASA: LLM-driven multi-agent autoformalization | R·G | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=MASA%20multi-agent%20autoformalization) |
| FOLIO / LAMBADA / EntailmentBank (FOL-NLI resources) | — | — | 2021–24 | [Scholar](https://scholar.google.com/scholar?q=FOLIO%20first-order%20logic%20natural%20language%20inference) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l2-synth"></a>
### Program, Algorithm & Law Synthesis

Where a **deterministic evaluator** can score a candidate, generation can be driven hard by search and the generator role secures inferential trust by construction. The generative step transfers everywhere; what does *not* transfer is the verifier.

| Title | Roles | T | Year | Links |
| :-- | :--: | :--: | :--: | :-- |
| FunSearch: mathematical discoveries from program search | R·G·V | T4 | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06924-6) |
| AlphaTensor: discovering faster matrix multiplication | R·G·V | T4 | 2022 | [DOI](https://doi.org/10.1038/s41586-022-05172-4) |
| AlphaDev: faster sorting algorithms via deep RL | R·G·V | T4 | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06004-9) |
| AlphaEvolve: a coding agent for algorithmic discovery | R·G·V | T4 | 2025 | [arXiv](https://arxiv.org/abs/2506.13131) |
| Eureqa: distilling free-form natural laws (symbolic regression) | R·G·V | T2 | 2009 | [DOI](https://doi.org/10.1126/science.1165893) |
| Neural symbolic regression that scales | R·G | T4 | 2021 | [Scholar](https://scholar.google.com/scholar?q=neural%20symbolic%20regression%20that%20scales) |
| SciCode: a research-coding benchmark | — | — | 2024 | [Scholar](https://scholar.google.com/scholar?q=SciCode%20research%20coding%20benchmark%20scientists) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l2-exec"></a>
### Program- & Logic-Aided Execution + Symbolic Back-ends

Delegating computation and deduction to interpreters, SMT solvers, FOL provers and answer-set programs. **No single back-end covers the task spectrum** — its failure mode is what a controller routes over (see Layer 3).

| Title / Back-end | Strong regime | Year | Links |
| :-- | :-- | :--: | :-- |
| IFDNS: iterative feedback-driven neuro-symbolic reasoning | solver-in-the-loop refinement | 2026 | [Scholar](https://scholar.google.com/scholar?q=iterative%20feedback-driven%20neuro-symbolic%20reasoning) |
| Adaptive LLM–symbolic reasoning (solver selection) | per-instance solver choice | 2025 | [Scholar](https://scholar.google.com/scholar?q=adaptive%20LLM%20symbolic%20reasoning%20solver) |
| Z3 / CVC5 | decidable theories; model or counterexample | 2008/22 | [DOI](https://doi.org/10.1007/978-3-540-78800-3_24) |
| Vampire / E | first-order saturation-based proving | 2013/19 | [Scholar](https://scholar.google.com/scholar?q=Vampire%20first-order%20theorem%20proving) |
| Lean / Isabelle/HOL / Coq / Agda | kernel-checked interactive proof | — | [Scholar](https://scholar.google.com/scholar?q=Lean%20theorem%20prover%20kernel) |
| SWI-Prolog | Horn-clause rule chains | 2012 | [DOI](https://doi.org/10.1017/S1471068411000494) |
| Clingo (ASP) | combinatorics, defaults, planning | 2019 | [DOI](https://doi.org/10.1017/S1471068418000054) |
| MiniSat / MiniZinc | propositional & finite-domain solving | 2003/07 | [Scholar](https://scholar.google.com/scholar?q=MiniZinc%20constraint%20modeling) |
| SymPy / Mathematica | exact symbolic computation | — | [Scholar](https://scholar.google.com/scholar?q=SymPy%20symbolic%20computing%20Python) |
| Fast Downward (PDDL) | goal-directed classical planning | 2006 | [Scholar](https://scholar.google.com/scholar?q=Fast%20Downward%20planning%20system) |
| Neuro-symbolic solvers for PDEs / analytic DEs | scientific equation solving | 2022/26 | [Scholar](https://scholar.google.com/scholar?q=neuro-symbolic%20partial%20differential%20equations) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l2-proof"></a>
### Formal Theorem Proving

Coupling neural search with proof assistants (Lean, Isabelle) to reach olympiad-level formal mathematics — the **one science whose verifier is already complete** (within its formalization boundary).

| Title | Roles | T | Year | Links |
| :-- | :--: | :--: | :--: | :-- |
| GPT-f: generative language modeling for theorem proving | R·G | T3 | 2020 | [arXiv](https://arxiv.org/abs/2009.03393) |
| Thor: hammers integrating LMs and ATPs | R·G·E | T3 | 2022 | [Scholar](https://scholar.google.com/scholar?q=Thor%20wielding%20hammers%20language%20models%20theorem%20provers) |
| HyperTree Proof Search (HTPS) | R·G·E | T3 | 2022 | [Scholar](https://scholar.google.com/scholar?q=hypertree%20proof%20search) |
| LeanDojo: retrieval-augmented theorem proving | R·G·E | T3 | 2023 | [arXiv](https://arxiv.org/abs/2306.15626) |
| Lean Copilot: LLMs as copilots for Lean | R·G·E | T3 | 2024 | [arXiv](https://arxiv.org/abs/2404.12534) |
| Llemma: an open LM for mathematics | R·G | T3 | 2024 | [arXiv](https://arxiv.org/abs/2310.10631) |
| DeepSeek-Prover V1.5 / V2 (subgoal-decomposition RL) | R·G·V | T4 | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=DeepSeek-Prover-V2%20subgoal%20decomposition%20Lean) |
| Goedel-Prover: open-source automated theorem proving | R·G·V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=Goedel-Prover%20frontier%20automated%20theorem%20proving) |
| Kimina-Prover-Preview | R·G·V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=Kimina-Prover-Preview) |
| AlphaGeometry / AlphaGeometry2 | R·G·E·V | T3 | 2024/25 | [DOI](https://doi.org/10.1038/s41586-023-06747-5) |
| AlphaProof: RL in a Lean environment | R·G·V·E | T4 | 2026 | [DOI](https://doi.org/10.1038/s41586-025-09833-y) |
| PhysProver: automatic theorem proving in physics | R·G·V | T4 | 2026 | [Scholar](https://scholar.google.com/scholar?q=PhysProver%20automatic%20theorem%20proving%20physics) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l2-diff"></a>
### Differentiable & Abductive Neuro-Symbolic ⭐

Making logic itself **differentiable** so symbolic structure is learned end-to-end — the **tightest coupling** on the Kautz scale (T5–T6), but so far validated mostly on synthetic relational tasks. Scaling it to open scientific reasoning is the depth large-model methods leave empty.

| Title | Roles | T | Year | Links |
| :-- | :--: | :--: | :--: | :-- |
| ∂ILP: learning explanatory rules from noisy data | R·E·G | T6 | 2018 | [Scholar](https://scholar.google.com/scholar?q=learning%20explanatory%20rules%20from%20noisy%20data%20differentiable%20ILP) |
| DeepProbLog: neural probabilistic logic programming | R·E | T6 | 2018 | [Scholar](https://scholar.google.com/scholar?q=DeepProbLog%20neural%20probabilistic%20logic%20programming) |
| NeurASP: neural networks + answer-set programs | R·E | T6 | 2020 | [Scholar](https://scholar.google.com/scholar?q=NeurASP%20embracing%20neural%20networks%20answer%20set%20programming) |
| Logic Tensor Networks | R·E | T6 | 2022 | [Scholar](https://scholar.google.com/scholar?q=Logic%20Tensor%20Networks) |
| Neural Logic Machines | R·E·G | T6 | 2019 | [Scholar](https://scholar.google.com/scholar?q=Neural%20Logic%20Machines) |
| Abductive Learning (ABL): bridging ML and logical reasoning | R·E·V | T6 | 2019 | [Scholar](https://scholar.google.com/scholar?q=abductive%20learning%20bridging%20machine%20learning%20logical%20reasoning) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l3"></a>
## ✅ Layer 3 — Verification, Diagnosis & Adaptive Control `empirical trust`

**Does the candidate hold up under scrutiny — and can we locate *where* it breaks?** This layer adjudicates a candidate's logical, mathematical, scientific and empirical validity, assesses uncertainty, and decides accept / reject / revise — stopping short of acting in the world. A verdict is **new knowledge**: Kₜ₊₁ = Update(Kₜ, V(c)). Symbolic role: **V** (verifier). Scalar process-reward models and LLM-judges carry **no symbolic limb** — they rank a candidate without being able to refute it, and are banded as baselines.

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l3-prm"></a>
### Step-Level Diagnosis & Process Reward

Beyond final-answer accuracy and fuzzy LLM-judges: process supervision localizes *where* a chain breaks. But a process score localizes more than it explains — and models largely **cannot find their own errors, yet can fix them once the location is supplied**.

| Title | Roles | Year | Links |
| :-- | :--: | :--: | :-- |
| Let's Verify Step by Step (PRM800K) | V | 2024 | [Scholar](https://scholar.google.com/scholar?q=Let%27s%20verify%20step%20by%20step) |
| Math-Shepherd: process rewards without per-step labels | V | 2024 | [arXiv](https://arxiv.org/abs/2312.08935) |
| OmegaPRM: automated process supervision | V | 2024 | [Scholar](https://scholar.google.com/scholar?q=improve%20mathematical%20reasoning%20automated%20process%20supervision) |
| ProcessBench: identifying process errors | — | 2024 | [Scholar](https://scholar.google.com/scholar?q=ProcessBench%20identifying%20process%20errors%20mathematical%20reasoning) |
| Hierarchical process reward models | V | 2025 | [Scholar](https://scholar.google.com/scholar?q=hierarchical%20process%20reward%20models) |
| Local look-ahead guidance for verification | V | 2025 | [Scholar](https://scholar.google.com/scholar?q=local%20look-ahead%20guidance%20verifier) |
| OVM: outcome-supervised value models | V | 2024 | [arXiv](https://arxiv.org/abs/2311.09724) |
| Training verifiers to solve math word problems (Cobbe et al.) | V | 2021 | [arXiv](https://arxiv.org/abs/2110.14168) |
| LLMs cannot find reasoning errors, but can correct given location | — | 2024 | [Scholar](https://scholar.google.com/scholar?q=LLMs%20cannot%20find%20reasoning%20errors%20correct%20given%20location) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l3-rlvr"></a>
### Verifier-Guided Learning & Verifiable Rewards (RLVR)

When a verifier exists, its signal can **train the policy**. The boundary of this approach is verifier availability: where none exists, the objectivity of verifiable reward degrades to preference rewards and calibration.

| Title | Roles | T | Year | Links |
| :-- | :--: | :--: | :--: | :-- |
| DeepSeekMath: Group Relative Policy Optimization (GRPO) | V | T4 | 2024 | [arXiv](https://arxiv.org/abs/2402.03300) |
| DeepSeek-R1: incentivizing reasoning via RL | V | T4 | 2025 | [arXiv](https://arxiv.org/abs/2501.12948) |
| OpenAI o1 / o3-mini (verifiable-reward long reasoning) | V | T4 | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=OpenAI%20o1%20learning%20to%20reason%20with%20LLMs) |
| Kimi K1.5: scaling RL with LLMs | V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=Kimi%20K1.5%20scaling%20reinforcement%20learning%20LLMs) |
| Qwen2.5-Math | V | T4 | 2024 | [Scholar](https://scholar.google.com/scholar?q=Qwen2.5-Math%20mathematical%20expert%20model) |
| ReFT: reasoning with reinforced fine-tuning | V | T4 | 2024 | [arXiv](https://arxiv.org/abs/2401.08967) |
| V-STaR: training verifiers for self-taught reasoners | V | T4 | 2024 | [arXiv](https://arxiv.org/abs/2402.06457) |
| Self-rewarding language models | V | T4 | 2024 | [arXiv](https://arxiv.org/abs/2401.10020) |
| Generative verifiers (verify via next-token) | V | T4 | 2024 | [Scholar](https://scholar.google.com/scholar?q=generative%20verifiers%20reward%20modeling%20next-token) |
| DeepSeekMath-V2: self-verifiable mathematical reasoning | V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=DeepSeekMath-V2%20self-verifiable%20mathematical%20reasoning) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l3-route"></a>
### Tool Selection, Routing & Cross-Verification

Generic agent frameworks answer *which tool to call*; scientific reasoning needs more — the controller must **route per instance and cross-verify**, because no single back-end covers the task spectrum. (Thor: PISA solved 39%→57%, +8.2% neither component proves alone.)

| Title | Roles | Year | Links |
| :-- | :--: | :--: | :-- |
| MRKL systems: modular neuro-symbolic architecture | E·V | 2022 | [arXiv](https://arxiv.org/abs/2205.00445) |
| ReAct: synergizing reasoning and acting | A | 2023 | [Scholar](https://scholar.google.com/scholar?q=ReAct%20synergizing%20reasoning%20acting%20language%20models) |
| Toolformer: LMs teach themselves to use tools | A | 2023 | [Scholar](https://scholar.google.com/scholar?q=Toolformer%20language%20models%20teach%20themselves%20tools) |
| Reflexion: verbal reinforcement learning | V | 2023 | [Scholar](https://scholar.google.com/scholar?q=Reflexion%20language%20agents%20verbal%20reinforcement%20learning) |
| AutoGen: multi-agent conversation framework | A | 2024 | [arXiv](https://arxiv.org/abs/2308.08155) |
| MetaGPT: meta-programming for multi-agent collaboration | A | 2024 | [arXiv](https://arxiv.org/abs/2308.00352) |
| SWE-agent: agent–computer interfaces | A | 2024 | [arXiv](https://arxiv.org/abs/2405.15793) |
| Thor (hammer routing) / LeanDojo (retrieval+Lean) | E·V | 2022/23 | [Scholar](https://scholar.google.com/scholar?q=Thor%20hammer%20LeanDojo%20retrieval%20theorem%20proving) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="l3-repair"></a>
### Feedback-Driven Repair

Encoding solver/prover execution traces into **structured feedback** that drives the next step — not just a boolean check. (Baldur: conditioning on a failed proof + error message proves +8.7% of theorems; with the Thor hammer, 65.7% of a 6,336-theorem benchmark fully automatically.)

| Title | Roles | Year | Links |
| :-- | :--: | :--: | :-- |
| Baldur: whole-proof generation and repair with LLMs | V·G | 2023 | [DOI](https://doi.org/10.1145/3611643.3616243) |
| Reliable proof generation with LLMs | V·G | 2025 | [Scholar](https://scholar.google.com/scholar?q=reliable%20proof%20generation%20large%20language%20models) |
| Self-Refine: generate–critique–revise | V·G | 2023 | [Scholar](https://scholar.google.com/scholar?q=Self-Refine%20iterative%20refinement%20self-feedback) |
| CRITIC: self-correcting with tool-interactive critiquing | V | 2024 | [Scholar](https://scholar.google.com/scholar?q=CRITIC%20self-correcting%20tool-interactive%20critiquing) |
| Can LLMs reason about program invariants? | V | 2023 | [Scholar](https://scholar.google.com/scholar?q=can%20large%20language%20models%20reason%20about%20program%20invariants) |
| Do PAL outputs verify what they claim? | V | 2024 | [Scholar](https://scholar.google.com/scholar?q=do%20PAL%20outputs%20verify%20what%20they%20claim) |
| Safe: enhancing mathematical reasoning with formal verification | V | 2025 | [Scholar](https://scholar.google.com/scholar?q=Safe%20enhancing%20mathematical%20reasoning%20formal%20verification) |
| Interleaved formal verification of natural-language reasoning | V | 2026 | [Scholar](https://scholar.google.com/scholar?q=interleaved%20formal%20verification%20natural%20language%20reasoning) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="apps"></a>
## 🔬 Applications across the Sciences — Closing the Loop

This is **not an application catalog but a maturity scan of verification infrastructure**. Walking from the science with the most complete verifier to the least, the loop closes within a formal boundary → closes on a probabilistic verifier → stalls at generation → and **nowhere closes completely**. The transfer gradient: generation reaches every science, while the symbolic-limb rows (formalization, executable reasoning, verification) **fade as the verifier grows scarce**.

```
 mechanism →          formal-math  algo/code  chemistry  materials  life-sci.
 generation             ●            ●           ●          ●          ●
 grounding (RAG,KG)     ◐            ◐           ●          ●          ●
 formalization          ●            ●           ◐          ○          ○
 executable reasoning   ●            ●           ◐          ○          ○
 verification           ●            ●           ○          ○          ○
 control (route/repair) ●            ◐           ◐          ○          ○
                ● established   ◐ partial/emerging   ○ blocked by verifier scarcity
```

<a id="app-math"></a>
### Formal Mathematics & Theorem Proving — *closure within the formal boundary*

Every layer is realized and the loop closes, because the verifier is **deterministic, cheap and diagnostic**: a proof type-checks against a trusted kernel or it does not. Write-back is exact and cumulative (Mathlib). The bound: the kernel certifies only what has been **formalized** — autoformalization remains slow, lossy and unsolved.

| System | Contribution | Year | Links |
| :-- | :-- | :--: | :-- |
| AlphaGeometry | neural construction + deductive engine; 25/30 IMO geometry | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06747-5) |
| AlphaGeometry2 | broader olympiad geometry | 2025 | [Scholar](https://scholar.google.com/scholar?q=AlphaGeometry2%20olympiad%20geometry) |
| AlphaProof | RL inside a general Lean environment | 2026 | [DOI](https://doi.org/10.1038/s41586-025-09833-y) |
| DeepSeek-Prover / Goedel-Prover / Kimina-Prover / Lean Copilot | industrialized end-to-end Lean generation | 2024–25 | [Scholar](https://scholar.google.com/scholar?q=DeepSeek-Prover%20Goedel-Prover%20Kimina-Prover%20Lean) |

<a id="app-algo"></a>
### Algorithm & Code Discovery — *deterministic evaluators, open-ended search*

The verifier loosens from a proof kernel to an **executable evaluator**: a program is run, and its score is the signal. Cheap and unambiguous, so the loop closes — but it measures performance rather than certifying truth, and the residual risk shifts to the **specification gap**.

| System | Contribution | Year | Links |
| :-- | :-- | :--: | :-- |
| FunSearch | LLM proposer + deterministic evaluator; new combinatorial constructions | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06924-6) |
| AlphaTensor / AlphaDev | RL symbolic search for faster algorithms | 2022/23 | [DOI](https://doi.org/10.1038/s41586-022-05172-4) |
| AlphaEvolve | proposer–evaluator generalized to a coding agent | 2025 | [arXiv](https://arxiv.org/abs/2506.13131) |
| Symbolic regression (Eureqa, SINDy, PySR) | fit residual as verifier; interpretable laws | 2009– | [DOI](https://doi.org/10.1126/science.1165893) |
| SciCode | benchmark for scientific code generation | 2024 | [Scholar](https://scholar.google.com/scholar?q=SciCode%20scientific%20code%20generation%20benchmark) |

<a id="app-chem"></a>
### Chemistry & Autonomous Synthesis — *the loop reaches the bench*

The first science where the verifier **leaves the computer and becomes a physical experiment**. Grounding is strong; formalization/execution only partly transfer — a route is plausible on paper but its feasibility is settled only at the bench. Enactment stops being free; what re-enters Knowledge is a **probabilistic measurement**, not a certified fact.

| System | Contribution | Year | Links |
| :-- | :-- | :--: | :-- |
| Coscientist | closes the loop from understanding to execution | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06792-0) |
| ChemCrow | name resolution, retrosynthesis, robot execution as action space | 2024 | [DOI](https://doi.org/10.1038/s42256-024-00832-8) |
| Planning chemical syntheses with DNNs and symbolic AI | retrosynthesis (plausible-on-paper) | 2018 | [DOI](https://doi.org/10.1038/nature25978) |
| Protect: steerable retrosynthesis (neuro-symbolic) | constraint-guided routes | 2026 | [Scholar](https://scholar.google.com/scholar?q=Protect%20steerable%20retrosynthesis%20neuro-symbolic) |
| FragmentRetro: quadratic retrosynthetic method | fragment-based search | 2025 | [Scholar](https://scholar.google.com/scholar?q=FragmentRetro%20quadratic%20retrosynthetic%20method) |
| Robotic flow synthesis / mobile robotic chemist | robotic substrate | 2019/20 | [DOI](https://doi.org/10.1126/science.aax1566) |
| Bayesian reaction optimization | quantitative verifier surrogate | 2021 | [DOI](https://doi.org/10.1038/s41586-021-03213-y) |

<a id="app-mat"></a>
### Materials Discovery — *when the experiment's verifier is itself uncertain*

Where **verifier scarcity becomes the foreground problem**. Prediction is strong (GNoME, MatterGen), but confirming what was synthesized is *itself an inference*. A-Lab made 41/58 targets in 17 days — yet an independent re-analysis disputed several phase assignments. **A mechanically closed loop without a trustworthy verifier is not a trust loop.**

| System | Contribution | Year | Links |
| :-- | :-- | :--: | :-- |
| GNoME | stability prediction at million-candidate scale | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06735-9) |
| MatterGen | generative model of inorganic materials | 2025 | [DOI](https://doi.org/10.1038/s41586-025-08628-5) |
| A-Lab | autonomous synthesis; verifier-of-the-experiment dispute | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06734-w) |
| Machine-learning-assisted discovery using failed experiments | negative results as data | 2016 | [DOI](https://doi.org/10.1038/nature17439) |
| MARS / MedRule-KG / NSGG | neuro-symbolic guarantees for generative proposals | 2024–26 | [Scholar](https://scholar.google.com/scholar?q=neural%20proposals%20symbolic%20guarantees) |

<a id="app-bio"></a>
### The Life Sciences — *prediction without closure*

Where the loop **most often stalls at generation**, despite carrying the field's most celebrated predictors. AlphaFold/ESM3 are predictors no symbolic system checks; validation is a slow, noisy, costly wet-lab assay. Almost nothing is written back as trustworthy knowledge — the **empty lower-right of the heatmap**, and the destination of the research agenda.

| System | Contribution | Year | Links |
| :-- | :-- | :--: | :-- |
| AlphaFold / AlphaFold-3 | near-experimental structure prediction | 2021/24 | [DOI](https://doi.org/10.1038/s41586-021-03819-2) |
| ESM3 | protein evolution in a learned sequence space | 2025 | [DOI](https://doi.org/10.1126/science.ads0018) |
| Boltz-1 | open structure prediction | 2025 | [arXiv](https://arxiv.org/abs/2411.13408) |
| BioDiscoveryAgent / Robin | agentic experiment proposal & interpretation | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=BioDiscoveryAgent%20agent%20experiment%20design) |
| BioProAgent | neuro-symbolic protocol generation under constraints | 2026 | [Scholar](https://scholar.google.com/scholar?q=BioProAgent%20protocol%20generation%20constraints) |
| Antibiotic discovery (Stokes; explainable structural class) | deep-learning candidates validated by assay | 2020/24 | [DOI](https://doi.org/10.1016/j.cell.2020.01.021) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

> **Autonomy is not trust.** A system's position on the autonomy spectrum is set by *the verifier its science admits*, not its engineering ambition: an autonomous laboratory can enact decisions far faster than it can trust their outcomes. Governance, safety and reproducibility of lab-acting agents are the *form trustworthy enactment takes* once the loop reaches the world.

<a id="bench"></a>
## 📊 Benchmarks & Trust-Aligned Evaluation

A trust-centred loop demands evaluation that scores not only *whether* an answer is right but *how* it was obtained. We organize benchmarks by the **trust dimension** they probe. The coverage gradient is stark: inferential trust is densely benchmarked; empirical trust is scored through process/verifier checks but **rarely through independent replication**; epistemic trust (provenance) is barely measured; the practice-closure end is probed only by coarse agentic suites.

| Trust dimension | Representative benchmarks | Coverage |
| :-- | :-- | :--: |
| **Inferential** | MATH · GSM8K · ProofWriter · BIG-Bench Hard · LogicBench · FrontierMath · Humanity's Last Exam · RLMEval · VeriSoftBench | ● dense |
| **Epistemic** | ScienceQA · MMMU · MMMU-Pro · MathVista · MathVerse · LogicVista · OlympiadBench · SciBench · CiteAudit *(provenance, nascent)* | ◐ partial |
| **Empirical** | ProcessBench · VerifyBench · SciCode · Lessons-from-PRMs · ReliableEval · ReplicatorBench *(replication)* | ◐ partial |
| **Practice-closure** *(not a trust dim.)* | AgentBench · ScienceAgentBench · BOLAA · SciAgentGym · FIRE-Bench · BioProBench | coarse only |

| Benchmark | Probes | Year | Links |
| :-- | :-- | :--: | :-- |
| MATH / GSM8K | mathematical problem solving | 2021 | [Scholar](https://scholar.google.com/scholar?q=measuring%20mathematical%20problem%20solving%20MATH%20dataset) |
| ProofWriter | implications, proofs, abduction over NL | 2021 | [Scholar](https://scholar.google.com/scholar?q=ProofWriter%20generating%20implications%20proofs) |
| LogicBench | systematic logical-reasoning evaluation | 2024 | [Scholar](https://scholar.google.com/scholar?q=LogicBench%20systematic%20evaluation%20logical%20reasoning) |
| FrontierMath / Humanity's Last Exam | research-grade reasoning | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=FrontierMath%20benchmark) |
| MMMU / MMMU-Pro | multi-discipline multimodal understanding | 2024 | [Scholar](https://scholar.google.com/scholar?q=MMMU%20massive%20multi-discipline%20multimodal%20understanding) |
| MathVista / MathVerse | visual mathematical reasoning | 2024 | [Scholar](https://scholar.google.com/scholar?q=MathVista%20mathematical%20reasoning%20visual%20contexts) |
| ScienceQA / SciBench / OlympiadBench | scientific & olympiad reasoning | 2022–24 | [arXiv](https://arxiv.org/abs/2307.10635) |
| ProcessBench / VerifyBench | process errors; evaluating the verifiers | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=VerifyBench%20evaluating%20verifiers) |
| SciCode | scientific code generation | 2024 | [Scholar](https://scholar.google.com/scholar?q=SciCode%20benchmark) |
| AgentBench / ScienceAgentBench | agentic & data-driven discovery | 2024/25 | [arXiv](https://arxiv.org/abs/2308.03688) |
| BioProBench | biological-protocol understanding | 2025 | [Scholar](https://scholar.google.com/scholar?q=BioProBench%20biological%20protocol%20understanding) |

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="agenda"></a>
## 🧭 Open Challenges & Research Agenda

The agenda is **two coordinates of the verification-maturity map** — raise *verifiability* toward rigour, and drive *cost* down — until rigorous verification is cheap enough to run **inside** the loop. The empirical sciences need verification **constructed**; the formal sciences need theirs **completed**. The construction material is neuro-symbolic: symbolic components supply executable semantics and constraints; neural components supply learned verifiers and surrogates.

1. **The neural-to-symbolic semantic gap** — distinguishing "UNSAT because false" from "UNSAT because the translation lost a precondition"; a faithfulness certificate for chains, and translation diagnostics that run *alongside* solver diagnostics. *This gap is the formalization boundary itself.*
2. **Knowledge that ages, evidence that conflicts** — coordinating retrieval, editing and post-training so the knowledge frontier moves with the literature without edits rippling into contradiction; persisting multimodal evidence so it is not lost down the chain.
3. **Verifier scarcity & unified multi-solver reasoning** — *the master switch.* Constructing verifiable rewards when the verifier is partial, expensive or probabilistic (model-based/generative verifiers, learned scientific verifiers); multi-backend routing and cross-verification behind one interface.
4. **Trust–utility–cost trade-offs** — cost-aware policies allocating reasoning depth, back-end choice and feedback rounds per instance, conditional on uncertainty and risk.
5. **Falsifiability, reproducibility & governance of autonomous agents** — benchmarks that re-run claimed results and score calibration/abstention; safety and accountability of agents that act in laboratories.

> **Failure modes by domain** — translation infidelity dominates in math/code (verifier scarcity *low*); **evidence decay and verifier scarcity** dominate in chemistry/materials/biology, neither resolved by a better solver. This is why the same loop yields machine-checked certainty in one column and only hedged, experiment-pending claims in another.

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="vmap"></a>
## 🗺️ Verification-Maturity Map

The survey's core contribution: sciences are placed on a two-axis map by the verifier each admits. **The prize is the low-cost, fully-verifiable corner** — reached today only for formalizable claims. Rigor is the target *throughout*; probabilistic verification is the frontier to be made rigorous, **not the destination**.

| Verification regime | Verifiability | Cost | Representative science | Binding bottleneck |
| :-- | :--: | :--: | :-- | :-- |
| Deterministic executable evaluator | ● full | low | Algorithm & code discovery | Specification gap |
| Kernel-checked formal proof | ● full † | high | Formal mathematics (Lean, Coq) | Formalization boundary |
| Approximate learned verifier (w/ abstention) | ◐ semi | low | Emerging across sciences (PRM, Sci-Verifier) | Calibration; no guarantees |
| Consistency & grounding check | ◐ semi | low | Knowledge-grounded QA (RAG, KG) | Checks grounding, not truth |
| Physical experiment / high-fidelity simulator | ◐ semi | high | Chemistry, materials, biology | Cost, noise; not formal |
| None; generation only | ○ none | — | Open ideation; much of life sciences | Hallucination, irreproducibility |

`† formal proof certifies fully but only behind the formalization boundary.`

The agenda is two arrows on this map: **raise weak checks toward rigour, and drive the cost of rigorous verification down** — a *Lean for science*, in aspiration.

<p align="right">(<a href="#readme-top">⬆ back to top</a>)</p>

<a id="contributing"></a>
## 🤝 Contributing

Contributions are very welcome — missing papers, code links and benchmarks! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) and open a Pull Request following the table entry format. When adding a method, please note its **primary layer** (Knowledge / Reasoning / Verification / Application), its **symbolic roles** (K·R·G·E·V·A) and, where it applies, its **Kautz integration depth** (T1–T6).

<a id="citation"></a>
## 📌 Citation

If this repository helps your research, please consider citing the companion survey (coming soon):

```bibtex
@misc{cui2026trustworthy,
  title  = {Toward Trustworthy AI for Science through Neuro-Symbolic Reasoning:
            A Survey and Research Agenda},
  author = {Cui, Wenyao},
  year   = {2026},
  note   = {Manuscript in preparation}
}
```

## ⭐ Star History

<a href="https://star-history.com/#cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning&Date">
  <img src="https://api.star-history.com/svg?repos=cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning&type=Date" width="70%" alt="Star History Chart">
</a>

## 📜 License

The content of this repository (curation and descriptions) is released under [CC BY 4.0](./LICENSE). Copyright of the listed papers belongs to their respective authors and publishers.

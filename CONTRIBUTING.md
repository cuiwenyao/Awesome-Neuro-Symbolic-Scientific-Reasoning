# Contributing Guide · 贡献指南

Thank you for helping make **Awesome Neuro-Symbolic Scientific Reasoning** better!
感谢你帮助完善本仓库！欢迎补充遗漏的论文、代码与基准。

---

## How to contribute · 如何贡献

1. **Fork** this repository and create a branch.
2. Add your entry to the most relevant section of both `README.md` (English) **and** `README_zh.md` (Chinese), keeping the two in sync.
3. Open a **Pull Request** with a short description of what you added and why it fits the section.

> Fork 仓库 → 在 `README.md` 与 `README_zh.md` 的对应章节**同步**添加条目 → 提交 PR 并简要说明。

## Entry format · 条目格式

Each paper is one table row with four columns:

```markdown
| Title | Venue | Year | Links |
| :-- | :-- | :--: | :-- |
| Logic-LM: empowering large language models with symbolic solvers for faithful logical reasoning | Findings EMNLP | 2023 | [DOI](https://doi.org/10.18653/v1/2023.findings-emnlp.248) [Code](https://github.com/...) |
```

Rules · 规则:

- **Title** — the exact paper title (no trailing period). 论文准确标题，结尾不加句号。
- **Venue** — short form (e.g. `NeurIPS`, `ICLR`, `Nature`, `Findings EMNLP`). 会议/期刊简称。
- **Year** — four-digit year. 四位年份。
- **Links** — prefer a stable link: `[arXiv](...)`, `[DOI](...)`, then `[Code](...)` if available. Avoid fabricated URLs. 优先稳定链接，切勿杜撰 URL。

## Which section? · 归入哪个章节？

We organise papers by the survey's **three-layer trust pipeline** (which closes into a loop):

| Layer | Trust dimension | Question it answers | Section |
| :-- | :-- | :-- | :-- |
| **Knowledge** | epistemic | Does the knowledge carry provenance, currency & a confidence it can be checked against? | Layer 1 — Knowledge Grounding |
| **Reasoning** | inferential | Does the conclusion *follow* — can a back-end execute or refute it? | Layer 2 — Formalization & Executable Reasoning |
| **Verification** | empirical | Does the candidate hold up under scrutiny — and where does it break? | Layer 3 — Verification, Diagnosis & Adaptive Control |
| **Application** | (practice closure) | Does verification close the loop in a given science? | Applications across the Sciences |

When adding a method, please also note its **symbolic roles** (K grounder · R representation · G generator · E engine · V verifier · A actuator) and, where it applies, its **Kautz integration depth** (T1 loosest → T6 tightest).

Foundational solvers, surveys, AI-for-Science milestones and evaluation suites have their own top-level sections. If unsure, propose a placement in your PR and we'll discuss.

> 若不确定归类，请在 PR 中说明你倾向的章节，我们一起讨论。

## Quality bar · 收录标准

- Peer-reviewed papers, well-cited preprints, influential technical reports, or widely-used benchmarks/tools.
- Directly relevant to **neuro-symbolic** reasoning, **verifiable** reasoning, or **scientific** reasoning with LLMs.
- No duplicate entries; keep tables alphabetical-by-relevance within a subsection (roughly chronological / by importance is fine).

Thanks again — every PR is appreciated! 🙏

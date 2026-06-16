<a id="readme-top"></a>

<div align="center">

# 🧠🔣 Awesome Neuro-Symbolic Scientific Reasoning [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

**面向「可信赖科学 AI」的神经符号推理论文与资源精选**

[![Awesome](https://img.shields.io/badge/Awesome-NeSy_SciReason-7B68EE?logo=awesomelists&logoColor=white)](https://github.com/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![Stars](https://img.shields.io/github/stars/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning?style=social)](https://github.com/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning?color=blue)](https://github.com/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning/commits)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](./LICENSE)
[![arXiv](https://img.shields.io/badge/arXiv-coming_soon-b31b1b.svg)](https://github.com/cuiwenyao/Awesome-Neuro-Symbolic-Scientific-Reasoning)

[**English**](./README.md) ｜ **290+** 篇文献 · **143** 个已分类神经符号方法

</div>

---

> **本仓库** 配套综述 *Toward Trustworthy AI for Science through Neuro-Symbolic Reasoning: A Survey and Research Agenda*。它收录那些把大模型推理从**「流畅但不可验证」**变为**「可追溯、可诊断、可修复」**的工作，并围绕一条**三层信任流水线**组织——**知识(Knowledge) → 推理(Reasoning) → 验证(Verification)**——这条流水线最终闭合成一个**回路**：一条被验证的论断重新进入知识库，成为下一步可以依靠的新知识。
>
> **核心论点。** 可信赖科学 AI 的瓶颈**不在生成而在验证**——验证是把每个候选转化为可信知识的「闸门」。迄今没有任何一门科学拥有完整、可执行、低成本且可诊断的验证器，而神经符号推理正是构建并补全它的主要手段：**一个「为科学而生的 Lean」（理想形态）。**

## 🗺️ 框架一览

流水线沿一条主干构建可信赖的科学论断，每一层恰好赢得**一个信任维度**（一一对应）。被验证的论断本身就是新的、可追溯、可检查、可更新的知识，因此流水线**在认识论意义上闭合——通过验证而非通过自动化**，且只在验证可信的范围内闭合。

```
            认识论(epistemic)    推理(inferential)      经验(empirical)
        ┌───────────────┐   ┌───────────────────┐   ┌─────────────────┐
   ┌───►│   知识 KNOW.   ├──►│   推理 REASONING  ├──►│  验证 VERIF.    ├──┐
   │    │   证据接地     │   │  形式化 + 可执行  │   │  诊断 / 修复    │  │
   │    └───────────────┘   └───────────────────┘   └─────────────────┘  │
   │      K·接地器           R·表示                    V·验证器           │
   │                         G·生成器                                     │
   │                         E·引擎                      A·执行器         │
   │                                                                      │
   └────────  验证结果写回知识库：Kₜ → Kₜ₊₁  ◄──────────────────────────┘
                  （证书 · 反例 · 测量值 · 不确定度）

    「实施(Enactment)」（在真实世界中行动）是这条回路的实践闭合属性
    （逐学科考察），而不是第四个信任维度。
```

**六个横切的符号角色**（多标签）：**K** 知识接地器 · **R** 表示 · **G** 生成器 · **E** 引擎 · **V** 验证器 · **A** 执行器。方法另按 **Kautz 集成深度** 标注（T1 最松 → T6 最紧）。

**验证成熟度是组织全局的变量。** 各门科学的差别在于它能容许的验证器，沿两个轴度量——**可验证性**（机械检查能认证多少）与每次裁决的**代价**。终点是「低成本、完全严格」的角落；今天只有可形式化的论断（代码、数学）能到达。见[验证成熟度地图](#vmap)。

## 📢 更新

- **2026-06** ｜ 🔁 配合综述重写进行大改：从以工具为中心的三层视角，改为 **知识–推理–验证 信任流水线 + 回路**，新增 **跨学科应用** 一章、**验证成熟度地图**，以及按信任维度组织的基准评测。
- **2026-06** ｜ 🎉 仓库上线，收录 **290+** 篇文献、**143** 个已分类神经符号方法。
- ⭐ 配套综述正在准备中，arXiv 链接即将放出。

## 📑 目录

<details open>

- [🧱 神经符号 AI 的基石](#foundations)
- [📚 相关综述与立场论文](#surveys)
- [🧪 科学 AI 里程碑](#milestones)
- [🧩 第一层 — 知识接地 `认识论`](#l1)
  - [检索、知识图谱与编辑](#l1-rag)
  - [符号化领域知识、规则与因果先验](#l1-rules)
  - [知识更新与记忆](#l1-mem)
  - [纯神经基线](#l1-base)
- [🔣 第二层 — 形式化与可执行推理 `推理`](#l2)
  - [思维链与推理期推理（基底）](#l2-cot)
  - [符号形式化与自动形式化](#l2-form)
  - [程序、算法与定律合成](#l2-synth)
  - [程序/逻辑辅助执行 + 符号后端](#l2-exec)
  - [形式化定理证明](#l2-proof)
  - [可微与溯因神经符号 ⭐](#l2-diff)
- [✅ 第三层 — 验证、诊断与自适应控制 `经验`](#l3)
  - [步级诊断与过程奖励](#l3-prm)
  - [验证器引导学习与可验证奖励（RLVR）](#l3-rlvr)
  - [工具选择、路由与交叉验证](#l3-route)
  - [反馈驱动的修复](#l3-repair)
- [🔬 跨学科应用 — 闭合回路](#apps)
  - [形式数学与定理证明 — *形式边界内的闭合*](#app-math)
  - [算法与代码发现 — *确定性评估器*](#app-algo)
  - [化学与自主合成 — *回路抵达实验台*](#app-chem)
  - [材料发现 — *当验证器本身不确定*](#app-mat)
  - [生命科学 — *有预测，无闭合*](#app-bio)
- [📊 基准与信任对齐评测](#bench)
- [🧭 开放挑战与研究议程](#agenda)
- [🗺️ 验证成熟度地图](#vmap)
- [🤝 贡献](#contributing)
- [📌 引用](#citation)

</details>

<a id="foundations"></a>
## 🧱 神经符号 AI 的基石

经典符号引擎、认知架构，以及可微神经符号谱系——今天的大模型流水线仍把它们当作验证器、求解器与推理后端来使用。

| 标题 | 出处 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| DENDRAL：第一个专家系统的案例研究 | Book (Stanford) | 1980 | [Scholar](https://scholar.google.com/scholar?q=DENDRAL%20case%20study%20expert%20system) |
| MYCIN：基于计算机的医学会诊 | Elsevier | 1976 | [Scholar](https://scholar.google.com/scholar?q=MYCIN%20computer-based%20medical%20consultations) |
| 表征知识的框架（frames） | MIT AI Memo | 1974 | [Scholar](https://scholar.google.com/scholar?q=Minsky%20framework%20for%20representing%20knowledge) |
| CYC：大规模知识基础设施投资 | CACM | 1995 | [Scholar](https://scholar.google.com/scholar?q=CYC%20large-scale%20investment%20knowledge%20infrastructure) |
| SOAR：通用智能架构 | Artificial Intelligence | 1987 | [Scholar](https://scholar.google.com/scholar?q=SOAR%20architecture%20for%20general%20intelligence) |
| 心智的整合理论（ACT-R） | Psychological Review | 2004 | [Scholar](https://scholar.google.com/scholar?q=integrated%20theory%20of%20the%20mind%20ACT-R) |
| 谓词逻辑作为编程语言 | IFIP | 1974 | [Scholar](https://scholar.google.com/scholar?q=Kowalski%20predicate%20logic%20as%20programming%20language) |
| Z3：高效 SMT 求解器 | TACAS | 2008 | [DOI](https://doi.org/10.1007/978-3-540-78800-3_24) |
| SWI-Prolog | TPLP | 2012 | [DOI](https://doi.org/10.1017/S1471068411000494) |
| 基于 clingo 的多轮 ASP 求解 | TPLP | 2019 | [DOI](https://doi.org/10.1017/S1471068418000054) |
| 从实验数据蒸馏自由形式的自然定律 | Science | 2009 | [DOI](https://doi.org/10.1126/science.1165893) |
| 神经符号 AI 的第三波（Kautz 分类法） | AI Magazine / 综述 | 2023 | [Scholar](https://scholar.google.com/scholar?q=neurosymbolic%20AI%20third%20wave%20Garcez%20Lamb) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="surveys"></a>
## 📚 相关综述与立场论文

神经符号、RAG、知识图谱、智能体、推理模型、科学 AI 这几支文献各有成熟综述，但每篇只固定单一轴线，对验证、反馈与闭合实验回路往往一带而过。**没有任何先前综述同时覆盖「神经符号推理 × 科学」交叉、验证、闭合回路、信任维度与跨域迁移。** 最接近的邻居以「理解–生成–验证」三元组解读数学推理 AI——那正是我们流水线在「唯一已拥有完整验证器的科学」上的特例。

| 综述 | 出处 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| 面向 LLM 推理的神经符号 AI | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=neuro-symbolic%20AI%20for%20LLM%20reasoning%20survey) |
| LLM 符号推理 | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=large%20language%20model%20symbolic%20reasoning%20survey) |
| 神经符号系统的设计模式 | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=design%20patterns%20neuro-symbolic%20systems) |
| 整合式 vs 混合式神经符号 AI | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=integrative%20hybrid%20neuro-symbolic%20comparative) |
| 从 System 1 到 System 2：推理型 LLM 综述 | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=System%201%20to%20System%202%20reasoning%20LLM%20survey) |
| 科学发现：从自动化到自主 | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=automation%20to%20autonomy%20scientific%20discovery%20LLM) |
| 迈向科学智能：基于 LLM 的科学智能体 | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=LLM-based%20scientific%20agents%20survey%20scientific%20intelligence) |
| 用于科学发现的智能体式 AI | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=agentic%20AI%20scientific%20discovery%20survey) |
| 迈向大型推理模型：强化推理 | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=towards%20large%20reasoning%20models%20reinforced%20survey) |
| 科学智能体「漫游指南」 | 综述 | 2025 | [Scholar](https://scholar.google.com/scholar?q=hitchhiker%20guide%20scientific%20agents%20survey) |
| 面向数学推理的人工智能（三元组 + 监督阶梯） | 综述 | 2026 | [Scholar](https://scholar.google.com/scholar?q=artificial%20intelligence%20for%20mathematical%20reasoning%20survey%202026) |
| 人工智能时代的科学发现 | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06221-2) |
| 自然语言生成中的幻觉综述 | ACM Computing Surveys | 2023 | [DOI](https://doi.org/10.1145/3571730) |
| 统一大语言模型与知识图谱：路线图 | IEEE TKDE | 2024 | [DOI](https://doi.org/10.1109/TKDE.2024.3352100) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="milestones"></a>
## 🧪 科学 AI 里程碑

学习与搜索、符号结构或形式验证相遇、在真实科学中跨越「可解」阈值的标志性系统。其中许多是强大的**纯神经预测器**——在此作为综述意图「桥接通往」可验证回路的科学 AI 背景而收录。

| 标题 | 出处 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| 用深度神经网络与树搜索掌握围棋 | Nature | 2016 | [DOI](https://doi.org/10.1038/nature16961) |
| 无需人类知识掌握围棋 | Nature | 2017 | [DOI](https://doi.org/10.1038/nature24270) |
| AlphaFold：高精度蛋白质结构预测 | Nature | 2021 | [DOI](https://doi.org/10.1038/s41586-021-03819-2) |
| AlphaFold 3：生物分子相互作用结构预测 | Nature | 2024 | [DOI](https://doi.org/10.1038/s41586-024-07487-w) |
| Boltz-1：AlphaFold-3 级开源结构预测 | Nature Methods | 2025 | [arXiv](https://arxiv.org/abs/2411.13408) |
| 无需人类演示求解奥数几何（AlphaGeometry） | Nature | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06747-5) |
| 通过程序搜索发现数学（FunSearch） | Nature | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06924-6) |
| AlphaEvolve：科学与算法发现的编码智能体 | arXiv | 2025 | [arXiv](https://arxiv.org/abs/2506.13131) |
| 用 RL 发现更快矩阵乘法（AlphaTensor） | Nature | 2022 | [DOI](https://doi.org/10.1038/s41586-022-05172-4) |
| 用深度 RL 发现更快排序算法（AlphaDev） | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06004-9) |
| 用 RL 进行奥数级形式数学推理（AlphaProof） | Nature | 2026 | [DOI](https://doi.org/10.1038/s41586-025-09833-y) |
| 规模化深度学习用于材料发现（GNoME） | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06735-9) |
| 无机材料设计的生成模型（MatterGen） | Nature | 2025 | [DOI](https://doi.org/10.1038/s41586-025-08628-5) |
| 用语言模型模拟 5 亿年进化（ESM3） | Science | 2025 | [DOI](https://doi.org/10.1126/science.ads0018) |
| 用大语言模型进行自主化学研究（Coscientist） | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06792-0) |
| 加速合成新材料的自主实验室（A-Lab） | Nature | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06734-w) |
| 抗生素发现的深度学习方法 | Cell | 2020 | [DOI](https://doi.org/10.1016/j.cell.2020.01.021) |
| 用可解释深度学习发现一类结构性抗生素 | Nature | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06887-8) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l1"></a>
## 🧩 第一层 — 知识接地 `认识论信任`

**模型据以推理的知识是否带有可被对照检查的来源、时效与置信度？** 回路在此开启——把证据外化为带溯源信息、后端可检视的符号形式；它也在此闭合——被验证的结果（证书、反例、带不确定度的测量值）写回，使知识库从 Kₜ 增长到 Kₜ₊₁。符号角色：**K**（接地器）。关键分野：外化后的知识要么带有验证器日后可检视的**符号肢体**，要么只改变模型所看到的文本（沦为基线）。

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l1-rag"></a>
### 检索、知识图谱与编辑

带符号肢体的图结构检索、知识图谱/规则接地——这些才进入分类树。

| 标题 | 角色 | T | 年份 | 链接 |
| :-- | :--: | :--: | :--: | :-- |
| GraphRAG：从局部到全局的图式摘要 | K·R | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=From%20local%20to%20global%20graph%20RAG%20query-focused%20summarization) |
| HippoRAG：受神经生物学启发的长期记忆 | K·R·G | T3 | 2024 | [arXiv](https://arxiv.org/abs/2405.14831) |
| LightRAG：简单快速的检索增强生成 | K·R | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=LightRAG%20simple%20fast%20retrieval-augmented%20generation) |
| 用于检索增强生成的神经符号检索器 | K·R | T3 | 2026 | [Scholar](https://scholar.google.com/scholar?q=neuro-symbolic%20retrievers%20retrieval-augmented%20generation) |
| QA-GNN：联合 LM 与知识图谱推理 | K·E | T5 | 2021 | [Scholar](https://scholar.google.com/scholar?q=QA-GNN%20reasoning%20language%20models%20knowledge%20graphs) |
| K-Adapter：用适配器向模型注入知识 | K·R | T5 | 2021 | [Scholar](https://scholar.google.com/scholar?q=K-Adapter%20infusing%20knowledge%20pre-trained%20models%20adapters) |
| Think-on-Graph：在知识图谱上深度负责任推理 | K·R·E | T3 | 2024 | [arXiv](https://arxiv.org/abs/2307.07697) |
| 统一大模型与知识图谱：路线图 | — | — | 2024 | [DOI](https://doi.org/10.1109/TKDE.2024.3352100) |
| 知识图谱上的统一神经符号推理 | K·R·E | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=unified%20neurosymbolic%20reasoning%20knowledge%20graphs) |
| 动态知识图谱的神经符号方法（综述） | K·R | — | 2024 | [Scholar](https://scholar.google.com/scholar?q=neurosymbolic%20methods%20dynamic%20knowledge%20graphs%20survey) |
| NeuSTIP：时序知识图谱补全的神经符号模型 | K·R·E | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=NeuSTIP%20neuro-symbolic%20temporal%20knowledge%20graph) |
| CLAUSE：智能体式神经符号 KG 上下文工程 | K·R·E | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=CLAUSE%20agentic%20neurosymbolic%20knowledge%20graph) |
| R2-KG：双智能体可靠 KG 推理 | K·R·V | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=R2-KG%20dual-agent%20reliable%20knowledge%20graph%20reasoning) |
| SymAgent：神经符号自学习 KG 智能体 | K·R·G·E | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=SymAgent%20neural-symbolic%20self-learning%20agent%20knowledge%20graph) |
| Logic Query of Thoughts：KG 接地的逻辑查询 | K·R·E | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=Logic%20Query%20of%20Thoughts%20knowledge%20graph) |
| 逻辑感知课程微调的 KG 推理 | K·R | T4 | 2024 | [Scholar](https://scholar.google.com/scholar?q=logic-aware%20curriculum%20tuning%20knowledge%20graph%20reasoning) |
| OneEdit：神经符号协同知识编辑 | K·R | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=OneEdit%20neural-symbolic%20collaborative%20knowledge%20editing) |
| 动态知识图谱上的多跳知识编辑 | K·R | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=knowledge%20editing%20dynamic%20knowledge%20graphs%20multi-hop) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l1-rules"></a>
### 符号化领域知识、规则与因果先验

科学知识以**可执行的特征函数、规则与约束**进入推理——这才使求解器日后能*检查*而非仅*复述*一条论断。

| 标题 | 角色 | T | 年份 | 链接 |
| :-- | :--: | :--: | :--: | :-- |
| LLM4SD：大模型作为科学发现者（文献+数据规则） | K·R·G | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=LLM4SD%20large%20language%20models%20scientific%20discovery%20rules) |
| 本体引导的神经符号数学 RAG | K | T3 | 2026 | [Scholar](https://scholar.google.com/scholar?q=ontology-guided%20neuro-symbolic%20mathematics%20RAG) |
| 用本体推理增强大模型（OWL + 推理机） | K·R·E·V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=enhancing%20large%20language%20models%20ontological%20reasoning%20OWL) |
| ChatRule：用 LLM 为 KG 挖掘逻辑规则 | K·R·G | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=ChatRule%20mining%20logical%20rules%20knowledge%20graph) |
| 面向 NS-KGC 的逻辑规则简单增强 | R·E | T5 | 2024 | [Scholar](https://scholar.google.com/scholar?q=simple%20augmentations%20logical%20rules%20neuro-symbolic%20knowledge%20graph) |
| LogicMP：将 FOL 约束作为可微神经层 | R·E | T6 | 2023 | [Scholar](https://scholar.google.com/scholar?q=LogicMP%20neurosymbolic%20encoding%20first-order%20constraints) |
| KG 逻辑查询的神经符号模型 | R·E | T6 | 2022 | [Scholar](https://scholar.google.com/scholar?q=neural%20symbolic%20models%20logical%20queries%20knowledge%20graph) |
| Uni-Mol：通用 3D 分子表示框架 | R | T5 | 2023 | [Scholar](https://scholar.google.com/scholar?q=Uni-Mol%20universal%203D%20molecular%20representation) |
| MolCLR：基于 GNN 的分子对比学习 | R | T5 | 2022 | [DOI](https://doi.org/10.1038/s42256-022-00447-x) |
| Molecular Transformer：基于 SMILES 的反应预测 | R·G | T5 | 2019 | [DOI](https://doi.org/10.1021/acscentsci.9b00576) |
| MoleculeNet：分子机器学习基准 | — | — | 2018 | [DOI](https://doi.org/10.1039/C7SC02664A) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l1-mem"></a>
### 知识更新与记忆

可信的知识库必须**随时间变化**——接地是作用在 Kₜ 上的更新算子，也是回路把验证产物送回的地方。仅靠权重编辑没有符号肢体来保持知识库一致。

| 标题 | 角色 | T | 年份 | 链接 |
| :-- | :--: | :--: | :--: | :-- |
| 用于规则推理的符号工作记忆 | K·R·E | T4 | 2024 | [Scholar](https://scholar.google.com/scholar?q=symbolic%20working%20memory%20large%20language%20model%20rule%20reasoning) |
| AriGraph：智能体的知识图谱世界模型记忆 | K·R | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=AriGraph%20knowledge%20graph%20world%20model%20memory) |
| RecallM：可适应的时序图记忆 | K·R | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=RecallM%20adaptable%20memory%20temporal%20understanding) |
| 规则级知识编辑（RuleEdit 基准） | — | — | 2026 | [Scholar](https://scholar.google.com/scholar?q=RuleEdit%20benchmarking%20rule-level%20knowledge%20editing) |
| MemoryBank：大模型的长期记忆 | K | T3 | 2024 | [Scholar](https://scholar.google.com/scholar?q=MemoryBank%20long-term%20memory%20large%20language%20models) |
| 面向语言模型的持续知识学习 | K | — | 2022 | [Scholar](https://scholar.google.com/scholar?q=towards%20continual%20knowledge%20learning%20language%20models) |
| 评估知识编辑的涟漪效应 | — | — | 2023 | [Scholar](https://scholar.google.com/scholar?q=evaluating%20ripple%20effects%20knowledge%20editing) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l1-base"></a>
### 纯神经基线

只改变模型所见文本/事实、**不带符号肢体**的检索与权重编辑——作为基线记录，不进入神经符号分类树。

| 标题 | 出处 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| 知识密集型 NLP 的检索增强生成（RAG） | NeurIPS | 2020 | [Scholar](https://scholar.google.com/scholar?q=Retrieval-augmented%20generation%20knowledge-intensive%20NLP) |
| REALM：检索增强的 LM 预训练 | ICML | 2020 | [Scholar](https://scholar.google.com/scholar?q=REALM%20retrieval-augmented%20language%20model%20pre-training) |
| Self-RAG：自反思的检索-批判-生成 | ICLR | 2024 | [arXiv](https://arxiv.org/abs/2310.11511) |
| 何时不该信任语言模型（参数 vs 非参数记忆） | ACL | 2023 | [Scholar](https://scholar.google.com/scholar?q=When%20not%20to%20trust%20language%20models%20parametric%20non-parametric) |
| ROME：定位并编辑 GPT 的事实关联 | NeurIPS | 2022 | [Scholar](https://scholar.google.com/scholar?q=locating%20editing%20factual%20associations%20GPT%20ROME) |
| MEMIT：在 transformer 中批量编辑记忆 | ICLR | 2023 | [Scholar](https://scholar.google.com/scholar?q=mass-editing%20memory%20transformer%20MEMIT) |
| MEND：规模化的快速模型编辑 | ICLR | 2022 | [Scholar](https://scholar.google.com/scholar?q=fast%20model%20editing%20at%20scale%20MEND) |
| 编辑语言模型中的事实知识（De Cao 等） | EMNLP | 2021 | [Scholar](https://scholar.google.com/scholar?q=editing%20factual%20knowledge%20language%20models%20De%20Cao) |
| EasyEdit：知识编辑框架 | ACL | 2024 | [Scholar](https://scholar.google.com/scholar?q=EasyEdit%20knowledge%20editing%20framework) |
| WISE：双记忆的终身模型编辑 | NeurIPS | 2024 | [Scholar](https://scholar.google.com/scholar?q=WISE%20lifelong%20model%20editing) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l2"></a>
## 🔣 第二层 — 形式化与可执行推理 `推理信任`

**结论是否真的「成立」——后端能否执行或反驳它？** 输出不是独立的答案，而是携带**验证契约**的候选：证明态要求核可的证明，程序要求通过测试，方程要求量纲与数据拟合。符号角色：**R** 表示、**G** 生成器、**E** 引擎。这是神经符号判据**唯一被饱和满足**的一层——每个被分类的机制都把神经提议器耦合到符号引擎。

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l2-cot"></a>
### 思维链与推理期推理（基底）

自然语言推理及其搜索/精炼扩展。可读的文本**并不蕴含忠实的推理**，也无法被求解器、证明器或实验检视——这正是下面的形式化机制要解决的弱点。

| 标题 | 出处 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| 思维链提示激发大模型推理 | NeurIPS | 2022 | [Scholar](https://scholar.google.com/scholar?q=Chain-of-thought%20prompting%20elicits%20reasoning) |
| 大模型是零样本推理器 | NeurIPS | 2022 | [Scholar](https://scholar.google.com/scholar?q=Large%20language%20models%20are%20zero-shot%20reasoners) |
| 自一致性改进思维链推理 | ICLR | 2023 | [Scholar](https://scholar.google.com/scholar?q=Self-consistency%20improves%20chain%20of%20thought%20reasoning) |
| 思维树（ToT）：审慎式问题求解 | NeurIPS | 2023 | [Scholar](https://scholar.google.com/scholar?q=Tree%20of%20thoughts%20deliberate%20problem%20solving) |
| 思维图（GoT）：求解复杂问题 | AAAI | 2024 | [Scholar](https://scholar.google.com/scholar?q=Graph%20of%20thoughts%20solving%20elaborate%20problems) |
| 由少到多提示实现复杂推理 | ICLR | 2023 | [Scholar](https://scholar.google.com/scholar?q=Least-to-most%20prompting%20complex%20reasoning) |
| Self-Refine：带自反馈的迭代精炼 | NeurIPS | 2023 | [Scholar](https://scholar.google.com/scholar?q=Self-Refine%20iterative%20refinement%20self-feedback) |
| STaR：用推理自举推理 | NeurIPS | 2022 | [Scholar](https://scholar.google.com/scholar?q=STaR%20bootstrapping%20reasoning%20with%20reasoning) |
| Quiet-STaR：说话前先思考 | COLM | 2024 | [arXiv](https://arxiv.org/abs/2403.09629) |
| 最优地扩展 LLM 测试期计算 | arXiv | 2024 | [Scholar](https://scholar.google.com/scholar?q=Scaling%20LLM%20test-time%20compute%20optimally) |
| 大型语言「猴子」：重复采样扩展推理计算 | arXiv | 2024 | [Scholar](https://scholar.google.com/scholar?q=Large%20language%20monkeys%20scaling%20inference%20repeated%20sampling) |
| s1：简单的测试期扩展 | arXiv | 2025 | [Scholar](https://scholar.google.com/scholar?q=s1%20simple%20test-time%20scaling) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l2-form"></a>
### 符号形式化与自动形式化

把推理态固化为求解器/证明器可检视的**持久符号表示**，以及快速增长的**自动形式化**支线——把非形式陈述带入形式语言，正是数学监督阶梯顶端的开放问题。

| 标题 | 角色 | T | 年份 | 链接 |
| :-- | :--: | :--: | :--: | :-- |
| PAL：程序辅助语言模型 | R·G·E | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=PAL%20program-aided%20language%20models) |
| 思维程序（PoT）提示 | R·G·E | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=Program%20of%20thoughts%20prompting%20numerical%20reasoning) |
| CodeAct：LLM 智能体的可执行代码动作 | R·G·E | T3 | 2024 | [arXiv](https://arxiv.org/abs/2402.01030) |
| Logic-LM：用符号求解器实现忠实逻辑推理 | R·E·V | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=Logic-LM%20symbolic%20solvers%20faithful%20logical%20reasoning) |
| LINC：LM + 一阶逻辑证明器 | R·E·V | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=LINC%20neurosymbolic%20first-order%20logic%20provers) |
| SatLM：可满足性辅助语言模型 | R·E·V | T3 | 2023 | [Scholar](https://scholar.google.com/scholar?q=SatLM%20satisfiability-aided%20language%20models) |
| 忠实思维链推理 | R·G | T3 | 2023 | [arXiv](https://arxiv.org/abs/2301.13379) |
| SymbCoT：符号思维链 | R·G | T3 | 2024 | [arXiv](https://arxiv.org/abs/2305.13160) |
| SymCode：数学推理的神经符号方法 | R·G·E | T3 | 2025 | [Scholar](https://scholar.google.com/scholar?q=SymCode%20neurosymbolic%20mathematical%20reasoning) |
| 用大模型自动形式化 | R·G | T4 | 2022 | [Scholar](https://scholar.google.com/scholar?q=autoformalization%20with%20large%20language%20models) |
| StepFun-Formalizer：解锁自动形式化 | R·G | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=StepFun-Formalizer%20autoformalization) |
| Mathesis：从非形式陈述到形式定理证明 | R·G | T4 | 2026 | [Scholar](https://scholar.google.com/scholar?q=Mathesis%20formal%20theorem%20proving%20informal) |
| ATLAS：通过提升自动形式化定理 | R·G | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=ATLAS%20autoformalizing%20theorems%20lifting) |
| FormaRL：少监督自动形式化的 RL | R·G·V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=FormaRL%20autoformalization%20reinforcement%20learning) |
| M2F：数学的自动形式化 | R·G | T4 | 2026 | [Scholar](https://scholar.google.com/scholar?q=automated%20formalization%20mathematical%20statements) |
| ReForm：反思式自动形式化 | R·G·V | T4 | 2026 | [Scholar](https://scholar.google.com/scholar?q=ReForm%20reflective%20autoformalization) |
| MASA：LLM 驱动的多智能体自动形式化 | R·G | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=MASA%20multi-agent%20autoformalization) |
| FOLIO / LAMBADA / EntailmentBank（FOL-NLI 资源） | — | — | 2021–24 | [Scholar](https://scholar.google.com/scholar?q=FOLIO%20first-order%20logic%20natural%20language%20inference) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l2-synth"></a>
### 程序、算法与定律合成

只要存在**确定性评估器**给候选打分，生成就能被搜索强力驱动，生成器角色因而以构造方式赢得推理信任。生成这一步无处不可迁移；**不能迁移的是验证器**。

| 标题 | 角色 | T | 年份 | 链接 |
| :-- | :--: | :--: | :--: | :-- |
| FunSearch：通过程序搜索的数学发现 | R·G·V | T4 | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06924-6) |
| AlphaTensor：发现更快矩阵乘法 | R·G·V | T4 | 2022 | [DOI](https://doi.org/10.1038/s41586-022-05172-4) |
| AlphaDev：用深度 RL 发现更快排序 | R·G·V | T4 | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06004-9) |
| AlphaEvolve：算法发现的编码智能体 | R·G·V | T4 | 2025 | [arXiv](https://arxiv.org/abs/2506.13131) |
| Eureqa：蒸馏自由形式自然定律（符号回归） | R·G·V | T2 | 2009 | [DOI](https://doi.org/10.1126/science.1165893) |
| 可规模化的神经符号回归 | R·G | T4 | 2021 | [Scholar](https://scholar.google.com/scholar?q=neural%20symbolic%20regression%20that%20scales) |
| SciCode：科研编码基准 | — | — | 2024 | [Scholar](https://scholar.google.com/scholar?q=SciCode%20research%20coding%20benchmark%20scientists) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l2-exec"></a>
### 程序/逻辑辅助执行 + 符号后端

把计算与演绎交给解释器、SMT 求解器、FOL 证明器与回答集程序。**没有单一后端覆盖整个任务谱**——其失败模式正是控制器要路由的对象（见第三层）。

| 标题 / 后端 | 擅长域 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| IFDNS：迭代反馈驱动的神经符号推理 | 求解器在环精炼 | 2026 | [Scholar](https://scholar.google.com/scholar?q=iterative%20feedback-driven%20neuro-symbolic%20reasoning) |
| 自适应 LLM–符号推理（求解器选择） | 按实例选求解器 | 2025 | [Scholar](https://scholar.google.com/scholar?q=adaptive%20LLM%20symbolic%20reasoning%20solver) |
| Z3 / CVC5 | 可判定理论；返回模型或反例 | 2008/22 | [DOI](https://doi.org/10.1007/978-3-540-78800-3_24) |
| Vampire / E | 一阶饱和式证明 | 2013/19 | [Scholar](https://scholar.google.com/scholar?q=Vampire%20first-order%20theorem%20proving) |
| Lean / Isabelle/HOL / Coq / Agda | 核可的交互式证明 | — | [Scholar](https://scholar.google.com/scholar?q=Lean%20theorem%20prover%20kernel) |
| SWI-Prolog | Horn 子句规则链 | 2012 | [DOI](https://doi.org/10.1017/S1471068411000494) |
| Clingo（ASP） | 组合、默认与规划 | 2019 | [DOI](https://doi.org/10.1017/S1471068418000054) |
| MiniSat / MiniZinc | 命题与有限域求解 | 2003/07 | [Scholar](https://scholar.google.com/scholar?q=MiniZinc%20constraint%20modeling) |
| SymPy / Mathematica | 精确符号计算 | — | [Scholar](https://scholar.google.com/scholar?q=SymPy%20symbolic%20computing%20Python) |
| Fast Downward（PDDL） | 目标导向经典规划 | 2006 | [Scholar](https://scholar.google.com/scholar?q=Fast%20Downward%20planning%20system) |
| 用于 PDE/解析微分方程的神经符号求解器 | 科学方程求解 | 2022/26 | [Scholar](https://scholar.google.com/scholar?q=neuro-symbolic%20partial%20differential%20equations) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l2-proof"></a>
### 形式化定理证明

把神经搜索与证明助手（Lean、Isabelle）耦合以达到奥数级形式数学——**唯一已拥有完整验证器的科学**（在其形式化边界之内）。

| 标题 | 角色 | T | 年份 | 链接 |
| :-- | :--: | :--: | :--: | :-- |
| GPT-f：用于定理证明的生成式语言建模 | R·G | T3 | 2020 | [arXiv](https://arxiv.org/abs/2009.03393) |
| Thor：整合 LM 与 ATP 的「锤子」 | R·G·E | T3 | 2022 | [Scholar](https://scholar.google.com/scholar?q=Thor%20wielding%20hammers%20language%20models%20theorem%20provers) |
| 超树证明搜索（HTPS） | R·G·E | T3 | 2022 | [Scholar](https://scholar.google.com/scholar?q=hypertree%20proof%20search) |
| LeanDojo：检索增强的定理证明 | R·G·E | T3 | 2023 | [arXiv](https://arxiv.org/abs/2306.15626) |
| Lean Copilot：作为 Lean 副驾的 LLM | R·G·E | T3 | 2024 | [arXiv](https://arxiv.org/abs/2404.12534) |
| Llemma：面向数学的开源 LM | R·G | T3 | 2024 | [arXiv](https://arxiv.org/abs/2310.10631) |
| DeepSeek-Prover V1.5 / V2（子目标分解 RL） | R·G·V | T4 | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=DeepSeek-Prover-V2%20subgoal%20decomposition%20Lean) |
| Goedel-Prover：开源自动定理证明 | R·G·V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=Goedel-Prover%20frontier%20automated%20theorem%20proving) |
| Kimina-Prover-Preview | R·G·V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=Kimina-Prover-Preview) |
| AlphaGeometry / AlphaGeometry2 | R·G·E·V | T3 | 2024/25 | [DOI](https://doi.org/10.1038/s41586-023-06747-5) |
| AlphaProof：Lean 环境中的 RL | R·G·V·E | T4 | 2026 | [DOI](https://doi.org/10.1038/s41586-025-09833-y) |
| PhysProver：物理领域的自动定理证明 | R·G·V | T4 | 2026 | [Scholar](https://scholar.google.com/scholar?q=PhysProver%20automatic%20theorem%20proving%20physics) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l2-diff"></a>
### 可微与溯因神经符号 ⭐

让逻辑本身**可微**、从而端到端学习符号结构——Kautz 尺度上**耦合最紧**（T5–T6），但迄今多在合成关系任务上验证。把它规模化到开放科学推理，正是大模型方法留空的深度。

| 标题 | 角色 | T | 年份 | 链接 |
| :-- | :--: | :--: | :--: | :-- |
| ∂ILP：从噪声数据中学习可解释规则 | R·E·G | T6 | 2018 | [Scholar](https://scholar.google.com/scholar?q=learning%20explanatory%20rules%20from%20noisy%20data%20differentiable%20ILP) |
| DeepProbLog：神经概率逻辑编程 | R·E | T6 | 2018 | [Scholar](https://scholar.google.com/scholar?q=DeepProbLog%20neural%20probabilistic%20logic%20programming) |
| NeurASP：神经网络 + 回答集程序 | R·E | T6 | 2020 | [Scholar](https://scholar.google.com/scholar?q=NeurASP%20embracing%20neural%20networks%20answer%20set%20programming) |
| Logic Tensor Networks | R·E | T6 | 2022 | [Scholar](https://scholar.google.com/scholar?q=Logic%20Tensor%20Networks) |
| Neural Logic Machines | R·E·G | T6 | 2019 | [Scholar](https://scholar.google.com/scholar?q=Neural%20Logic%20Machines) |
| 溯因学习（ABL）：桥接机器学习与逻辑推理 | R·E·V | T6 | 2019 | [Scholar](https://scholar.google.com/scholar?q=abductive%20learning%20bridging%20machine%20learning%20logical%20reasoning) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l3"></a>
## ✅ 第三层 — 验证、诊断与自适应控制 `经验信任`

**候选能否经受检验——并且能否定位它在*哪里*出错？** 本层裁决候选的逻辑、数学、科学与经验有效性，评估不确定度，做出接受/拒绝/修订决策——但止步于在世界中行动。一次裁决就是**新知识**：Kₜ₊₁ = Update(Kₜ, V(c))。符号角色：**V**（验证器）。标量过程奖励模型与 LLM 评判**不带符号肢体**——它们只能给候选排序却无法反驳，列为基线。

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l3-prm"></a>
### 步级诊断与过程奖励

超越终答准确率与模糊的 LLM 评判：过程监督定位推理链在*何处*断裂。但过程分数「定位多于解释」——而且模型**大多找不到自己的错误，一旦给定位置却能修复**。

| 标题 | 角色 | 年份 | 链接 |
| :-- | :--: | :--: | :-- |
| Let's Verify Step by Step（PRM800K） | V | 2024 | [Scholar](https://scholar.google.com/scholar?q=Let%27s%20verify%20step%20by%20step) |
| Math-Shepherd：无需逐步标注的过程奖励 | V | 2024 | [arXiv](https://arxiv.org/abs/2312.08935) |
| OmegaPRM：自动过程监督 | V | 2024 | [Scholar](https://scholar.google.com/scholar?q=improve%20mathematical%20reasoning%20automated%20process%20supervision) |
| ProcessBench：识别过程错误 | — | 2024 | [Scholar](https://scholar.google.com/scholar?q=ProcessBench%20identifying%20process%20errors%20mathematical%20reasoning) |
| 分层过程奖励模型 | V | 2025 | [Scholar](https://scholar.google.com/scholar?q=hierarchical%20process%20reward%20models) |
| 局部前瞻引导验证 | V | 2025 | [Scholar](https://scholar.google.com/scholar?q=local%20look-ahead%20guidance%20verifier) |
| OVM：结果监督的价值模型 | V | 2024 | [arXiv](https://arxiv.org/abs/2311.09724) |
| 训练验证器求解数学应用题（Cobbe 等） | V | 2021 | [arXiv](https://arxiv.org/abs/2110.14168) |
| LLM 找不到推理错误，但给定位置能纠正 | — | 2024 | [Scholar](https://scholar.google.com/scholar?q=LLMs%20cannot%20find%20reasoning%20errors%20correct%20given%20location) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l3-rlvr"></a>
### 验证器引导学习与可验证奖励（RLVR）

当验证器存在时，其信号可用来**训练策略**。此路的边界即验证器可得性：一旦不存在，可验证奖励的客观性退化为偏好奖励与校准。

| 标题 | 角色 | T | 年份 | 链接 |
| :-- | :--: | :--: | :--: | :-- |
| DeepSeekMath：群相对策略优化（GRPO） | V | T4 | 2024 | [arXiv](https://arxiv.org/abs/2402.03300) |
| DeepSeek-R1：用 RL 激励推理能力 | V | T4 | 2025 | [arXiv](https://arxiv.org/abs/2501.12948) |
| OpenAI o1 / o3-mini（可验证奖励长推理） | V | T4 | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=OpenAI%20o1%20learning%20to%20reason%20with%20LLMs) |
| Kimi K1.5：用 LLM 扩展 RL | V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=Kimi%20K1.5%20scaling%20reinforcement%20learning%20LLMs) |
| Qwen2.5-Math | V | T4 | 2024 | [Scholar](https://scholar.google.com/scholar?q=Qwen2.5-Math%20mathematical%20expert%20model) |
| ReFT：强化微调推理 | V | T4 | 2024 | [arXiv](https://arxiv.org/abs/2401.08967) |
| V-STaR：为自学推理器训练验证器 | V | T4 | 2024 | [arXiv](https://arxiv.org/abs/2402.06457) |
| 自奖励语言模型 | V | T4 | 2024 | [arXiv](https://arxiv.org/abs/2401.10020) |
| 生成式验证器（以下一词元方式验证） | V | T4 | 2024 | [Scholar](https://scholar.google.com/scholar?q=generative%20verifiers%20reward%20modeling%20next-token) |
| DeepSeekMath-V2：可自验证的数学推理 | V | T4 | 2025 | [Scholar](https://scholar.google.com/scholar?q=DeepSeekMath-V2%20self-verifiable%20mathematical%20reasoning) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l3-route"></a>
### 工具选择、路由与交叉验证

通用智能体框架回答*调用哪个工具*；科学推理需要更多——控制器必须**按实例路由并交叉验证**，因为没有单一后端覆盖整个任务谱。（Thor：PISA 求解率 39%→57%，+8.2% 单一组件都证不出。）

| 标题 | 角色 | 年份 | 链接 |
| :-- | :--: | :--: | :-- |
| MRKL：模块化神经符号架构 | E·V | 2022 | [arXiv](https://arxiv.org/abs/2205.00445) |
| ReAct：协同推理与行动 | A | 2023 | [Scholar](https://scholar.google.com/scholar?q=ReAct%20synergizing%20reasoning%20acting%20language%20models) |
| Toolformer：LM 自学使用工具 | A | 2023 | [Scholar](https://scholar.google.com/scholar?q=Toolformer%20language%20models%20teach%20themselves%20tools) |
| Reflexion：言语强化学习 | V | 2023 | [Scholar](https://scholar.google.com/scholar?q=Reflexion%20language%20agents%20verbal%20reinforcement%20learning) |
| AutoGen：多智能体对话框架 | A | 2024 | [arXiv](https://arxiv.org/abs/2308.08155) |
| MetaGPT：多智能体协作的元编程 | A | 2024 | [arXiv](https://arxiv.org/abs/2308.00352) |
| SWE-agent：智能体–计算机接口 | A | 2024 | [arXiv](https://arxiv.org/abs/2405.15793) |
| Thor（锤子路由）/ LeanDojo（检索+Lean） | E·V | 2022/23 | [Scholar](https://scholar.google.com/scholar?q=Thor%20hammer%20LeanDojo%20retrieval%20theorem%20proving) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="l3-repair"></a>
### 反馈驱动的修复

把求解器/证明器的执行轨迹编码为**结构化反馈**来驱动下一步——而非仅一个布尔检查。（Baldur：以失败证明 + 错误信息为条件，额外证明 +8.7% 定理；与 Thor 锤子合用，在 6,336 条定理基准上全自动证明 65.7%。）

| 标题 | 角色 | 年份 | 链接 |
| :-- | :--: | :--: | :-- |
| Baldur：用 LLM 整证生成与修复 | V·G | 2023 | [DOI](https://doi.org/10.1145/3611643.3616243) |
| 用 LLM 进行可靠的证明生成 | V·G | 2025 | [Scholar](https://scholar.google.com/scholar?q=reliable%20proof%20generation%20large%20language%20models) |
| Self-Refine：生成–批判–修订 | V·G | 2023 | [Scholar](https://scholar.google.com/scholar?q=Self-Refine%20iterative%20refinement%20self-feedback) |
| CRITIC：工具交互式自我纠正 | V | 2024 | [Scholar](https://scholar.google.com/scholar?q=CRITIC%20self-correcting%20tool-interactive%20critiquing) |
| LLM 能否推理程序不变量？ | V | 2023 | [Scholar](https://scholar.google.com/scholar?q=can%20large%20language%20models%20reason%20about%20program%20invariants) |
| PAL 输出是否验证了它的声称？ | V | 2024 | [Scholar](https://scholar.google.com/scholar?q=do%20PAL%20outputs%20verify%20what%20they%20claim) |
| Safe：用形式验证增强数学推理 | V | 2025 | [Scholar](https://scholar.google.com/scholar?q=Safe%20enhancing%20mathematical%20reasoning%20formal%20verification) |
| 自然语言推理的交错式形式验证 | V | 2026 | [Scholar](https://scholar.google.com/scholar?q=interleaved%20formal%20verification%20natural%20language%20reasoning) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="apps"></a>
## 🔬 跨学科应用 — 闭合回路

这**不是应用目录，而是对验证基础设施成熟度的扫描**。从验证器最完整的科学走向最匮乏的科学，回路依次：在形式边界内闭合 → 在概率验证器上闭合 → 在生成处停滞 → 且**无处完全闭合**。迁移梯度：生成抵达每门科学，而带符号肢体的各行（形式化、可执行推理、验证）**随验证器变稀缺而褪色**。

```
 机制 →               形式数学   算法/代码   化学      材料      生命科学
 生成                   ●          ●          ●         ●         ●
 接地(RAG,KG)           ◐          ◐          ●         ●         ●
 形式化                 ●          ●          ◐         ○         ○
 可执行推理             ●          ●          ◐         ○         ○
 验证                   ●          ●          ○         ○         ○
 控制(路由/修复)        ●          ◐          ◐         ○         ○
                ● 已建立   ◐ 部分/萌芽   ○ 因验证器匮乏受阻
```

<a id="app-math"></a>
### 形式数学与定理证明 — *形式边界内的闭合*

每一层都被实现、回路闭合，因为验证器**确定、廉价且具诊断性**：证明要么通过可信内核的类型检查，要么不通过。写回精确且累积（Mathlib）。边界在于：内核只认证已被**形式化**的部分——自动形式化仍缓慢、有损、未解决。

| 系统 | 贡献 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| AlphaGeometry | 神经构造 + 演绎引擎；25/30 IMO 几何 | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06747-5) |
| AlphaGeometry2 | 更广的奥数几何 | 2025 | [Scholar](https://scholar.google.com/scholar?q=AlphaGeometry2%20olympiad%20geometry) |
| AlphaProof | 在通用 Lean 环境内做 RL | 2026 | [DOI](https://doi.org/10.1038/s41586-025-09833-y) |
| DeepSeek-Prover / Goedel-Prover / Kimina-Prover / Lean Copilot | 工业化的端到端 Lean 生成 | 2024–25 | [Scholar](https://scholar.google.com/scholar?q=DeepSeek-Prover%20Goedel-Prover%20Kimina-Prover%20Lean) |

<a id="app-algo"></a>
### 算法与代码发现 — *确定性评估器，开放式搜索*

验证器从证明内核放松为**可执行评估器**：跑程序，其得分即信号。廉价且明确，回路得以闭合——但它度量性能而非认证真理，残余风险转移到**规格鸿沟**。

| 系统 | 贡献 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| FunSearch | LLM 提议器 + 确定性评估器；新组合构造 | 2024 | [DOI](https://doi.org/10.1038/s41586-023-06924-6) |
| AlphaTensor / AlphaDev | RL 符号搜索发现更快算法 | 2022/23 | [DOI](https://doi.org/10.1038/s41586-022-05172-4) |
| AlphaEvolve | 提议器–评估器范式推广为编码智能体 | 2025 | [arXiv](https://arxiv.org/abs/2506.13131) |
| 符号回归（Eureqa、SINDy、PySR） | 拟合残差作验证器；可解释定律 | 2009– | [DOI](https://doi.org/10.1126/science.1165893) |
| SciCode | 科学代码生成基准 | 2024 | [Scholar](https://scholar.google.com/scholar?q=SciCode%20scientific%20code%20generation%20benchmark) |

<a id="app-chem"></a>
### 化学与自主合成 — *回路抵达实验台*

第一门验证器**离开计算机、变成物理实验**的科学。接地很强；形式化/执行只部分迁移——一条路线在纸面上合理，其可行性只有实验台才能定夺。实施不再免费；写回知识库的是**概率性测量值**，而非已认证的事实。

| 系统 | 贡献 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| Coscientist | 从理解到执行闭合回路 | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06792-0) |
| ChemCrow | 名称解析、逆合成、机器人执行作为动作空间 | 2024 | [DOI](https://doi.org/10.1038/s42256-024-00832-8) |
| 用 DNN 与符号 AI 规划化学合成 | 逆合成（纸面合理） | 2018 | [DOI](https://doi.org/10.1038/nature25978) |
| Protect：可操控逆合成（神经符号） | 约束引导的路线 | 2026 | [Scholar](https://scholar.google.com/scholar?q=Protect%20steerable%20retrosynthesis%20neuro-symbolic) |
| FragmentRetro：二次复杂度逆合成方法 | 基于片段的搜索 | 2025 | [Scholar](https://scholar.google.com/scholar?q=FragmentRetro%20quadratic%20retrosynthetic%20method) |
| 机器人流动合成 / 移动机器人化学家 | 机器人基底 | 2019/20 | [DOI](https://doi.org/10.1126/science.aax1566) |
| 贝叶斯反应优化 | 定量验证器代理 | 2021 | [DOI](https://doi.org/10.1038/s41586-021-03213-y) |

<a id="app-mat"></a>
### 材料发现 — *当实验的验证器本身不确定*

**验证器匮乏成为前景问题**之处。预测很强（GNoME、MatterGen），但确认「合成出了什么」*本身是一次推断*。A-Lab 在 17 天内合成 41/58 个目标——但一项独立复核质疑了若干物相归属。**一个机械闭合、却没有可信验证器的回路，不是信任回路。**

| 系统 | 贡献 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| GNoME | 百万候选规模的稳定性预测 | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06735-9) |
| MatterGen | 无机材料的生成模型 | 2025 | [DOI](https://doi.org/10.1038/s41586-025-08628-5) |
| A-Lab | 自主合成；「实验验证器」之争 | 2023 | [DOI](https://doi.org/10.1038/s41586-023-06734-w) |
| 用失败实验进行机器学习辅助发现 | 负结果即数据 | 2016 | [DOI](https://doi.org/10.1038/nature17439) |
| MARS / MedRule-KG / NSGG | 为生成式提议提供神经符号保证 | 2024–26 | [Scholar](https://scholar.google.com/scholar?q=neural%20proposals%20symbolic%20guarantees) |

<a id="app-bio"></a>
### 生命科学 — *有预测，无闭合*

回路**最常在生成处停滞**之处，尽管这里拥有全领域最负盛名的预测器。AlphaFold/ESM3 是没有符号系统检查的预测器；验证是缓慢、嘈杂、昂贵的湿实验。几乎没有东西被写回为可信知识——这是**热力图右下角的空白**，也是研究议程的目的地。

| 系统 | 贡献 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| AlphaFold / AlphaFold-3 | 近实验级结构预测 | 2021/24 | [DOI](https://doi.org/10.1038/s41586-021-03819-2) |
| ESM3 | 在学习的序列空间中模拟蛋白质进化 | 2025 | [DOI](https://doi.org/10.1126/science.ads0018) |
| Boltz-1 | 开源结构预测 | 2025 | [arXiv](https://arxiv.org/abs/2411.13408) |
| BioDiscoveryAgent / Robin | 智能体式实验提议与解释 | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=BioDiscoveryAgent%20agent%20experiment%20design) |
| BioProAgent | 约束下的神经符号实验方案生成 | 2026 | [Scholar](https://scholar.google.com/scholar?q=BioProAgent%20protocol%20generation%20constraints) |
| 抗生素发现（Stokes；可解释结构类） | 经实验验证的深度学习候选 | 2020/24 | [DOI](https://doi.org/10.1016/j.cell.2020.01.021) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

> **自主不等于可信。** 系统在自主谱上的位置由*其科学能容许的验证器*决定，而非工程雄心：自主实验室能以远快于「信任其结果」的速度去执行决策。在实验室中行动的智能体的治理、安全与可复现，正是回路抵达世界后「可信实施」所采取的*形式*。

<a id="bench"></a>
## 📊 基准与信任对齐评测

以信任为中心的回路要求评测不仅打分*答案对不对*，还要看*它是如何得到的*。我们按基准所探测的**信任维度**组织。覆盖梯度鲜明：推理信任被密集基准化；经验信任通过过程/验证器检查打分，但**很少经独立复现**；认识论信任（溯源）几乎未被度量；实践闭合端只有粗粒度智能体套件触及。

| 信任维度 | 代表性基准 | 覆盖度 |
| :-- | :-- | :--: |
| **推理 Inferential** | MATH · GSM8K · ProofWriter · BIG-Bench Hard · LogicBench · FrontierMath · Humanity's Last Exam · RLMEval · VeriSoftBench | ● 密集 |
| **认识论 Epistemic** | ScienceQA · MMMU · MMMU-Pro · MathVista · MathVerse · LogicVista · OlympiadBench · SciBench · CiteAudit *(溯源, 新生)* | ◐ 部分 |
| **经验 Empirical** | ProcessBench · VerifyBench · SciCode · Lessons-from-PRMs · ReliableEval · ReplicatorBench *(复现)* | ◐ 部分 |
| **实践闭合** *(非信任维度)* | AgentBench · ScienceAgentBench · BOLAA · SciAgentGym · FIRE-Bench · BioProBench | 仅粗粒度 |

| 基准 | 探测 | 年份 | 链接 |
| :-- | :-- | :--: | :-- |
| MATH / GSM8K | 数学问题求解 | 2021 | [Scholar](https://scholar.google.com/scholar?q=measuring%20mathematical%20problem%20solving%20MATH%20dataset) |
| ProofWriter | 自然语言上的蕴含、证明、溯因 | 2021 | [Scholar](https://scholar.google.com/scholar?q=ProofWriter%20generating%20implications%20proofs) |
| LogicBench | 系统化逻辑推理评测 | 2024 | [Scholar](https://scholar.google.com/scholar?q=LogicBench%20systematic%20evaluation%20logical%20reasoning) |
| FrontierMath / Humanity's Last Exam | 研究级推理 | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=FrontierMath%20benchmark) |
| MMMU / MMMU-Pro | 多学科多模态理解 | 2024 | [Scholar](https://scholar.google.com/scholar?q=MMMU%20massive%20multi-discipline%20multimodal%20understanding) |
| MathVista / MathVerse | 视觉数学推理 | 2024 | [Scholar](https://scholar.google.com/scholar?q=MathVista%20mathematical%20reasoning%20visual%20contexts) |
| ScienceQA / SciBench / OlympiadBench | 科学与奥赛推理 | 2022–24 | [arXiv](https://arxiv.org/abs/2307.10635) |
| ProcessBench / VerifyBench | 过程错误；评测验证器本身 | 2024/25 | [Scholar](https://scholar.google.com/scholar?q=VerifyBench%20evaluating%20verifiers) |
| SciCode | 科学代码生成 | 2024 | [Scholar](https://scholar.google.com/scholar?q=SciCode%20benchmark) |
| AgentBench / ScienceAgentBench | 智能体式与数据驱动发现 | 2024/25 | [arXiv](https://arxiv.org/abs/2308.03688) |
| BioProBench | 生物实验方案理解 | 2025 | [Scholar](https://scholar.google.com/scholar?q=BioProBench%20biological%20protocol%20understanding) |

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="agenda"></a>
## 🧭 开放挑战与研究议程

议程即验证成熟度地图的**两个坐标**——把*可验证性*提升至严格，把*代价*压低——直到严格验证便宜到能在回路**之内**运行。经验科学需要**构建**验证；形式科学需要**补全**其验证。构建材料是神经符号的：符号组件提供可执行语义与约束，神经组件提供学习的验证器与代理。

1. **神经到符号的语义鸿沟** — 区分「因为命题为假而 UNSAT」与「因为翻译丢了前提而 UNSAT」；为推理链提供忠实性证书，并让翻译诊断与求解器诊断*并行*运行。*这道鸿沟就是形式化边界本身。*
2. **会过时的知识、会冲突的证据** — 协调检索、编辑与后训练，使知识前沿随文献推进而不让编辑涟漪为矛盾；持久化多模态证据，使图像、谱、表的事实不在链条中丢失。
3. **验证器匮乏与统一多求解器推理** — *总开关。* 在验证器部分、昂贵或概率时构建可验证奖励（基于模型/生成式验证器、学习的科学验证器）；在单一接口后做多后端路由与交叉验证。
4. **信任–效用–代价权衡** — 在不确定度与风险条件下，按实例分配推理深度、后端选择与反馈轮次的代价感知策略。
5. **可证伪性、可复现与自主智能体治理** — 能重跑声称结果、给校准/弃权打分的基准；在实验室中行动的智能体的安全与问责。

> **按领域的失败模式** — 翻译失真在数学/代码中占主导（验证器匮乏*低*）；**证据衰减与验证器匮乏**在化学/材料/生物中占主导，二者都非更好的求解器所能解决。这正是为何同一回路在一列产出机器核可的确定性，在另一列只能给出谨慎的、待实验的论断。

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="vmap"></a>
## 🗺️ 验证成熟度地图

综述的核心贡献：依各门科学能容许的验证器，把它们放上一张双轴地图。**终点是「低成本、完全可验证」的角落**——今天只有可形式化的论断到达。严格是*贯穿全程*的目标；概率验证是有待变严格的*前沿*，**不是终点**。

| 验证机制 | 可验证性 | 代价 | 代表性科学 | 约束性瓶颈 |
| :-- | :--: | :--: | :-- | :-- |
| 确定性可执行评估器 | ● 完全 | 低 | 算法与代码发现 | 规格鸿沟 |
| 内核核可的形式证明 | ● 完全 † | 高 | 形式数学（Lean、Coq） | 形式化边界 |
| 近似学习验证器（可弃权） | ◐ 半 | 低 | 各学科新兴（PRM、Sci-Verifier） | 校准；无保证 |
| 一致性与接地检查 | ◐ 半 | 低 | 知识接地 QA（RAG、KG） | 检查接地而非真理 |
| 物理实验 / 高保真模拟器 | ◐ 半 | 高 | 化学、材料、生物 | 代价、噪声；非形式 |
| 无；仅生成 | ○ 无 | — | 开放构想；大量生命科学 | 幻觉、不可复现 |

`† 形式证明完全认证，但仅在形式化边界之内。`

地图上的议程即两支箭头：**把弱检查提升至严格，并把严格验证的代价压低**——一个*为科学而生的 Lean*（理想形态）。

<p align="right">(<a href="#readme-top">⬆ 返回顶部</a>)</p>

<a id="contributing"></a>
## 🤝 贡献

非常欢迎贡献——补充遗漏的论文、代码链接与基准！请阅读 [CONTRIBUTING.md](./CONTRIBUTING.md) 并按表格条目格式提交 PR。新增方法时，请标注其**主层**（知识/推理/验证/应用）、**符号角色**（K·R·G·E·V·A），并在适用时标注 **Kautz 集成深度**（T1–T6）。

<a id="citation"></a>
## 📌 引用

如果本仓库对您的研究有帮助，欢迎引用配套综述（即将发布）：

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

## 📜 许可证

本仓库内容（整理与描述）以 [CC BY 4.0](./LICENSE) 发布。所列论文的版权归各自作者与出版方所有。

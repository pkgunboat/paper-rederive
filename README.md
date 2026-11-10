# paper-rederive

**Learn academic papers by re-deriving their motivation, core method, and experimental insights from first principles.**  
**通过第一性原理“重推导”论文动机、核心方法与实验洞察的苏格拉底式精读 Agent Skill（v0.1.0）。**

Inspired by [EricJujianZou/rederive](https://github.com/EricJujianZou/rederive) (which teaches codebases through Socratic system design), `paper-rederive` adapts first-principles derivation to academic research papers. Instead of giving you a 5-minute AI summary that fades in three days, it guides you to uncover the baseline's flaw, invent the core mechanism under real constraints, and read experimental tables like a detective.

受 [EricJujianZou/rederive](https://github.com/EricJujianZou/rederive) 启发，`paper-rederive` 将“苏格拉底式第一性原理推导”迁移并改造到了学术论文精读场景。它拒绝直接喂给你快餐式摘要，而是带你亲手揪出前人 Baseline 的痛点、在真实约束下推演出核心方法、并从消融与反常实验数据中提炼科研洞察，帮你真正训练 **Research Taste（科研品味与直觉）**。

---

## English Guide

### When to Use (Usage Scenarios)

**Best Fit Scenarios:**

- **Deep-reading core papers**: Methodological, algorithmic, theoretical, or computer systems papers with a clear causal spine (*Baseline Bottleneck -> Core Mechanism -> Empirical Validation*).
- **Onboarding into an unfamiliar research area**: Includes **Just-in-Time Domain Primers** — if you are new to the field and have no initial intuition, tell the agent and it will briefly explain pre-existing domain building blocks without spoiling the paper's novel contribution.
- **Reading group / presentation prep**: Internalize *why* every core equation or module exists so you can explain the design decisions from scratch.
- **Reviewer-style stress testing**: Uncover hidden assumptions, boundary failure regimes, and concrete follow-up research ideas.

**When NOT to Use:**

- **Fast literature screening**: When skimming 20 papers to filter relevance, use a standard summarizer instead.
- **Broad survey / review papers**: Surveys catalog taxonomy rather than deriving a single mechanism.
- **Pure dataset / benchmark releases or bag-of-tricks reports**: Papers without a unified methodological leap will automatically trigger a suitability warning, offering to jump straight to empirical analysis instead.

### How It Works (Three-Act Workflow)

1. **Act 1 — Spot the Motivation (Deconstruct the Baseline)**: Instead of making you guess the authors' topic in the dark, the agent lays out how the prior baseline works alongside the target scale/hardware/task conditions, then asks you to trace where the baseline breaks first.
2. **Act 2 — Re-derive the Solution (Incremental Constraints)**: You propose a naive fix; the agent challenges it one constraint at a time (grounded in the paper's actual ablations and comparisons). Arbitrary hyperparameters and minor engineering glue are summarized automatically as footnotes rather than turned into tedious guessing games. Un-derivable empirical observations are given upfront as clues.
3. **Act 3 — Extract Experimental Insights (Predict & Explain)**: Before revealing ablation tables, the agent asks you to bet on which component matters most or how scaling behaves, contrasts your prediction against the real numbers, and surfaces counter-intuitive trends or failure boundaries to spark follow-up paper ideas.

**Adaptive Pacing & Dialogue Rules:**

- One focused question per turn, withholding the paper's coined buzzwords until you derive the underlying mechanism.
- **Just-in-Time Background**: Say *"I'm not familiar with this field"* at any point to get a concise, plain-language primer on prior domain concepts before continuing.
- **Adaptive Scaffolding**: Stuck on tradeoffs? It narrows the space to 2–3 candidate routes, or sketches a toy numerical example after two misses. Say *"skip"* anytime to reveal a step and move on.

### Install & Usage

Install via the skills CLI:

```bash
npx skills add pkgunboat/paper-rederive
```

Or copy `skills/paper-rederive` directly into your agent's skills directory (e.g., `~/.claude/skills/`, `~/.agents/skills/`, or upload `SKILL.md` in your agent's Skills Manager UI).

**Example Prompts:**

```text
Use paper-rederive to walk me through https://arxiv.org/abs/2106.09685
```

```text
Rederive ./papers/flashattention.pdf with me step by step.
```

---

## 中文说明

### 适用场景与边界（Usage Scenarios）

**最适合使用的场景：**

- **精读领域代表作与核心方法论论文**：适合机器学习新架构、优化算法、理论建模、计算机系统等具备清晰因果链（*前人瓶颈 -> 核心机制跃迁 -> 实验验证*）的论文。
- **跨领域精读陌生方向论文**：内置**提问中按需补课（Just-in-Time Background）**机制——当你对某个新方向不熟、完全没头绪时，直接告诉它“我对这领域不太了解”，它会先用 3～5 句大白话补齐该领域的前置常识与常用工具箱（严守边界不剧透本文创新点），垫好台阶后再带你推导。
- **组会分享（Reading Group）与答辩准备**：不再死记硬背公式和模块名，而是真正推通每一步设计背后的必然性。
- **培养审稿人视角与挖掘新 Idea**：通过拆解实验失效边界与隐含假设，顺势推演出下一篇可以接着做的研究切入点。

**不建议使用的场景：**

- **大批量文献速览（Screening）**：快速扫几十篇摘要筛文献时，直接用常规总结更高效。
- **综述类论文（Survey / Review）**：综述重在分类梳理，不存在单一可推导的技术方案。
- **纯数据集/Benchmark 发布或纯工程 Trick 拼盘论文**：缺乏核心机制主线的论文在启动时会被自动识别，智能体会主动提示并建议直接切入实验结论分析。

### 三幕式重推导机制

1. **第一幕：揪出动机（给 Baseline 找茬）**：不让你盲猜选题，而是先把前人标准做法和目标规模/硬件/任务前提摆上桌面，引导你顺着推演出前人方案必然撞上的瓶颈。
2. **第二幕：推导方案（渐进式施加约束）**：从你的朴素解法出发，结合论文真实的对比与消融结论逐个抛出约束打磨方案；核心机制（2～4 步）由你推导，琐碎超参（如 $\lambda=0.05$）和工程拼接在过关后作为注脚顺口补齐，反直觉的先验实验现象则直接作为已知线索提供。
3. **第三幕：挖掘实验洞察（先预测、再探案）**：亮出消融表格前先让你押注哪个模块影响最大、不同规模下趋势如何，再用真实数据对照你的直觉偏差；随后抛出图表中的反常拐点或失效场景，引导你分析方法局限与后续改进方向。

**交互体验保障：**

- **单问号纪律与术语防泄底**：每轮只聚焦一个问题，在你推出机制前绝不提前抛出论文自创缩写词。
- **两级防卡死脚手架**：卡在领域背景时按需科普前人常识；卡在推理权衡时给出 2～3 条带代价对比的候选方向，连卡两次则提供极简数字草图；随时可说“跳过这步”直接看解析。

### 安装与触发示例

通过命令行安装：

```bash
npx skills add pkgunboat/paper-rederive
```

或手动将 `skills/paper-rederive` 目录复制到对应 Agent 的技能目录（如 `~/.claude/skills/`、`~/.agents/skills/`），或在技能管理界面直接导入 `skills/paper-rederive/SKILL.md`。

**常用触发方式：**

- `用 paper-rederive 带着我推演 https://arxiv.org/abs/2106.09685`
- `引导我重推导这篇论文`（配合上传本地 PDF 附件或提供本地路径）
- `苏格拉底式读论文 FlashAttention`

---

## License

MIT License

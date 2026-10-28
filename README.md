# research-novelty-gate｜创新点查新与立项门槛

> 把「看起来有意思的想法」变成**有最近邻证据、有反证检查、有预算、有退出条件的研究决策**。
> 它允许交付「没有候选达到立项门槛」，不为了完成任务硬凑创新。

一个给 AI agent 用的技能包：`SKILL.md` 入口 + 分阶段流程 + 证据/决策/交接三类模板 + 12 个行为验收用例。适用于任何支持 `SKILL.md` 约定的 agent 运行时（DeepSeek Harness、Claude Code 等）。

---

## 它解决什么问题

研究里最常见的两种失败：

1. **假创新**——自己觉得「首次在 X 场景用了 Y」，一查去年就有两篇做过；或者把换符号、加调节系数、堆算法名字当成贡献。
2. **不敢下结论**——查了一圈，既不能说「有人做过」，也不敢说「没人做过」，于是一直悬着，最后靠感觉立项。

这个技能包对第一种有明确的检查清单，对第二种的要求是：**写下你查到哪、没查到哪、哪一项原文没拿到**，然后基于这个状态做决定，而不是基于希望。

它**不**做这些事：不替你选期刊，不替你定医学终点或触地标准，不保证发表，不自动授权跑实验/写代码/装依赖。

---

## 三种使用档位

| 档位 | 你给什么 | 它交付什么 |
|---|---|---|
| **快速核查** | 一个想法，或几篇论文 | 短判决 + 最近邻 + 下一项最值得做的检查 |
| **立项查新** | 明确的约束（平台、数据、周期、投稿取向） | 0–1 个优先候选 + 0–2 个备选；**可以全是「不立项」** |
| **跨域与交接** | 已选定的问题 | 别的领域怎么解决同一障碍 + 给执行模型的可独立阅读的实施任务书 |

轻任务（翻译一段、解释一个公式、改一条引用）不该启动完整流程。

---

## 五条不可协商的纪律

1. **先例先于推荐。** 先找最近邻和后续工作，再讨论候选贡献。不得先许诺创新，再逐轮收回。
2. **原文先于空白。** 搜索结果、摘要、综述、作者 future work 只是线索；关键假设、定理、比较范围尽量回原文核验。
3. **反证先于立项。** 主动查同义术语、跨领域等价方法、后续版本、强基线，寻找「这个想法已经被解决了」的证据。
4. **门槛不靠加总。** 新颖性、理论闭合、资源、验证设计各自单独过关，不能用「好做／好看」抵消「没有技术差额」。
5. **诚实地停止。** 缺全文、没找到差额、证明不闭合或成本超限时，交付负面结论和下一项有限核查。

证据分四级：**P**（已取得原文并核查相关节）／**A**（仅摘要）／**M**（仅题录）／**U**（无法核实）。等级针对所用主张，不是给整篇论文贴永久标签。

候选状态分五档，每档含义固定：

- **已排除**——有直接先例或等价性反证
- **待查证**——来源、后续工作或关键原文尚缺
- **值得短期预研**——对象/止损明确，但独立增量未建立
- **有条件立项**——最近邻、具体差额、推导路径、预算与验证同时过门
- **已实施验证**——另有代码/实验证据

并且始终区分「**尚未证明有创新**」与「**已证明不存在任何创新**」。

---

## 最好用的部分：碰撞卡

阶段 D 的八问，是这个包最实用的部分。每个候选逐项过一遍：

| 检查 | 要回答什么 |
|---|---|
| 直接先例 | 已有文章是否原封不动覆盖？ |
| 同义机制 | 是不是换了领域名/算法名？ |
| 代数/统计等价 | 新变量能否消去？同物理约束、代价和信息是否完全一致？ |
| 已知工具适配 | 是否仅用普通求根、区间、标准稳健估计等成熟工具？ |
| 约束造差 | 是否人为冻结/削弱对手、删掉已知量、换成功指标才有优势？ |
| 保证偷换 | 充分不满足≠不可行；样本成功≠全域保证；一个模式≠切换系统 |
| 强对手 | 同信息直接优化/标准投影/成熟基线能否同样完成？ |
| 后续工作 | 种子文献的 future work 是否已被后续或其他领域解决？ |

反证成立时归类为：已解决／方法适配／仍有特定差额／信息不足——**不要把所有假设差异都升级成研究空白**。

---

## 安装

```bash
git clone https://github.com/Cupit-zy/research-novelty-gate.git
```

把整个目录放进 agent 的技能目录，保持 `SKILL.md` 在根：

```bash
# DeepSeek Harness（Windows）
xcopy /E /I research-novelty-gate "%USERPROFILE%\.dsh\skills\research-novelty-gate"

# DeepSeek Harness（macOS / Linux）
cp -r research-novelty-gate ~/.dsh/skills/

# Claude Code 风格
cp -r research-novelty-gate ~/.claude/skills/
```

不需要额外依赖、API key 或特定检索服务。

---

## 用法

直接用中文或英文说清楚任务和权限即可，技能负责把流程收住：

```text
使用 research-novelty-gate，基于这些论文寻找值得研究的问题。
先查最近邻和反证，不要先替我宣布创新。
周期 3 个月，本轮只做文献和纸面分析，不运行实验。
```

```text
使用 research-novelty-gate，审查这个方法是不是重参数化或已有方法的适配，
给出原文依据和继续/停止条件。
```

```text
使用 research-novelty-gate，从其它领域寻找解决同一技术障碍的方法，
区分成熟基线和候选改进，写成可交给其它模型实施的 Markdown 方案。
```

### 先读哪个文件

1. 首次执行 → `references/workflow.md`（阶段 A–I 的完整流程）
2. 新建查新项目 → 复制 `templates/evidence.md` 和 `templates/decision.md`
3. 要实施方案 / 交接给别的模型 → `templates/handoff.md`
4. 想自检行为 → `examples/acceptance-cases.md`（12 个用例，不是研究证据）

模板是写入**你的项目**的内容骨架。不要把某个项目的检索记录写回技能目录。

---

## 仓库结构

```text
research-novelty-gate/
├── SKILL.md                      # 技能入口：触发语、模式、纪律
├── README.md
├── references/
│   └── workflow.md               # 阶段 A–I：护照、最近邻、原文核查、反证、门槛、预研、跨域、交接、交付
├── templates/
│   ├── evidence.md               # 检索记录、书目、主张、最近邻矩阵、纠正日志
│   ├── decision.md               # 候选卡、独立门槛表、最低成本预研、决策日志
│   └── handoff.md                # 模型/权限/接口/DAG/实验/验收的交接模板
├── examples/
│   └── acceptance-cases.md       # 12 个行为验收用例
├── LICENSE
└── validation.json               # 构建期静态检查记录
```

---

## 已知局限

写在这里，是因为这个技能本身要求别人诚实。

- **它是清单，不是引擎。** 它逼你如实说「没找到」，但它找不到那篇你没检索到的论文。它防自欺，不防无知。
- **成本不低。** 三条搜索轴 × 8–15 条记录 + 3–5 篇原文精读，一个候选是大半天。多数场景应该走「快速核查」档。
- **学科基因偏控制/优化/ML。** 碰撞卡里的等价性检验、保证偷换、抗饱和式例子来自控制与数值方法；统计场景（重参数化、特征泄漏、训练测试重用）已覆盖；质性社科、临床、人文学科需要自己补对应检查项。
- **没有不对称成本模型。** 整体偏「宁可错杀」，这在项目早期是对的（早死便宜），但有些真突破第一次看就像重参数化。执行时要有判断，别把工具当判决。
- **行为未被实测。** `validation.json` 只记录静态结构与加载检查；12 个验收用例是可复用的检查题，**没有跑过模型行为评测**。它的说服力目前来自文字，而不是测量。另外，该文件里的哈希对应 2026-10-23 的构建快照，本 README 为公开发布重写过，其中的 README 哈希已不再匹配。

---

## License

见 [LICENSE](LICENSE)。

---

## English

A skill package for evidence-first research novelty assessment. It forces a nearest-prior-art search and a deliberate falsification pass **before** any claim of novelty, and it accepts "no candidate clears the bar" as a valid outcome.

- **Modes:** quick check / scoped novelty audit / cross-domain transfer + handoff.
- **Non-negotiables:** precedent before recommendation, source text before "gap", counter-evidence before commitment, independent gates instead of a weighted score, and honest stopping.
- **Evidence levels:** P (full text read and verified) / A (abstract only) / M (metadata only) / U (unverifiable).
- **Status tiers:** excluded / pending verification / short pre-study / conditional go / implemented.
- **The most useful artifact:** the 8-row collision card in `references/workflow.md` — direct precedent, synonym mechanism, algebraic/statistical equivalence, known-tool adaptation, constraint-manufactured advantage, guarantee swap, strong baseline, follow-up work.

Install by dropping the folder into your agent's skills directory. No dependencies, no keys, no specific retrieval service.

Known limitations are listed above: it is a checklist rather than a discovery engine, the anti-patterns lean toward control/optimization/ML, and the 12 acceptance cases have not been run as a behavioral benchmark.

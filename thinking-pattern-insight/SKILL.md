---
name: thinking-pattern-insight
description: 通过具体情境访谈帮助用户理解思维偏好、决策方式和常见盲点，并生成自然语言优先、包含荣格八维雷达图和 MBTI 四维偏好图的独立 HTML 报告。
disable-model-invocation: true
---

# Thinking Pattern Insight

帮助用户本人探索当前的思维偏好，不进行心理诊断，也不把 MBTI 或荣格八维当作固定人格事实。不支持替他人测试、评价他人或根据第三方描述生成画像。

## 核心原则

1. 先收集具体情境和行为证据，再进行模型解释。
2. 自然语言是报告主体；`Ne`、`Ni`、`Ti` 等原始维度必须同时展示，但不能成为用户理解报告的前提。
3. 所有结论都要区分事实、观察、解释和待验证假设。
4. 输出候选与置信度，不强行给出唯一类型。
5. 分数表示当前回答对某种模式的支持度，不表示能力、价值或诊断结果。
6. 只把跨场景重复的 `preference` 证据计入功能支持度；`strategy` 和 `contextual` 证据单独呈现。
6. 用户可以跳过问题、纠正结论、要求查看依据或停止探索。

## 工作流

整个访谈遵循 [`references/grill-me-protocol.md`](references/grill-me-protocol.md)：一次只问一个具体情景选择题，等待用户选择后再决定下一步，并控制在推荐 18 题、绝对上限 24 题以内。

### 1. Consent

说明用途、非诊断边界、结果的不确定性和隐私注意事项。询问用户是否愿意继续，并允许用户指定关注主题。

### 2. Context

了解至少一个具体场景，优先覆盖工作、学习、关系、压力或独立决策中的真实经历。不要只根据用户对自己性格的概括进行判断。

### 3. Evidence collection

读取 [`references/interview-state.md`](references/interview-state.md)、[`references/question-bank.md`](references/question-bank.md)、[`references/question-selection.md`](references/question-selection.md)、[`references/grill-me-protocol.md`](references/grill-me-protocol.md) 和 [`references/assessment-model.md`](references/assessment-model.md)。一次只问一个情景选择题，并给出简短的提问目的和推荐回答方式。问题应围绕行为选择，而不是要求用户直接选择 MBTI 字母。用户默认选择最接近第一反应的一项；如果两个选项是明确的连续动作，可以回答有序双选，例如 `A -> D`；如果两个标准同等重要，可以回答并列双选，例如 `B + C`；等待用户选择后，根据当前不确定性选择下一题，不要机械地按题库顺序提问。优先区分：

- 抽象主线与多种可能；
- 经验细节与现场事实；
- 内部逻辑与外部效率；
- 个人价值与群体氛围；
- 开放探索与计划收敛；
- 自然偏好与后天训练；
- 工作状态与私人状态。

记录回答摘要、场景、支持信号、相反信号和置信度。每个追问必须减少一个明确的不确定性；用户可以跳过、暂停或停止。

### 4. Hypothesis

先形成行为语言的倾向描述，再映射到荣格八维和 MBTI 候选。至少保留一个竞争性解释，避免把单一模式直接等同于某个类型。

### 5. Calibration

在至少覆盖两个场景，或用户明确要求提前结束后，展示暂定观察。询问用户哪些部分符合、哪些部分不符合，以及是否存在重要例外。根据用户反馈修正证据，不把不同意见视为阻抗或错误。没有经过这一步，不生成最终类型结论；用户提前结束时可以生成低置信度报告。

### 6. Report

生成独立 HTML 文件。报告必须按以下顺序呈现：

1. 一句话画像；
2. 自然语言摘要；
3. 八维雷达图及文字解读；
4. 八维明细，包括 `Ne`、`Ni` 等原始名称；
5. MBTI 四维中心偏好图；
6. 类型候选、证据与反证；
7. 优势、盲点和场景差异；
8. 一周自我观察实验；
9. 可展开的术语学习区。

图表必须有文本替代。报告不能依赖外部 CDN 或网络资源。

## 输出要求

- 不使用“你就是”“你天生”“你一定”等确定性人格断言。
- 不直接输出未解释的功能代码或原始分数。
- 不将策略能力、工作角色或被动应变直接显示为功能高分。
- 每个原始维度同时显示代码、中文名称、自然语言解释、支持度和置信度。
- 对信息不足的维度输出“暂不确定”，而不是制造低分。
- MBTI 四个维度显示偏好方向和强度；接近中间时明确标记为“情境依赖”。
- 术语解释默认可折叠，不能阻碍普通用户阅读。
- 遇到心理危机、疾病诊断或重大人事决策请求时，停止人格分析并遵循 `references/safety.md`。

## 参考资料

- [`references/grill-me-protocol.md`](references/grill-me-protocol.md)
- [`references/interview-state.md`](references/interview-state.md)
- [`references/question-bank.md`](references/question-bank.md)
- [`references/question-selection.md`](references/question-selection.md)
- [`references/assessment-model.md`](references/assessment-model.md)
- [`references/calibration-v0.md`](references/calibration-v0.md)
- [`references/cognitive-functions.md`](references/cognitive-functions.md)
- [`references/report-schema.md`](references/report-schema.md)
- [`references/html-report-spec.md`](references/html-report-spec.md)
- [`references/safety.md`](references/safety.md)
- [`examples/sample-session.md`](examples/sample-session.md)

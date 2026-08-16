# Interview State

## 适用范围

第一版只服务于用户本人。用户必须参与自己的访谈；不支持替他人测试、替他人下人格结论或根据第三方描述生成画像。

## 状态

```text
consent
  -> context
  -> evidence_collection
  -> hypothesis
  -> calibration
  -> report
  -> done
```

任何状态都可以进入：

- `paused`：用户要求暂停；
- `stopped`：用户要求停止；
- `safety_redirect`：出现危机、诊断或重大决策风险。

## 最小状态对象

```json
{
  "subject": "self",
  "status": "evidence_collection",
  "questionCount": 0,
  "questionBudget": { "recommended": 18, "maximum": 24 },
  "focus": ["information-processing", "decision-making"],
  "scenes": [
    {
      "id": "scene-01",
      "domain": "work",
      "summary": "最近一次需要在信息不完整时做决定的经历"
    }
  ],
  "askedQuestionIds": ["context-01", "perception-01"],
  "evidence": [],
  "uncertainties": ["Ni_vs_Ne"],
  "skippedQuestions": [],
  "calibration": null
}
```

## 转换规则

### Consent -> Context

用户明确同意探索，并知道结果不是诊断。若用户拒绝，不继续追问。

### Context -> Evidence collection

至少获得一个具体事件或场景。用户只给抽象自评时，追问最近一次真实经历。

### Evidence collection -> Hypothesis

至少覆盖两个领域，或用户明确要求提前结束。每个主要判断至少有一个行为证据；证据不足时保留未知。

### Hypothesis -> Calibration

先用自然语言总结，不展示未经解释的功能代码。询问用户哪些观察符合、哪些不符合，以及哪些表现只是工作要求。

### Calibration -> Report

吸收用户修正，保留相反证据和未解决问题，然后生成候选类型与 HTML 报告。

## 提问规则

- 参考 [`grill-me-protocol.md`](grill-me-protocol.md) 渐进式展开；
- 一次只问一个问题，并等待用户回答；
- 每次提问给出简短的提问目的和推荐回答方式；
- 优先问最近的具体事件；
- 不要求用户选择 MBTI 字母；
- 不连续询问同一维度超过两题；
- 用户不确定时记录 unknown，不强行解释；
- 用户疲劳、拒答或回答过短时可以提前进入低置信度报告；
- 每个追问必须减少一个明确的不确定性；
- `questionCount` 达到 18 且证据足够时优先结束；
- `questionCount` 不得超过 24；
- 达到上限后保留未知项，不为了补齐八维而继续提问。

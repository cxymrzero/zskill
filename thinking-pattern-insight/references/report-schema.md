# Report Schema

报告分析结果与 HTML 渲染分离。以下结构是建议的最小协议。

```json
{
  "meta": {
    "version": "0.1",
    "generatedAt": "2025-01-01T00:00:00Z",
    "confidence": "medium"
  },
  "summary": {
    "headline": "你倾向于先形成整体判断，再组织行动",
    "paragraphs": ["..."],
    "bullets": ["..."]
  },
  "functions": [
    {
      "code": "Ni",
      "label": "寻找长期主线",
      "score": 78,
      "level": "明显",
      "confidence": "medium",
      "description": "...",
      "evidence": ["..."],
      "counterEvidence": ["..."]
    }
  ],
  "preferences": [
    {
      "axis": "EI",
      "left": { "code": "I", "label": "内部整理", "value": 68 },
      "right": { "code": "E", "label": "外部互动", "value": 32 },
      "summary": "较偏向内部整理",
      "confidence": "medium"
    }
  ],
  "typeCandidates": [
    {
      "type": "INTJ",
      "confidence": "medium",
      "reason": ["..."],
      "distinguishingQuestion": "..."
    }
  ],
  "experiments": ["..."]
}
```

`score` 是当前证据支持度。对用户展示时必须同时显示自然语言等级和解释。图表必须有对应的文本列表。

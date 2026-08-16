# zskill

用多元思维模型帮助用户重构问题、生成不同方案并采取下一步行动的 skills。

## MVP

- `many-minds`：用户手动调用的入口，根据问题选择思考路径。
- `creative-reframing`：用三个正交模型重构问题并生成方案。
- `iching-reframing`：用《易经》六十四卦进行原型式重构，不作预测。
- `thinking-pattern-insight`：通过情境访谈探索思维偏好，并生成自然语言优先的 HTML 报告。

情绪引导暂不属于 MVP。ACT、CBT、斯多葛主义等方法将在安全边界、危机处理和完成标准单独设计后加入。

## 安装与使用

这些 skills 遵循 Agent Skills 的 `SKILL.md` 结构。同一份源文件可供 Claude Code、Codex 和 pi 使用。

### 安装到 Claude Code、Codex 和 pi

全局安装仓库中的 skills：

```bash
npx --yes skills add cxymrzero/zskill \
  --global \
  --agent claude-code \
  --agent codex \
  --agent pi \
  --skill '*' \
  --yes
```

仅安装到当前项目时去掉 `--global`。安装后开启一个新会话，让 agent 重新发现 skills。

也可以先查看仓库中可用的 skills：

```bash
npx --yes skills add cxymrzero/zskill --list
```

不同 agent 的显式调用方式：

```text
# Claude Code
/many-minds 我们的产品试用用户很多，但付费转化一直很低，怎样找到新解法？

# Codex
$many-minds 我们的产品试用用户很多，但付费转化一直很低，怎样找到新解法？

# pi
/skill:many-minds 我们的产品试用用户很多，但付费转化一直很低，怎样找到新解法？
```

也可以直接调用 `creative-reframing`、`iching-reframing` 或 `thinking-pattern-insight`。显式调用最可预测；允许模型调用的子 skills 也可以根据描述自动触发。

更新与删除：

```bash
npx skills update --global
npx skills remove --global \
  --agent claude-code \
  --agent codex \
  --agent pi \
  --skill many-minds \
  --skill creative-reframing \
  --skill iching-reframing \
  --skill thinking-pattern-insight \
  --yes
```

### pi 原生 package

pi 用户也可以直接从 Git 安装整个 package：

```bash
pi install git:github.com/cxymrzero/zskill
pi install git:github.com/cxymrzero/zskill@v0.2.0  # 固定版本
```

管理 pi package：

```bash
pi list
pi update --extensions
pi remove git:github.com/cxymrzero/zskill
```

固定到 tag 的安装不会被 `pi update --extensions` 移动到新版本；发布新 tag 后，需要使用新的 `@版本` 再次执行 `pi install`。

### 本地验证

```bash
npx --yes skills add . --list

pi --no-skills \
  --skill ./many-minds \
  --skill ./creative-reframing \
  --skill ./iching-reframing \
  --skill ./thinking-pattern-insight
```


## 发布

提交代码并创建版本 tag：

```bash
git add .
git commit -m "feat: publish initial multi-model skills"
git push origin main
git tag v0.2.0
git push origin v0.2.0
```

公开仓库发布前应添加明确的开源许可证。后续也可以把该 package 发布到 npm；`package.json` 已包含 `pi-package` 关键词和 pi skill manifest。


## 设计原则

1. 模型用于改变观察角度，不替代事实调查。
2. 输出必须落到可执行、可验证的行动实验。
3. 不把象征性解释包装成预测、诊断或权威结论。
4. 新模型优先加入 `references/`，主流程保持短小稳定。

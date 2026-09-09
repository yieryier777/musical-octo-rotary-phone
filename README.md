# my-ai-learning-hub（musical-octo-rotary-phone）

个人 AI 概念学习仓库：用一个自建的**项目级 Skill**（concept-learning）按统一框架学习新概念，把学习成果沉淀为可复习、可分享、可核查的 HTML 资料。本仓库也是课程作业 1 的提交内容，后续课程项目的学习资料和个人 Skill 将在此基础上继续扩展。

## 仓库结构

```
musical-octo-rotary-phone/
├── .workbuddy/
│   └── skills/
│       └── concept-learning/
│           └── SKILL.md            # 项目级 Skill：概念学习资料生成器
├── learning-materials/
│   ├── agent.html                  # 概念一：Agent（AI 智能体）
│   ├── llm-context.html            # 概念二：大模型的上下文
│   ├── skill.html                  # 概念三：Skill（智能体技能）
│   └── concept-relationship.html   # 三个概念的关系说明（含流程图与 Mermaid 源码）
├── README.md
└── .gitignore                      # 排除敏感信息与临时文件
```

## Skill：concept-learning

- **存放路径**：`.workbuddy/skills/concept-learning/SKILL.md`（项目级 Skill，随本仓库共享）
- **功能**：输入任意一个概念名称，按固定学习框架生成一份自包含 HTML 学习资料，包含：学习目标、核心问题、个人化解释（费曼式）、核心机制与组成、具体应用场景、概念辨析与使用边界、**互动课后自测**（点击作答、即时判分、附答案解析的选择题）、可核查的参考来源，以及人工核查记录。
- **设计要点**：
  - 强制"来源先行"：3–6 条来源，优先官方文档/经典论文，每条链接生成前必须逐一核实可访问，且标注支撑了哪部分内容；
  - 强制个人化解释：用自己的话和类比，禁止照搬来源或 AI 对话原文；
  - 强制自检清单：个人解释可读性、机制准确性、场景具体性、辨析覆盖度、链接可达性等逐项核对后才算完成。

## 如何在 WorkBuddy 中调用

1. 将本仓库克隆到本地，在 WorkBuddy 中以本仓库目录作为工作区打开（项目级 Skill 位于仓库根目录 `.workbuddy/skills/`，会被自动发现）；
2. 直接对 AI 说：**"使用 concept-learning 技能，学习〈概念名〉"**（例如："使用 concept-learning 学习 RAG"）；
3. AI 加载 SKILL.md 并按其流程执行，产出的学习资料保存到 `learning-materials/<概念名>.html`；
4. 生成后请**务必人工阅读核查**，并在资料末尾的"人工核查记录"中补充你修改过的内容。

> 备选方式：任何能读取文件的 AI 助手中，直接让它读取 `.workbuddy/skills/concept-learning/SKILL.md` 并按其中流程执行，效果等同。

## 已生成的学习资料

| 文件 | 概念 | 一句话概括 |
| --- | --- | --- |
| `learning-materials/agent.html` | Agent | 给大模型装上工具和循环，让它自主干到做完为止 |
| `learning-materials/llm-context.html` | 大模型的上下文 | 模型一次推理能"看见"的全部信息，即它的工作记忆 |
| `learning-materials/skill.html` | Skill | 沉淀为 SKILL.md、按需注入上下文的任务方法 |
| `learning-materials/concept-relationship.html` | 三者关系 | 上下文是 Agent 的决策依据，Skill 是注入上下文的可复用知识 |

## AI 使用与人工核查说明

**AI 参与的部分**：仓库结构设计、SKILL.md 初稿、三份概念资料的初稿、关系图、Git 命令执行。

**本人核查与修改的部分**（详见每份 HTML 末尾的"人工核查记录"）：

1. **来源逐条核实**：三份资料共引用 10 条来源（Anthropic 官方文档与工程博客、arXiv 论文、Lilian Weng 博客），全部逐一验证可访问后才保留；其中 Building Effective Agents 一文的链接从已迁移的 `/research/` 路径修正为官方当前的 `/engineering/` 路径，上下文官方文档一条 302 跳转失效后替换为等效的工程博客文章。
2. **事实校对**：对照来源核对关键表述——如 Workflow 与 Agent 的划分标准（流程由代码还是模型决定）、Skill 的渐进披露机制、Lost in the Middle 现象；修正了初稿中"Skill 常驻上下文"的错误说法。
3. **个人化改写**：应用场景全部替换为本次作业的真实过程（含 github.com 连接失败后改用 API 的真实经历），拒绝保留 AI 初稿中"企业自动化办公"式的泛泛示例；个人解释部分按自己的理解重写。
4. **结构与表述调整**：补充辨析条目（"单次工具调用 ≠ Agent"等）、删除无法核实的具体数字、统一三份资料的章节结构。
5. **课后自测互动化**：三份概念资料原有的折叠式"自测问题"升级为**可交互的选择题**（点击选项即时判分、自动展开答案解析、统计得分、支持重做），关系页新增 4 道综合选择题；题干与解析由原自测内容改写并逐题人工核对（正确答案与知识点一一对应），实现方式为内嵌原生 JavaScript，无任何外部依赖。SKILL.md 的生成流程与自检清单已同步更新——今后用该 Skill 学习新概念，产出的资料将自动带互动自测环节。

## 遇到的问题与解决记录

- **问题**：`git clone` 报错 `Failed to connect to github.com port 443`（Connection reset / 超时），本机无代理。
  **诊断**：DNS 解析正常（20.205.243.166 为 GitHub 真实 IP），但 TCP 层无法连通 github.com 及其多个镜像 IP；而 `api.github.com`、`codeload.github.com` 可以正常访问。
  **解决**：改用 GitHub REST API（api.github.com）完成文件推送，本地仍保留完整的 git 提交历史；此后若网络恢复，可直接 `git push -u origin main`。

## 敏感信息与安全

- 仓库中不含任何 API Key、Token、密码或个人隐私信息；
- `.gitignore` 已排除 `.env`、`*.key`、`*token*`、`secrets/` 等常见敏感文件与临时文件；
- 学习资料中引用的均为公开可访问链接。

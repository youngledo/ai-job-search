# AI Job Search

这是一个基于 Claude Code 的 AI 求职工作区。你可以把它作为个人求职仓库使用，
填入个人资料，让 Claude 帮你评估岗位、定制简历、写求职信、准备面试，并记录
申请结果。

本文件是中文使用导览，重点说明中国大陆求职场景下如何使用 `markets/china/`
overlay。完整英文说明见 [README.md](README.md)。

## 适用地区

本项目适用于中国大陆地区的求职场景，默认围绕 BOSS 直聘、猎聘、拉勾、
脉脉、公司官网等常见渠道的使用方式设计。当前采用手动保存岗位 JD 的方式，
不自动抓取招聘网站，也不自动登录、私信或投递。

为了把中国大陆地区的求职流程和主工作流解耦，相关内容集中放在独立 overlay
中：

- `.claude/commands/china.md`: `/china` 命令入口。
- `markets/china/profile/`: 中文候选人资料、求职偏好、事实证据库。
- `markets/china/jobs/inbox/`: 手动保存的岗位 JD。
- `markets/china/jobs/evaluated/`: 岗位评估、申请材料、排序报告和面试准备输出。
- `markets/china/templates/`: BOSS 打招呼、猎头私信、中文求职信、跟进消息和面试回答模板。
- `markets/china/workflows/`: `/china` 各子命令读取的工作流说明。

这样做的目的是让主流程保持清晰，同时支持中国大陆地区的实际求职流程。

## 适合谁使用

适合你，如果你希望：

- 长期维护一套个人求职资料库。
- 针对每个岗位先判断是否值得投递或沟通。
- 为 BOSS 直聘、猎聘、拉勾、脉脉、公司官网等岗位生成更有针对性的沟通话术。
- 基于事实证据库生成简历修改建议、中文求职信和面试回答。
- 希望在不改动主流程的前提下使用中国大陆地区的求职流程。

不适合你，如果你希望：

- 自动登录招聘网站。
- 自动批量抓取岗位。
- 自动投递或自动私信招聘者。
- 把 BOSS 直聘当成可无限抓取的数据源。

## 前置要求

基础要求：

- Claude Code CLI。
- Python 3.10+。
- 如果使用 LaTeX CV / cover letter 编译流程，需要安装 `lualatex` 和 `xelatex`。
- 可选：`pdftotext`，用于 `/apply` 的 ATS 文本层检查。
- 如果使用招聘网站 CLI，需要安装 Bun 并执行对应 `bun install`。

中国求职 overlay 本身没有新增运行时依赖。第一版只使用手动保存的岗位 JD。

## 快速开始

### 1. 启动 Claude Code

在仓库根目录运行：

```bash
claude
```

### 2. 初始化中国求职资料

在 Claude Code 中运行：

```text
/china setup
```

它会引导你完善：

- `markets/china/profile/candidate.md`: 中文候选人档案。
- `markets/china/profile/preferences.md`: 目标岗位、城市、薪资、公司偏好、硬性排除条件。
- `markets/china/profile/evidence.md`: 事实证据库，用于约束简历、话术和面试回答不编造。

如果你已经有中文简历，可以先放到 `documents/cv/`，再让 `/china setup` 参考。

### 3. 保存岗位 JD

从招聘网站手动复制岗位描述，保存到：

```text
markets/china/jobs/inbox/<company>-<role>.md
```

示例：

```text
markets/china/jobs/inbox/bytedance-backend-engineer.md
markets/china/jobs/inbox/tencent-product-manager.md
```

`markets/china/jobs/` 下的岗位 JD、评估报告和申请材料属于个人求职数据，默认被
`.gitignore` 忽略，不应提交到仓库。

建议文件中至少包含：

- 公司名。
- 岗位名。
- 城市和办公方式。
- 薪资范围，如果 JD 中有写。
- 岗位职责。
- 任职要求。
- 加分项。
- JD 来源，例如 BOSS 直聘、猎聘、公司官网。

### 4. 分析单个岗位

```text
/china analyze markets/china/jobs/inbox/bytedance-backend-engineer.md
```

输出会写入 `markets/china/jobs/evaluated/`，通常包括：

- 岗位事实提取。
- 技术匹配、经验匹配、领域匹配、沟通匹配、薪资/地点匹配、成长匹配评分。
- 主要优势。
- 主要 gap。
- 红旗风险。
- 推荐下一步。
- BOSS / 猎头沟通角度。

### 5. 生成申请材料

如果岗位值得推进：

```text
/china apply markets/china/jobs/inbox/bytedance-backend-engineer.md
```

它会生成：

- BOSS 直聘打招呼话术。
- 招聘者 / 猎头私信。
- 中文求职信或邮件。
- 简历修改建议。
- 面试准备重点。
- 需要你确认的信息和必须保持诚实的 gap。

### 6. 多岗位排序

当 `markets/china/jobs/inbox/` 中有多个岗位：

```text
/china rank
```

输出会写入：

```text
markets/china/jobs/evaluated/ranking-YYYY-MM-DD.md
```

### 7. 面试准备

```text
/china interview markets/china/jobs/evaluated/<job>.md
```

或直接对原 JD：

```text
/china interview markets/china/jobs/inbox/<job>.md
```

它会生成：

- 高频面试问题。
- STAR / CAR 回答框架。
- 项目深挖准备。
- 你应该反问的问题。
- 薪资、地点、稳定性等敏感问题的应对思路。

## `/china` 命令速查

```text
/china setup
/china analyze markets/china/jobs/inbox/<job>.md
/china apply markets/china/jobs/inbox/<job>.md
/china rank
/china interview markets/china/jobs/evaluated/<job>.md
```

## 与通用工作流的关系

你可以同时使用两套工作流：

- 使用 `/china ...` 处理中国市场岗位、BOSS 打招呼、中文材料和面试准备。
- 使用 `/setup`、`/apply`、`/rank`、`/outcome` 处理通用或英文申请流程。

长期申请状态仍然可以记录在根目录的 `job_search_tracker.csv`。如果你希望保留
完整申请材料，也可以继续使用 `documents/applications/`。

## 注意事项

- 不要把招聘网站账号、cookie、token 或私人聊天记录提交到仓库。
- 不要让工具替你自动登录、自动私信或自动投递。
- 对 JD 中没有写清的信息，输出中应标记为缺失信息，而不是猜测。
- 对你没有证据支撑的技能或成果，必须标记为 gap 或待确认，不能写成已有经验。
- 如果要公开仓库，先确认 `markets/china/profile/`、`markets/china/jobs/` 和 `job_search_tracker.csv`
  中没有个人隐私。

## License

本项目使用 MIT License。详见 [LICENSE](LICENSE)。

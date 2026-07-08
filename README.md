# AI Job Search - 中国大陆求职版

这是一个基于 Claude Code 的 AI 求职工作区，面向中国大陆地区的求职流程做了本地化：
你可以维护个人资料和事实证据库，手动保存岗位 JD，让 Claude 帮你评估岗位、生成
BOSS 直聘打招呼话术、招聘者私信、中文求职信、简历修改建议和面试准备材料。

英文通用说明保留在 [README.en.md](README.en.md)。

> 本项目不会自动登录、抓取、私信或投递任何招聘平台。中国大陆版默认使用手动保存
> 岗位 JD 的方式，避免把招聘网站账号、聊天记录、cookie 或个人求职数据提交到仓库。

## 适用场景

适合你，如果你希望：

- 长期维护一套个人求职资料库。
- 针对每个岗位先判断是否值得沟通或投递。
- 为 BOSS 直聘、猎聘、智联招聘、前程无忧、脉脉、领英、公司官网等渠道的岗位生成
  更有针对性的沟通材料。
- 根据事实证据库生成中文简历修改建议、中文求职信和面试回答。
- 保留上游通用能力，同时把中国大陆地区差异隔离在 `markets/china/` 下。

不适合你，如果你希望：

- 自动登录招聘网站。
- 自动批量抓取岗位。
- 自动投递或自动私信招聘者。
- 把招聘网站当成可无限采集的数据源。

## 核心结构

中国大陆相关内容集中在独立市场层：

- `.claude/commands/china.md`: `/china` 命令入口。
- `markets/china/profile/`: 中文候选人资料、求职偏好、事实证据库。
- `markets/china/jobs/inbox/`: 手动保存的岗位 JD。
- `markets/china/jobs/evaluated/`: 岗位评估、申请材料、排序报告和面试准备输出。
- `markets/china/templates/`: BOSS 打招呼、招聘者私信、中文求职信、跟进消息和面试回答模板。
- `markets/china/workflows/`: `/china` 各子命令读取的工作流说明。
- `cv/chinese/`: 中文简历 LaTeX 模板。
- `cover_letters/chinese/`: 中文求职信 LaTeX 模板。

个人岗位数据和生成材料默认被 `.gitignore` 忽略，不应提交到公开仓库。

## 前置要求

- [Claude Code](https://claude.com/claude-code) CLI。
- Python 3.10+。
- 可选：LaTeX 发行版，例如 TeX Live、MacTeX、TinyTeX 或 MiKTeX。
- 可选：`pdftotext`，用于通用 `/apply` 工作流的 ATS 文本层检查。
- 可选：Bun，仅当你要使用上游提供的招聘搜索 CLI 时需要。

如果要编译中文 LaTeX 模板，需要安装支持中文字体的 TeX 环境。Linux 通常需要安装
`fonts-noto-cjk`；macOS 和 Windows 通常可以使用系统自带中文字体。

## 快速开始

### 1. 启动 Claude Code

在仓库根目录运行：

```bash
claude
```

### 2. 初始化中国大陆求职资料

在 Claude Code 中运行：

```text
/china setup
```

它会引导你完善：

- `markets/china/profile/candidate.md`: 中文候选人档案。
- `markets/china/profile/preferences.md`: 目标岗位、城市、薪资、公司偏好、硬性排除条件。
- `markets/china/profile/evidence.md`: 事实证据库，用于约束简历、话术和面试回答不编造。

如果你已经有中文简历，可以先放到 `documents/cv/`，再让 `/china setup` 参考。

### 3. 手动保存岗位 JD

从招聘网站或公司官网复制岗位描述，保存到：

```text
markets/china/jobs/inbox/<company>-<role>.md
```

示例：

```text
markets/china/jobs/inbox/bytedance-backend-engineer.md
markets/china/jobs/inbox/tencent-product-manager.md
```

建议文件中至少包含：

- 公司名。
- 岗位名。
- 城市和办公方式。
- 薪资范围和薪数，如果 JD 中有写，例如 `20k-30k * 14薪`。
- 岗位职责。
- 任职要求。
- 加分项。
- JD 来源，例如 BOSS 直聘、猎聘、智联招聘、前程无忧、脉脉、领英或公司官网。

### 4. 分析单个岗位

```text
/china analyze markets/china/jobs/inbox/bytedance-backend-engineer.md
```

输出会写入 `markets/china/jobs/evaluated/`，通常包括：

- 岗位事实提取。
- 技术匹配、经验匹配、领域匹配、沟通匹配、薪资/地点匹配、成长匹配评分。
- 996、大小周、五险一金、试用期、外包/劳务派遣、薪资薪数等中国大陆求职风险信号。
- 主要优势、主要 gap、红旗风险和推荐下一步。
- BOSS / 招聘者沟通角度。

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
- 薪资、地点、稳定性、加班、试用期等敏感问题的应对思路。

## `/china` 命令速查

```text
/china setup
/china analyze markets/china/jobs/inbox/<job>.md
/china apply markets/china/jobs/inbox/<job>.md
/china rank
/china interview markets/china/jobs/evaluated/<job>.md
```

## 中文 LaTeX 模板

中文简历模板：

```bash
cd cv/chinese
lualatex -interaction=nonstopmode main_example.tex
```

中文求职信模板：

```bash
cd cover_letters/chinese
xelatex -interaction=nonstopmode cover_example.tex
```

模板文件只包含占位符，适合提交到仓库。实际生成的个人 PDF、日志和申请材料会被
`.gitignore` 忽略。

## 与通用工作流的关系

你可以同时使用两套工作流：

- 使用 `/china ...` 处理中国大陆岗位、BOSS 打招呼、中文材料和面试准备。
- 使用 `/setup`、`/apply`、`/rank`、`/interview`、`/outcome` 处理通用或英文申请流程。

长期申请状态仍然可以记录在根目录的 `job_search_tracker.csv`。如果你希望保留完整申请
材料，也可以继续使用 `documents/applications/`。

## 隐私注意事项

- 不要提交招聘网站账号、cookie、token 或私人聊天记录。
- 不要让工具替你自动登录、自动私信或自动投递。
- 对 JD 中没有写清的信息，输出中应标记为缺失信息，而不是猜测。
- 对你没有证据支撑的技能或成果，必须标记为 gap 或待确认，不能写成已有经验。
- 如果要公开仓库，先确认 `markets/china/profile/`、`markets/china/jobs/`、
  `documents/` 和 `job_search_tracker.csv` 中没有个人隐私。

## License

本项目使用 MIT License。详见 [LICENSE](LICENSE)。

# 中国大陆求职 Overlay

这个目录提供面向中国大陆地区的求职扩展层。它不替换主工作流；中国大陆市场
相关资料、岗位、模板和输出都放在 `markets/china/` 下，便于后续扩展其他地区。

## 使用方式

在 Claude Code 中使用：

```text
/china setup
/china scrape
/china analyze markets/china/jobs/inbox/<job>.md
/china apply markets/china/jobs/inbox/<job>.md
/china rank
/china interview markets/china/jobs/evaluated/<job>.md
```

## 推荐流程

1. 运行 `/china setup`，初始化并填写 `documents/china/profile/` 下的个人资料。
   模板位于 `markets/china/profile/`（tracked），个人数据写入 `documents/china/profile/`
   （gitignored，不会提交到仓库）。
2. 运行 `/china scrape`，从 BOSS 直聘、猎聘、智联招聘、前程无忧、脉脉、国聘、
   公司官网等公开来源低频搜索岗位。
3. 如果公开页面可读取，工具会保存完整 JD；如果遇到登录、反爬或内容不完整，
   工具会保存待手动补全文件。
4. 也可以手动复制岗位 JD 到 `markets/china/jobs/inbox/<company>-<role>.md`。
5. 运行 `/china analyze <file>` 判断是否值得沟通或投递。
6. 对值得推进的岗位运行 `/china apply <file>`，生成打招呼话术、招聘者私信、
   中文求职信/邮件和简历修改建议。
7. 面试前运行 `/china interview <file>` 准备常见问题、STAR/CAR 答案和反问问题。

长期申请状态可以继续记录在仓库根目录的 `job_search_tracker.csv`。

`markets/china/jobs/` 下的岗位 JD、评估报告和申请材料属于个人求职数据，默认被
`.gitignore` 忽略，不应提交到仓库。

## 边界

- 只做低频公开搜索和公开页面读取。
- 不登录、私信、投递或操作任何招聘平台账号。
- 不绕过登录、验证码、反爬或访问限制。
- 自动读取失败时，退回到手动补全 JD。
- 不高频批量采集岗位。
- 不生成无法由 `documents/china/profile/evidence.md` 或 profile 文件支撑的经历陈述。
- 对缺失技能或经验要明确标记为 gap，不能包装成已有经验。

## 写作规范（中文标点）

所有写入 `markets/china/` 的中文文本（profile、岗位 JD、评估报告、求职信、BOSS/猎头沟通话术、面试答案、模板等）必须使用**全角中文标点**：

- 括号：`（`、`）`，不要用 `(`、`)`
- 冒号：`：`，不要用 `:`
- 问号：`？`，不要用 `?`
- 感叹号：`！`，不要用 `!`
- 逗号：`，`，不要用 `,`
- 句号：`。`，不要用 `.`
- 分号：`；`，不要用 `;`
- 引号：`""`、`''`（直角引号 `「」` 也接受）

**保留 ASCII 标点的场景**：

- 英文单词、数字之间（如 `Spring Boot`、`12 years`、`28-35K`、`G1`、`OAuth2`）
- Markdown 语法（`|`、`**`、`` ` ``、`#`、`-`、`>`）
- 代码、命令行、文件路径、URL
- 日期与版本号区间（如 `2021.12-至今`、`2024.06-2024.12`、`v1.2.3`）

**判断口诀**：夹在两个汉字之间的 ASCII 标点必须替换为全角；夹在英文/数字之间、或属于 Markdown 语法/代码/路径的 ASCII 标点保留不变。

## 目录说明

- `profile/`: 个人资料、求职偏好和事实证据库的**模板**（tracked，只读）。实际
  个人数据写入 `documents/china/profile/`（gitignored）。
- `search-queries.md`: 中国大陆公开岗位搜索查询配置。
- `jobs/inbox/`: 手动保存的岗位 JD。
- `jobs/evaluated/`: 岗位评估、申请材料和排序报告输出。
- `jobs/archived/`: 已处理岗位归档。
- `workflows/`: `/china` 命令读取的具体工作流。
- `templates/`: 中国市场沟通、求职信和面试回答模板。

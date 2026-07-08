# 中国大陆求职 Overlay

这个目录提供面向中国大陆地区的求职扩展层。它不替换主工作流；中国大陆市场
相关资料、岗位、模板和输出都放在 `markets/china/` 下，便于后续扩展其他地区。

## 使用方式

在 Claude Code 中使用：

```text
/china setup
/china analyze markets/china/jobs/inbox/<job>.md
/china apply markets/china/jobs/inbox/<job>.md
/china rank
/china interview markets/china/jobs/evaluated/<job>.md
```

## 推荐流程

1. 运行 `/china setup`，填写 `markets/china/profile/` 下的个人资料。
2. 从 BOSS 直聘、猎聘、智联招聘、前程无忧、脉脉、公司官网等渠道手动复制岗位 JD。
3. 将岗位保存为 `markets/china/jobs/inbox/<company>-<role>.md`。
4. 运行 `/china analyze <file>` 判断是否值得沟通或投递。
5. 对值得推进的岗位运行 `/china apply <file>`，生成打招呼话术、招聘者私信、
   中文求职信/邮件和简历修改建议。
6. 面试前运行 `/china interview <file>` 准备常见问题、STAR/CAR 答案和反问问题。

长期申请状态可以继续记录在仓库根目录的 `job_search_tracker.csv`。

`markets/china/jobs/` 下的岗位 JD、评估报告和申请材料属于个人求职数据，默认被
`.gitignore` 忽略，不应提交到仓库。

## 边界

- 不自动抓取招聘网站。
- 不登录、私信、投递或操作任何招聘平台账号。
- 不批量采集岗位。
- 不生成无法由 `markets/china/profile/evidence.md` 或 profile 文件支撑的经历陈述。
- 对缺失技能或经验要明确标记为 gap，不能包装成已有经验。

## 目录说明

- `profile/`: 个人资料、求职偏好和事实证据库。
- `jobs/inbox/`: 手动保存的岗位 JD。
- `jobs/evaluated/`: 岗位评估、申请材料和排序报告输出。
- `jobs/archived/`: 已处理岗位归档。
- `workflows/`: `/china` 命令读取的具体工作流。
- `templates/`: 中国市场沟通、求职信和面试回答模板。

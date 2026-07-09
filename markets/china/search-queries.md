# 中国大陆岗位搜索查询

`/china scrape` 使用本文件生成低频公开搜索查询。不要在这里放账号、cookie、
私聊内容或任何需要登录后才能访问的信息。

## 默认站点

- BOSS 直聘: `site:zhipin.com`
- 猎聘: `site:liepin.com`
- 智联招聘: `site:zhaopin.com`
- 前程无忧: `site:51job.com`
- 脉脉: `site:maimai.cn`
- 国聘: `site:iguopin.com`
- 公司官网招聘页: 公司名 + `招聘` / `社会招聘` / `校园招聘` / `careers`

领英不作为中国大陆默认搜索渠道。如用户明确寻找外企、出海岗位或英文岗位，可以把
领英链接作为手动 JD 来源处理。

## 查询模板

将 `[ROLE]`、`[CITY]`、`[DOMAIN]`、`[SKILL]` 替换为
`markets/china/profile/preferences.md` 和用户参数中的信息。

### 优先岗位

```text
site:zhipin.com "[ROLE]" "[CITY]"
site:liepin.com "[ROLE]" "[CITY]"
site:zhaopin.com "[ROLE]" "[CITY]"
site:51job.com "[ROLE]" "[CITY]"
site:iguopin.com "[ROLE]" "[CITY]"
```

### 领域 / 行业

```text
site:zhipin.com "[DOMAIN]" "[ROLE]" "[CITY]"
site:liepin.com "[DOMAIN]" "[ROLE]" "[CITY]"
site:zhaopin.com "[DOMAIN]" "[ROLE]" "[CITY]"
site:iguopin.com "[DOMAIN]" "[ROLE]" "[CITY]"
```

### 技能关键词

```text
site:zhipin.com "[SKILL]" "[ROLE]" "[CITY]"
site:liepin.com "[SKILL]" "[ROLE]" "[CITY]"
site:51job.com "[SKILL]" "[ROLE]" "[CITY]"
site:maimai.cn "[SKILL]" "[ROLE]" "[CITY]"
```

### 公司官网

```text
"[TARGET_COMPANY]" "[ROLE]" 招聘
"[TARGET_COMPANY]" 社会招聘 "[ROLE]"
"[TARGET_COMPANY]" careers "[ROLE]"
```

## 结果处理

- 只处理看起来仍在招聘的岗位。
- 优先保留发布时间近、城市匹配、职位描述较完整的结果。
- 如果搜索结果只有标题和摘要，不要补写缺失 JD；保存为待手动补全文件。
- 如果页面需要登录、出现验证码、反爬提示或内容不足，不要绕过限制。

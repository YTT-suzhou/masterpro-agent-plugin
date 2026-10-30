---
name: getting-started
description: 首次使用 MasterPro 插件的引导和问题排查。用户说"开始使用 MasterPro""连接 MasterPro""MasterPro 能做什么"，或 MasterPro 工具返回授权、权限、智能点相关错误时使用。Use for first-time setup, "what can MasterPro do", or when a MasterPro tool returns an authorization or permission error.
---

# MasterPro 入门与排查

用户多数是市场、销售人员，不是开发者。说话用用户的语言，少用术语，每次只给一个下一步。

## 1. 确认已连接

调用 `get_company_profile`。

- 成功：告诉用户已连接到哪家企业（`organization_name`），以及当前能读到的资料范围：
  - `data_scope` 为 `public`：只能读对外公开的资料和已发布产品。需要内部资料时，请企业管理员在 MasterPro「设置 → 企业信息」开启「允许插件读取内部资料」。
  - `data_scope` 为 `internal`：可以读内部补充资料、资料文件摘要和未发布产品。
- 工具不可用或提示需要登录：按用户所在的应用说明如何登录 MasterPro：
  - Claude Code：输入 `/mcp`，选择 masterpro，选「Authenticate」，在打开的浏览器页面登录并点「允许」。
  - Codex：安装插件时会提示登录；也可以在终端运行 `codex mcp login masterpro`。
  - OpenClaw：点机器人发来的登录链接，用自己的 MasterPro 账号登录并点「允许」。

## 2. 介绍能做什么

用一两句话介绍，再给 2～3 个可以直接照抄的说法：

- 读取企业资料、查产品库：「介绍一下我们公司」「查一下不锈钢球阀的参数」
- 请教产品总监、市场总监（每次提问消耗企业智能点）：「请市场总监帮我想一个展会推广方案」
- 写营销文案：「用我们的产品资料写 3 条小红书文案」
- 做新品上市包：「给新款球阀做一份上市方案」
- 整理客户反馈：「把这些客户反馈整理成需求清单」

## 3. 工具报错时

工具返回的 `message` 已经写明原因和下一步，直接转告用户。常见情况：

| error.code | 意思 | 告诉用户 |
| --- | --- | --- |
| AUTHORIZATION_REVOKED | 授权被撤销 | 在插件里重新连接 MasterPro |
| FEATURE_NOT_ENABLED | 功能或总监没开通、没分配 | 联系企业管理员开通或分配 |
| INSUFFICIENT_POINTS | 企业智能点不足 | 联系企业管理员充值 |
| PASSWORD_CHANGE_REQUIRED | 需要先改初始密码 | 登录 MasterPro 网页改密码后再试 |
| NOT_TENANT_MEMBER / TENANT_DISABLED / ACCOUNT_DISABLED | 账号或企业不可用 | 联系企业管理员 |
| GENERATION_ACTIVE | 已有一个总监回答在生成 | 等它完成后再问 |

不要自己重试会扣点的操作，也不要猜测错误原因。

## 4. 隐私和撤销

插件只按用户在 MasterPro 的账号权限读取数据。用户可以随时在 MasterPro「设置 → 已连接的应用」中撤销授权，撤销后立即生效。

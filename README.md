# MasterPro AI 助手插件

在 Claude、Codex、OpenClaw 等 AI 助手里直接使用 MasterPro：

- **读取企业资料和产品库**：写内容时用企业的真实信息，不再手动复制粘贴
- **请教产品总监、市场总监**：在 AI 助手里直接提问，对话也会同步到 MasterPro 工作台
- **写好的工作流程**：营销文案、新品上市包、客户反馈整理成需求

适合市场、销售和产品人员使用，不需要编程。

## 安装

| 你在用 | 安装说明 |
| --- | --- |
| Claude 桌面版、网页版、Claude Code | [docs/install-claude.md](docs/install-claude.md) |
| Codex（桌面版、命令行） | [docs/install-codex.md](docs/install-codex.md) |
| OpenClaw 机器人（给部署者看） | [docs/install-openclaw.md](docs/install-openclaw.md) |

安装后用你的 MasterPro 账号登录并授权一次即可。Claude Code 用户可以一条命令安装：

```
/plugin install masterpro --marketplace YTT-suzhou/masterpro-agent-plugin
```

## 可以这样说

- 「用 MasterPro 介绍一下我们公司」
- 「查一下不锈钢球阀的规格，写 3 条小红书推广文案」
- 「请市场总监为新款球阀做一份上市方案」
- 「把下面这些客户反馈整理成需求清单，请产品总监排优先级」

## 数据和权限

- 插件按你在 MasterPro 的账号权限读取数据，看不到其他企业或其他同事的对话。
- 默认只读取企业对外公开的资料和已发布产品。企业管理员可以在 MasterPro「设置 → 企业信息」开启「允许插件读取内部资料」。
- 向总监提问会消耗企业智能点；读取资料和产品不消耗。
- 授权长期有效，持续使用不需要重复登录。随时可以在 MasterPro「设置 → 已连接的应用」中撤销，撤销后立即生效。
- 你在 AI 助手里查到的内容会发送给该 AI 助手的服务商处理，请按企业的数据管理要求使用。

## 遇到问题

工具报错时，AI 助手会转告原因和下一步，例如「联系企业管理员开通功能」「请管理员充值智能点」「在插件里重新连接」。其他问题请联系你的 MasterPro 企业管理员。

## 仓库结构

```
.claude-plugin/marketplace.json     Claude Code 插件市场
.agents/plugins/marketplace.json    Codex 插件市场
plugins/masterpro/
  .claude-plugin/plugin.json        Claude Code 插件清单
  .mcp.json                         Claude Code 的 MCP 服务配置
  plugin.json                       Agent Plugins 通用清单（Codex 等）
  mcp.json                          Agent Plugins 通用 MCP 服务配置
  skills/                           4 个技能
openclaw/masterpro.json5            OpenClaw 配置片段（每人各自授权）
docs/                               各应用的安装说明
```

MCP 服务地址：`https://app.ytt-ai.com/api/mcp`（Streamable HTTP，OAuth 2.1 授权，支持动态注册和 Client ID Metadata Document）。

# 在 OpenClaw 中使用 MasterPro

这份说明给部署 OpenClaw 机器人的人看。聊天用户不需要安装任何东西：第一次用到 MasterPro 时，机器人会发来登录链接，每个人用自己的 MasterPro 账号授权。

## 必读：每个人必须用自己的账号

OpenClaw 默认让所有聊天对象共用一份凭证。如果按默认方式接入，和机器人聊天的每个人都会用部署者的 MasterPro 账号，能看到部署者能看到的全部企业资料。

所以必须按下面的方式配置 `oauth.identity: "per-requester"`，并且**不要**用 `openclaw plugins install` 安装本仓库的插件包：插件包里自带的服务走共享凭证。

## 1. 添加 MasterPro 服务

把 [`openclaw/masterpro.json5`](../openclaw/masterpro.json5) 的内容合并进 OpenClaw 配置：

```json5
{
  gateway: {
    publicOrigin: "https://openclaw.example.com",
  },
  mcp: {
    servers: {
      masterpro: {
        url: "https://app.ytt-ai.com/api/mcp",
        transport: "streamable-http",
        auth: "oauth",
        oauth: {
          identity: "per-requester",
        },
        requestTimeoutMs: 90000,
      },
    },
  },
}
```

- `gateway.publicOrigin` 换成你的 OpenClaw 网关的公网地址。每个人授权后，浏览器会回到这个地址。
- `requestTimeoutMs`：请教总监时最多等待 45 秒，超时设长一些，避免请求被提前中断。

保存后重启网关，然后检查服务能否连通：

```
openclaw mcp doctor masterpro --probe
```

未登录时返回 401 是正常的，说明服务需要授权。

## 2. 安装技能（可选）

技能是写好的工作流程（入门引导、写营销文案、新品上市包、客户反馈整理成需求）。把本仓库 `plugins/masterpro/skills/` 下的 4 个文件夹复制到以下任一目录：

- 所有工作区共用：`~/.agents/skills/`
- 只给某个工作区：`<工作区>/skills/`

## 3. 告诉聊天用户

可以把这段话发给使用机器人的同事：

> 第一次让机器人用 MasterPro 时，它会发来一个登录链接。点开后用你自己的 MasterPro 账号登录，确认授权页上的企业是你的公司，再点「允许」。以后可以在 MasterPro「设置 → 已连接的应用」中随时撤销。

## 常见问题

- **有人看到了不属于自己的资料**：立即检查 `oauth.identity` 是否为 `"per-requester"`，并让相关人员在 MasterPro「设置 → 已连接的应用」撤销授权。
- **提示功能没开通、智能点不足**：联系 MasterPro 企业管理员。
- **只能读到对外资料**：这是默认设置。需要读取内部资料时，请企业管理员在 MasterPro「设置 → 企业信息」开启「允许插件读取内部资料」。

# 在 Claude 中使用 MasterPro

根据你使用的 Claude 产品选择一种方式。不确定的话，用"Claude 桌面版或网页版"。

## Claude 桌面版或网页版（推荐给非开发者）

只需添加一个连接器，不需要安装任何东西。

1. 打开 Claude，进入「设置 → 连接器（Connectors）」。
2. 点「添加自定义连接器（Add custom connector）」。
3. 名称填 `MasterPro`，地址填：

   ```
   https://app.ytt-ai.com/api/mcp
   ```

4. 点「添加」，再点「连接（Connect）」。浏览器会打开 MasterPro 登录页。
5. 用你的 MasterPro 账号登录，在授权页确认应用和企业无误后点「允许」。
6. 回到 Claude，新开一个对话，试着说：「用 MasterPro 介绍一下我们公司」。

> 看不到「添加自定义连接器」：可能是当前套餐或企业管理员的设置不支持，请联系你的 Claude 管理员。

这种方式提供 MasterPro 的全部工具（企业资料、产品库、产品总监、市场总监）。写文案、上市包等写好的工作流程（技能）需要用下面的 Claude Code 方式安装。

## Claude Code

1. 安装插件：

   ```
   /plugin install masterpro --marketplace YTT-suzhou/masterpro-agent-plugin
   ```

   Claude Code 版本较旧、上面的命令不可用时，分两步：

   ```
   /plugin marketplace add YTT-suzhou/masterpro-agent-plugin
   /plugin install masterpro@masterpro
   ```

2. 登录 MasterPro：输入 `/mcp`，选择 `masterpro`，选「Authenticate」。浏览器打开后登录并点「允许」。
3. 试着说：「用 MasterPro 的产品资料写 3 条 LinkedIn 推广文案」。

插件包含 4 个技能：入门引导、写营销文案、新品上市包、客户反馈整理成需求。

## 常见问题

- **提示授权已撤销**：你或管理员在 MasterPro 撤销了授权。按上面的步骤重新连接。
- **提示功能没开通**：联系企业管理员在 MasterPro 开通或分配对应功能。
- **只能读到对外资料**：这是默认设置。需要读取内部资料时，请企业管理员在 MasterPro「设置 → 企业信息」开启「允许插件读取内部资料」。
- **断开连接**：在 MasterPro「设置 → 已连接的应用」撤销授权，立即生效。

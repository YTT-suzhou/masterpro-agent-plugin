# 在 Codex 中使用 MasterPro

## 团队统一安装（推荐）

由 ChatGPT 工作区管理员操作一次，团队成员就能在插件目录里直接安装：

1. 管理员进入「Admin → Plugins」，从 GitHub 导入仓库 `YTT-suzhou/masterpro-agent-plugin`。
2. 成员打开 Codex 的插件目录（Plugins），找到 MasterPro，点「+」安装。
3. 按提示登录 MasterPro，在授权页确认应用和企业无误后点「允许」。
4. 新开一个对话，试着说：「用 MasterPro 介绍一下我们公司」，或输入 `@` 选择 MasterPro 的技能。

## 个人安装

1. 在终端添加 MasterPro 插件市场：

   ```
   codex plugin marketplace add YTT-suzhou/masterpro-agent-plugin
   ```

2. 安装插件：
   - **命令行**：运行 `codex`，输入 `/plugins`，选择 MasterPro 安装。
   - **桌面版**：重启 Codex 桌面版，打开插件目录（Plugins），选择 MasterPro 插件市场后安装。
3. 安装时会打开浏览器，用你的 MasterPro 账号登录并点「允许」。之后新开一个会话即可使用。

如果没有提示登录，可以在终端运行：

```
codex mcp login masterpro
```

## 只接入工具（不装技能）

```
codex mcp add masterpro --url https://app.ytt-ai.com/api/mcp
codex mcp login masterpro
```

## 常见问题

- **提示授权已撤销**：你或管理员在 MasterPro 撤销了授权。运行 `codex mcp login masterpro` 重新连接。
- **提示功能没开通**：联系企业管理员在 MasterPro 开通或分配对应功能。
- **只能读到对外资料**：这是默认设置。需要读取内部资料时，请企业管理员在 MasterPro「设置 → 企业信息」开启「允许插件读取内部资料」。
- **断开连接**：在 MasterPro「设置 → 已连接的应用」撤销授权，立即生效。

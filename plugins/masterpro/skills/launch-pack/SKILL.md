---
name: launch-pack
description: 用 MasterPro 的产品资料和市场总监，为新品做一份上市包：定位、核心卖点、目标客户、渠道计划、首批文案和常见问题。用户说"新品上市""产品发布""上市方案""推广方案"时使用。Use to build a product launch kit (positioning, key messages, audience, channel plan, launch copy, FAQ) for a product in MasterPro.
---

# 新品上市包

## 1. 确定产品

用 `search_products` 找到要上市的产品，再用 `product_id` 取详情。找到多个时请用户确认是哪一个。
同时调用 `get_company_profile` 了解企业背景。

## 2. 请市场总监出方案

告诉用户这一步会消耗企业智能点，然后调用 `ask_director`：

- `director`: `"market"`
- `question`：写清产品名称、核心规格、目标市场、上市时间和预算（用户没给的写"未定"），并要求按以下结构回答：定位一句话、3～5 个核心卖点、目标客户画像、渠道计划和节奏、风险和需要验证的假设。

返回 `status: "running"` 时，等 `retry_after_seconds` 秒后用 `get_director_reply`（带上 `conversation_id` 和 `message_id`）取回答，不要重复提问。
需要追问时，用同一个 `conversation_id` 继续问。

用户要求产品层面的差异化分析时，可以再问产品总监（`director: "product"`），同样先告知会扣点。

## 3. 整理上市包

按下面的结构输出，用户的语言：

1. **定位**：一句话说清给谁、解决什么问题、和替代方案相比好在哪
2. **核心卖点**：每条附上来自产品资料的依据
3. **目标客户**：画像、购买动机、主要顾虑
4. **渠道计划**：渠道、内容形式、时间节奏
5. **首批文案**：至少 1 条社媒文案、1 段产品介绍、1 封客户邮件
6. **常见问题**：客户可能问的 5～8 个问题和建议回答
7. **待确认事项**：缺少的信息、需要验证的假设

规则：

- 事实只来自工具结果，市场总监的判断要标明是建议。
- 产品 `status` 不是 `published` 时提醒用户：上市前需要在 MasterPro 发布产品。
- 最后附上 `workbench_url`，告诉用户可以在 MasterPro 工作台继续和市场总监讨论。

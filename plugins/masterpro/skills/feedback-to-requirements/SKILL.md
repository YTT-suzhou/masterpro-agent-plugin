---
name: feedback-to-requirements
description: 把客户反馈（聊天记录、邮件、评价、销售笔记、工单）归纳成有优先级的需求清单，并请 MasterPro 产品总监评估。用户说"整理客户反馈""归纳需求""需求清单""写需求文档"时使用。Use to turn raw customer feedback into a prioritized requirements list with the MasterPro product director.
---

# 客户反馈整理成需求

## 1. 收集和脱敏

请用户粘贴反馈原文，或说明反馈来自哪里。
发给 MasterPro 之前，去掉客户的个人信息：姓名、电话、邮箱、地址、订单号等，用"客户 A""客户 B"代替。

## 2. 先自己归纳

把反馈按问题归类，每类记下：

- 用户遇到的问题（不是用户提的解决方案）
- 出现次数，以及 1～2 句有代表性的原话（已脱敏）
- 涉及的产品（需要时用 `search_products` 核对产品名称和参数）

## 3. 请产品总监评估

告诉用户这一步会消耗企业智能点，然后调用 `ask_director`：

- `director`: `"product"`
- `question`：附上归纳后的问题清单（不要附原始反馈全文），请总监按用户价值、业务价值、实现成本和风险给出优先级（P0～P2）、建议方案和需要进一步验证的问题。

返回 `status: "running"` 时，等 `retry_after_seconds` 秒后用 `get_director_reply` 取回答，不要重复提问。

## 4. 输出需求清单

用表格输出，用户的语言：

| 优先级 | 需求 | 用户问题 | 证据（次数、原话） | 建议方案 | 验收标准 |
| --- | --- | --- | --- | --- | --- |

之后列出：

- **暂不处理**：价值低或证据不足的反馈，以及原因
- **待验证**：需要再找客户确认的问题
- 产品总监对话的 `workbench_url`，方便用户在 MasterPro 继续讨论

规则：区分客户原话、你的归纳和产品总监的建议，不要把推测写成事实。

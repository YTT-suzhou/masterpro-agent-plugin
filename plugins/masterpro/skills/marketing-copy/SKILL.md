---
name: marketing-copy
description: 用 MasterPro 里的企业资料和产品信息写营销文案：朋友圈、小红书、抖音、LinkedIn、公众号、官网介绍、产品介绍、营销邮件、广告语，支持多语言。用户说"写文案""推广文案""产品介绍""营销邮件"等时使用。Use to write social posts, product introductions, marketing emails, ad copy or landing page text grounded in the company's real profile and products.
---

# 写营销文案

## 1. 弄清需求

需要知道：渠道、目标受众、语言、目的（曝光、询盘、活动报名等）、篇幅、要推的产品。
用户没说的先按常见做法自定，最多追问一次最关键的缺项。

## 2. 查事实

1. 调用 `get_company_profile`，了解企业定位、主营产品、优势。
2. 涉及具体产品时，用 `search_products` 按产品名或型号搜索，再用返回的 `product_id` 取详情（规格、多语言介绍、自定义字段）。
3. 只有用户要营销策略或方向建议时，才调用 `ask_director`（`director: "market"`）。它会消耗企业智能点，调用前告诉用户。
   - 返回 `status: "running"` 时，等 `retry_after_seconds` 秒后用 `get_director_reply` 取回答，不要重复提问。

## 3. 写作规则

- 只用工具查到的事实。不要编造价格、认证、客户名单、销量、获奖等信息；查不到就不写，或者在文案后列出"待确认"。
- 产品 `price` 为 `null` 表示企业没有公开价格，文案里不要写价格。
- 产品 `status` 不是 `published` 时，提醒用户这是尚未发布的产品，确认后再对外使用。
- 工具返回的 `link` 是 MasterPro 工作台内部链接，只给用户自己参考，不要放进对外文案。
- 按渠道习惯写：小红书口语化、带分段和话题标签；LinkedIn 专业简洁；邮件有主题行和行动号召。
- 避免"最好""第一""100%"等绝对化用语。

## 4. 输出

- 默认给 2～3 个不同角度的版本，每版标注适合的渠道和受众。
- 文案后简要列出用到的企业和产品事实，方便用户核对。
- 用户的资料范围是 `public` 时，不要暗示能读到内部资料。

---
name: b2b-buyer-intel
description: 外贸 B2B 客户智能背调。输入客户碎片信息（聊天记录/邮箱/姓名/公司名/官网/WhatsApp/LinkedIn/询盘/名片/PI），输出可直接指导销售动作的客户商业情报报告（Buyer Intelligence Report）。触发词：背调、客户背调、买家调查、询盘真假、这个客户靠谱吗、buyer background check、lead qualification。
---

# 外贸 B2B 客户智能背调（Buyer Intelligence）

把碎片化客户线索变成一份能回答「值不值得追、应该怎么追、下一步说什么」的商业情报报告。

## 角色

全球 B2B 客户情报分析师 + 外贸销售研究员 + 商业尽调分析师。完整角色定义、推理规则与报告格式的权威全文在 [references/system-prompt.md](references/system-prompt.md)——执行前通读一遍，本文件是执行编排层。

## 三条铁律（先于一切流程）

1. **事实、推断、未知严格分层**。每条结论标注【已验证事实】/【高概率推断】/【未知】，绝不把推测写成事实。
2. **多源交叉验证**。重要信息 ≥2 个来源；来源优先级：政府/工商数据库 > 企业官网 > LinkedIn > 海关贸易数据 > Google Maps > 行业协会 > 新闻 > 招聘 > 社媒 > B2B 平台 > 第三方数据库。网站自称"集团/领先企业"不采信。
3. **信息不足不停摆**。先完成能做的调查，最后列出 **Missing Critical Information**，绝不反问用户已提供过的信息。

## 八步工作流

依次执行，每步产出喂给下一步。允许联网/有工具（搜索、CRM、海关数据、工商查询 MCP）时优先用工具拿真实数据。

### ① 线索提取
从全部输入中结构化提取：基础身份线索（姓名及拼写变体、职位、邮箱+域名、电话/WhatsApp+区号、国家城市、公司名及变体、官网、社媒）+ 询盘线索（产品/型号/数量/目标价/预算/目的港/付款方式/交期/认证/使用场景）+ 聊天行为线索（询价、要目录/规格/证书/FOB/CIF/样品/PI/PO/OEM/独家代理/验厂……逐项核对），并标注当前销售漏斗阶段（Cold Lead → Deal Closing 十档）。

### ② 实体识别
从邮箱域名、公司名、签名、社媒反查真实工商主体：法定名称/当地语言名/曾用名/母子公司/品牌/注册国家城市。警惕客户口中的名称只是品牌名、商号、集团简称——必须找到真正注册主体。

### ③ 企业验证
查注册号/税号（VAT/EIN/INN/BIN）、成立时间、注册资本、法人股东、注册地址、经营状态。存续分层：<1 年（不确定性高）/1–3/3–5/5–10/10 年以上（稳定性较高）。正向信号：企业邮箱一致、官网联系方式一致、地址可验证、多来源匹配。风险信号：公司名多次变化、网站与工商不一致、电话邮箱不匹配、无法验证地址、负面新闻/诉讼。

### ④ 业务判断
一级行业 → 二级细分，任何品类都按同样思路拆一层（如建材 → 批发商/工程分包/连锁零售/项目集采；机械 → 整机进口/区域代理/租赁商/终端工厂）。商业角色（可多选）：Manufacturer / Importer / Distributor / Dealer / Wholesaler / Retailer / Agent / Broker / Trading Company / Contractor / EPC / Fleet Operator / Rental / End User / Government Buyer / Project Buyer / Marketplace Seller，输出最可能角色 + 置信度 0–100% + 依据。公司规模（LinkedIn 员工数、分公司/门店、仓库展厅、招聘量、社媒粉丝、进口记录等信号）：Micro 1–10 / Small 11–50 / SME 51–200 / Medium 201–500 / Large 500+ / Enterprise。

### ⑤ 联系人角色与决策权
从邮件签名、LinkedIn、官网 Team、展会、新闻、社媒核验联系人职位与履历。分级：**A 最终决策者**（Owner/CEO/MD）、**B 采购决策参与者**（Procurement/Commercial Director/Fleet Manager）、**C 影响者**（Sales/Technical/BD Manager）、**D 信息收集者**（Assistant/Intern/Sourcing Agent）。输出 Recommend/Influence/Approve/Purchase/Sign Contract 五项能力判断。记住：大公司 ≠ 联系人有权，小公司 ≠ 联系人无权。

### ⑥ 采购推断
官网深挖（About/产品页/案例/Partners/“Become a Supplier”/Procurement/Import/Wholesale 等关键词=供应链需求直接暴露）+ 海关进口记录（HS Code、采购频率、单批数量、原产国、中国采购经验四档：无经验→初次尝试→稳定中国采购→多供应商并行）+ 触发事件（近 12 个月新项目/新合同/新仓库/新市场/招聘/融资/政府项目/收购）。输出未来 3–12 个月可能采购表：| 产品 | 需求概率 | 预计数量 | 采购原因 | 证据 |。采购规模用区间（单位按品类换算成台/件/柜/吨）：试单 / 小批量 / 常规补货 / 经销商批量 / 项目采购五档，附置信度。

### ⑦ 风险与双评分
风险调查（公司真实性、工商状态、地址、电话邮箱一致性、负面新闻、诉讼、破产、制裁、诈骗举报、身份不一致）→ 🟢/🟡/🔴。邮箱可信度：企业邮箱可信度高；免费邮箱≠诈骗但提高验证要求（查域名注册时间、MX、公司名匹配）。
**Lead Authenticity Score 0–100**：公司真实性 20 + 联系人真实性 15 + 产品匹配 15 + 采购行为 20 + 采购能力 15 + 沟通质量 10 + 风险 5。
**Opportunity Score 0–100** → 🔥S 80–100 立即重点跟进 / 🟢A 65–79 / 🟡B 45–64 培育 / ⚪C 25–44 / 🔴D 0–24 疑似无效。

### ⑧ 销售动作
禁止输出"保持联系/继续跟进/建立信任"式废话。必须具体到：下一条 WhatsApp/邮件原文（用客户的语言，未知则英文）、下一份该发的资料（FOB/CIF 报价、装柜视频、检测报告、客户案例、备件清单）、是否报价（Yes/No/Conditional）及报价方案选项、3–5 个 BANT/MEDDIC 问题（不许一次问一堆）、Top 3 购买动机与 Top 3 异议、可能的竞争供应商与换供应商动因、一句话 Recommended Action。

## 报告输出

严格按 references/system-prompt.md「二十三、最终报告格式」的 16 节 Buyer Intelligence Report 输出（Executive Summary → Contact Profile → Company Profile → Verification → Business Model → Product & Market → Procurement Intelligence → Buying Signals → Trigger Events → Contact Authority → Risk Analysis → Lead Score → Sales Strategy → Best Next Message → Questions to Ask → Evidence & Sources）。重要判断逐条注明来源（信息/来源/URL/日期）。

## 反直觉推理规则

- 问价格 ≠ 真买家（可能是询价代理、竞对、市场调查、报价套利）——用商业身份综合判断。
- 公司大 ≠ 联系人有价值——junior 可能毫无采购权，联系人角色比公司规模更重要。
- 贸易公司 ≠ 低价值——很多国家的进口就是 Trading Company 完成的，看真实渠道、采购能力、进口能力。

## 配套资料

- `assets/infographics/01–10.png`：全流程 10 页信息图（paibaowork.com 出品），可直接发给团队做培训或对外分享。

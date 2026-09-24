# 外贸 B2B 客户智能背调 Agent（Buyer Intelligence Skill）

> 把碎片化客户线索——聊天记录、邮箱、姓名、公司名、官网、WhatsApp、询盘、名片——变成一份能直接指导销售决策的**客户商业情报报告**。
>
> 回答外贸人最关心的问题：**这个客户值不值得追？应该怎么追？下一步说什么？**

由 [paibaowork.com（派宝外贸智能体）](https://paibaowork.com) 出品并开源。

## 它能回答什么

| 客户是谁 | 公司是否真实 | 采购什么 |
|---|---|---|
| **采购规模多大** | **谁有决策权** | **下一步怎么跟进** |

## 八步工作流

1. **线索提取** —— 从聊天记录、邮箱、网站等多源信息提取关键线索
2. **实体识别** —— 识别公司、联系人、域名、社媒等实体并标准化
3. **企业验证** —— 验证企业真实性、经营状态、规模及基础信息
4. **业务判断** —— 判断行业、产品相关性、市场定位及竞争格局
5. **联系人角色** —— 识别联系人职位、职责范围及在采购链路中的角色（A/B/C/D 决策权分级）
6. **采购推断** —— 推断采购需求、产品规格、预算范围及采购时间
7. **风险评分** —— 识别信用、合规、支付、贸易履约等风险；询盘真实性评分 + 商机价值评分（S/A/B/C/D）
8. **销售动作** —— 输出跟进建议、话术、资料清单及下一步行动计划（BANT/MEDDIC）

完整 10 页流程信息图见 [`assets/infographics/`](assets/infographics/)。

## 使用方式

### 方式一：Claude Code / Claude 技能

```bash
git clone https://github.com/iPythoning/b2b-buyer-intel.git
mkdir -p ~/.claude/skills && ln -s "$(pwd)/b2b-buyer-intel" ~/.claude/skills/b2b-buyer-intel
```

之后在对话里直接说「帮我背调这个客户」并贴上客户信息（聊天记录/邮箱/名片截图都行）。

### 方式二：任意 AI 工具（ChatGPT / DeepSeek / Kimi / 豆包……）

把 [`references/system-prompt.md`](references/system-prompt.md) 全文作为系统提示词或对话开头贴入，再提交客户信息即可。允许联网的模型效果最好。

### 输入示例

```
帮我背调这个客户：
- WhatsApp: +52 1 xx xxxx xxxx
- 邮箱: carlos@xxximport.mx
- 聊天记录: "Hi, do you have stock for model X? Need CIF price to Veracruz, quantity around 2 containers..."
```

### 输出

一份 16 节的 Buyer Intelligence Report：Executive Summary、公司验证、商业模式、联系人决策权、采购情报、风险分析、双评分（真实性 0–100 + 商机价值 S/A/B/C/D）、可直接发送的下一条 WhatsApp 消息、3–5 个关键问题、证据来源清单。

## 核心原则

- **事实、推断、未知严格分层**：所有结论标注【已验证事实】/【高概率推断】/【未知】，绝不把推测写成事实
- **多源交叉验证**：重要信息至少 2 个来源，工商数据库 > 官网 > LinkedIn > 海关数据 > ……
- **拒绝废话建议**：不输出"保持联系、继续跟进"，只输出具体到话术和资料清单的动作

## 适用品类

工作流本身行业无关——机械设备、建材、化工、消费电子、纺织服装、汽车及配件、医疗器械、食品……任何外贸 B2B 品类都适用，把示例中的产品换成你自己的即可。

## 产品互链

本 Skill 的线上产品化形态是 **AI 探客**（[paibaowork.com](https://paibaowork.com) / Console `/leads`）：同类产品买家挖掘、商业角色判定（买家/经销商/同行）、证据分层、决策人分级、有效性标记与理赔，均以本 Skill 的八步工作流与三条铁律为准绳——产品能力只在其上增强，不弱于它。线上挖到线索后，可回到本 Skill 做八步深背调。

## 关于派宝外贸智能体

- 🌐 官网：https://paibaowork.com
- 💬 WhatsApp：https://wa.me/8615810959875
- 📮 合作咨询：https://paibaowork.com/contact/

## License

[MIT](LICENSE) — 提示词与信息图可自由使用、修改、分发，保留出处署名即可。

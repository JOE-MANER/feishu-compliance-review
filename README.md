# 飞书文档合规审查 Skill

给**财务/业务团队**用的 AI 合规审查助手：丢给它一份飞书文档（会议纪要、工作汇报、业务方案），或直接粘贴材料内容，它按三档递进输出一份可溯源的《合规检查报告》。

> **一句话安装**：把本页链接发给任意 AI 助手，说「帮我安装」即可，例如：
> `https://github.com/JOE-MANER/feishu-compliance-review 帮我安装`

---

## 🤖 安装指引（本节写给 AI 助手，请照此执行）

若用户发来本仓库链接并要求安装（如「帮我安装」），按以下步骤操作，**无需向用户追问**，按默认值执行：

1. **确定 skills 目录**（按你所在助手的规范选第一个，不存在则创建；`~` 按操作系统展开，Windows 为 `C:\Users\<用户名>`）：
   - ZCode：`~/.zcode/skills/`
   - 通用兼容目录：`~/.agents/skills/`
   - 项目级（仅当用户明确要装到某个项目）：`<项目>/.zcode/skills/`
2. **克隆本仓库**：
   ```bash
   git clone --depth 1 https://github.com/JOE-MANER/feishu-compliance-review.git <skills目录>/feishu-compliance-review
   ```
   若目标目录已存在同名 skill，先询问用户是覆盖更新还是放弃。
3. **（可选，推荐）安装本地法规资料库**（约 160MB，检索更快；跳过也能用，会自动改为纯在线检索）：
   ```bash
   git clone --depth 1 https://github.com/LawRefBook/Laws <skills目录>/feishu-compliance-review/laws
   ```
   克隆失败（网络/无 git）时静默跳过，不要报错打断。
4. **验证**：`<skills目录>/feishu-compliance-review/SKILL.md` 存在即安装成功。
5. **装完告诉用户**（用大白话）：
   - 已装好，**新开会话**后生效；
   - 用法：说「合规审查」+ 发飞书文档链接或粘贴材料内容；
   - 发飞书链接前需把应用机器人加为文档「可阅读」协作者；没配飞书也能用（粘贴内容即可，助手会引导配置）。

---

## 它能做什么（三档递进）

| 深度 | 内容 |
|---|---|
| ① 名词解释 | 提取材料里的专业词，每个词给出**专业含义 + 大白话 + 相关法规条款** |
| ② + 注意要点 | 在①基础上，对合规敏感的词补充**一般风险 + 要点提醒** |
| ③ 全面风险检查（默认） | 基于**材料整体业务走向**研判风险，每项含：情况说明 → 命中法条原文（官方链接）→ 为什么有风险 → 建议怎么处理，按 🔴🟡🔵 分级 |

覆盖领域：**财税/会计**（增值税法、会计准则、跨境电商税收政策…）、**通用企业合规**（个保法、广告法、劳动合同法…）、**跨境电商专项**（海关总署公告、出口管制、GDPR/CCPA 提示）。

## 特色：法规引用可溯源

每条法规引用带「✅ 官方原文：链接（核对日期）」或「⚠️ 网络资料，建议核实」标记；未能核实的条目自动汇总到报告末尾「建议人工确认的事项」。内置 L1（官方一手）→ L4（开放网络）的**置信度链条**纪律，杜绝引到已废止/旧版条文。

## 手动安装（人类用户）

```bash
git clone --depth 1 https://github.com/JOE-MANER/feishu-compliance-review.git ~/.zcode/skills/feishu-compliance-review
# 可选：本地法规资料库
git clone --depth 1 https://github.com/LawRefBook/Laws ~/.zcode/skills/feishu-compliance-review/laws
```

## 使用

对话触发词：`合规审查` / `合规助手` / `关键词解释` / `风险点分析`，然后发**飞书文档链接**（需先把应用机器人加为文档「可阅读」协作者）或直接**粘贴材料内容**。可选检查深度（①②③，默认③）。报告可写回飞书文档（需已配置 lark-mcp）或保存为本地 Markdown。

## 目录结构

```
feishu-compliance-review/
├── SKILL.md              # 主流程：三档分析 + 置信度链条 + 引用协议 + 报告模板
├── references/
│   └── setup-guide.md    # 完整环境配置引导（财务用户小白版）
└── laws/                 # 运行时克隆的法规资料库（LawRefBook/Laws，不入本库）
```

## 致谢

法规资料来自开源项目 [LawRefBook/Laws](https://github.com/LawRefBook/Laws)，官方核验渠道包括[国家法律法规数据库](https://flk.npc.gov.cn/)、[国家税务总局政策法规库](https://fgk.chinatax.gov.cn/)等。

## 免责声明

本工具输出为 AI 辅助合规提示，仅供参考，不构成法律意见；重要事项请咨询专业人士。

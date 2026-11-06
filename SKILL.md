---
name: skill-go-to-market
description: "Package a methodology into a sellable SKILL.md, push to GitHub, list on marketplaces, and set up payout — the go-to-market playbook for selling AI agent skills."
version: 1.1.0
author: AlqEdge
license: proprietary
metadata:
  hermes:
    tags: [skill, marketplace, go-to-market, packaging, payout, publish]
    related_skills: [opportunity-validation]
---

# Skill 出海工具箱：把方法论做成可售 skill 并卖出去

> 把任何一套方法论/流程打包成 AI agent skill（SKILL.md），推上 GitHub 引流，上架内容市场（Agensi/PromptBase 等）卖钱，并打通收款。本 skill 是**踩坑过的实战流程**——每步标注了真实会遇到的坑，照做即可，不要重复踩。

## When to Use

- 你有一套方法论/工作流，想做成 AI agent skill 卖钱
- 已经写好 SKILL.md，不知道下一步怎么上架、怎么收款
- 想从 0 走一遍「打包 → 引流 → 上架 → 收款」的完整链路
- 在多个 skill 市场铺货，需要一份统一的自查 + 定价 + 上架清单

## 全流程总览（5 步）

```
打包 → 引流（GitHub）→ 上架（市场）→ 收款 → 验证 + 迭代
 ①      ②             ③         ④       ⑤
```

---

## ① 打包：把方法论固化成 SKILL.md

### 目录结构（Claude Code 标准）

```
my-skill/
├── SKILL.md          # 主文件（必须！frontmatter 必填 name + description）
├── scripts/          # 可执行脚本（可选，脚本必须无密钥）
└── references/       # 数据/基线资料（可选，付费版核心卖点常在这）
```

### frontmatter 铁律
- `name`：小写 + 连字符（如 `skill-go-to-market`）
- `description`：1-1024 字符，第一句 57 字符内可独立触发
- ⚠️ **zip 必须含名为 `SKILL.md` 的文件**（不是 SKILL-selfcontained.md）——打包前把自包含版重命名

### 三种打包形态
| 形态 | 说明 | 用途 |
|---|---|---|
| 单文件自包含版 | 方法论+数据全塞进一个 SKILL.md | 上传到市场最省事（一次传完） |
| 多文件版 | SKILL.md + scripts/ + references/ | 功能完整，zip 打包上传 |
| 目录版 | `.claude/skills/<name>/SKILL.md` | GitHub 仓库标准结构 |

### SKILL.md 写作原则（借鉴社区最佳实践）
- **imperative 命令式语气**：写「Read X. Run Y.」，不写「You should…」（软绵绵的命令 agent 不会照做）
- **dense 高密度**：不要礼貌废话、不要装饰性引用块；≤500 行 / ~5k tokens 以内
- **渐进式披露**：SKILL.md 只留核心流程 + 指针，细节下沉到 references/（一层深引用，不链式引用）
- **description 三要素**：1-1024 字符、第三人称、同时含「做什么 what + 什么时候用 when」+ ≥3 个触发短语
- **name 规范**：小写 + 数字 + 单连字符，1-64 字符，不用保留词（anthropic/claude）
- **路径用正斜杠** `/`，不用反斜杠 `\`
- **不放时效性内容**（或隔离到「Old patterns」节）——AI 技能 3-6 个月就过时
- 具体例子代替抽象占位（"审计底稿结构化" 而非 "Excel AI"）

---

## ② 引流：推上 GitHub（免费版）

### 策略：免费 Lite 引流 + 付费 Pro 收钱
- 公开仓库放**免费 Lite 版**（方法论文档，不含付费数据/脚本）→ 白送引流位
- 私有仓库（或市场上传）放**付费 Pro 版**（含密度基线/脚本/更新承诺）
- README 引导到付费购买链接（README 是 Documentation Link，买家点开就是白送引流位）

### GitHub 上架要点
- 仓库结构：`SKILL.md` 放 `.claude/skills/<name>/SKILL.md`，根目录留 README/LICENSE
- 若市场支持「Import from GitHub」：SKILL URL 必须指到技能文件夹（`/tree/main/.claude/skills/<name>`），不是仓库根
- 私有仓库连接部分市场需升级套餐 → 绕开方法：直接「Upload/Paste SKILL.md 文件」上架

---

## ③ 上架：选市场 + 逐字段填写

### 市场选型（内容市场）
| 平台 | 分成 | 大陆收款 | 判断 |
|---|---|---|---|
| Agensi | 70% | USDC(Solana) 需实测 | 内容市场首选，Creator 教程最全 |
| SkillExchange | 85% | Stripe Connect（大陆不通） | 分成最高但收款是坑，别先花时间 |
| MCP Market | 80% | Stripe（大陆不通） | 卖家侧无 API，弃用 |
| PromptBase | 80-100% | USDC 可用（需实测） | 与 Agensi 同通道，可铺 |

### 上架前自查（Agensi 8 点安全扫描）
- [ ] 无危险命令（rm -rf 等破坏性命令）
- [ ] 无硬编码密钥/API key
- [ ] 无 prompt injection
- [ ] 无数据外泄（脚本只输出本地 markdown）
- [ ] 无混淆代码
- [ ] 外部抓取在描述里写明用途（如「no API key, uses public search」）
- [ ] 无凭据访问
- [ ] 无提权

### 权限最小化
- 只申请真实用到的工具
- Environment Variables / Browser / Write Files **不开是加分项**（说明无密钥、不碰用户数据）
- **Read Files 必须开**——如果卖点在 references/（数据基线），不开等于废掉核心功能

### 逐字段填写要点
- **Notes**：英文逐条解释每个权限为什么需要，带「No credentials / no user data accessed」
- **Known Limitations**：别照抄系统自动推断，按真实约束扩写成 5 条左右（时效性/数据盲区/边界），提前声明真实限制 = 挡差评 + 审核加分
- **FAQ**：手动填 5 条（干什么/和直接问 ChatGPT 有何不同/要不要联网和密钥/数据准不准/一次买断还是订阅），退款条款与收款店铺一致
- **Documentation Link**：填公开 GitHub 仓库 README（不是私有仓库——买家点开 404 扣信任分；不是落地页——语义不匹配）
- **The result（输出样例）**：700+ 字符，开头 3 秒给结论（决策标签+密度+置信度），表格放真实数据，Next Steps 给具体动作
- **The request（提问示例）**：中英双语 + 尽量详细，每条 2-3 句带真实语气，覆盖不同触发场景

---

### 多市场铺货（借鉴社区实践，但收款是我们的差异化）
- 同一个 skill 可以在多个市场 + GitHub 铺货（有开源工具支持一键发布到 GitHub/ClawHub/npm，如 `skill-multi-publisher`）
- 但**纯发布工具不解决两件事**：①收款（大陆开发者要用 USDC/MoR，见第④步）②内容市场（Agensi/PromptBase 要手动上架，无卖家 API）
- 所以铺货策略 = 免费版铺 GitHub（引流）+ 付费版铺内容市场（Agensi/PromptBase）+ 独立站承接信任
- 多市场铺货注意：**每个市场购买链接指向同一个收银台**，别让买家看到多个购买入口

## ④ 收款：选对通道（大陆开发者特供）

### 关键判断
- **Stripe Connect 是海外 skill 市场默认收款，其支持清单不含中国大陆**——大陆个人在这些市场几乎全卡在收款
- 唯一希望 = 平台的**加密（USDC）提现通道**（如 Agensi 的 USDC via Zoneless），需注册实测

### 两条路线
| 路线 | 平台 | 大陆提现 | 说明 |
|---|---|---|---|
| **市场分发** | Agensi（USDC）+ PromptBase（USDC） | 加密通道实测 | 做分发，USDC → 交易所 C2C 换法币 |
| **自建收银** | Waffo Pancake / Anyway / Creem（MoR） | ✅ 支付宝直提 | 配独立站自售，MoR 平台当法定卖家处理税务 |

### 出金铁律（USDC 路线）
1. 先 1 USDC 小额测试，再走大额
2. 网络选对（Solana SPL），选错丢币
3. 保留 TXID / 订单截图
4. 交易所 C2C 卖币选 99%+ 好评商家，防冻卡

---

## ⑤ 验证 + 迭代

### 上线验证（不轻信汇报）
```bash
curl -s -o /dev/null -w "%{http_code}\n" -L <你的购买/产品URL>   # 须 200
```
- 抽查产品描述/价格/购买按钮是否真实上线（不是缓存旧版）
- 新平台购买链接必须指向**同一个收银台**，别让买家看到多个购买入口

### 迭代节奏
- 先手动跑通第一单交付（后台见订单 → 发文件/授权），再上 Webhook 自动发货
- 每版升级前 **dogfooding**：用团队自己的任务手动 run 一遍验证方法论可用再上架（能抓出误判）
- 持续看竞品价格带（同品类低价竞品出现 = 需求被验证 + 价格在下探，差异化要持续强调）

### 发布前 A/B/C 分级清单（借鉴社区最佳实践）
> 每次发布前逐项过一遍。A = 每个 skill 的最低标准；B = 对外分享/上架的 skill；C = 高风险的 skill。

**A. 最低标准（每个 skill）**
- [ ] `name` 与文件夹名完全一致（大小写敏感）
- [ ] `name` 小写 + 数字 + 单连字符
- [ ] `description` 1-1024 字符、第三人称、含 ≥3 个触发短语
- [ ] frontmatter 从第 1 行 `---` 开始
- [ ] 正文命令式语气（Read/Run），不是 You should…
- [ ] 高密度，≤500 行 / ~5k tokens
- [ ] references 一层深引用（不链式）
- [ ] 所有 `[text](path)` 链接能解析
- [ ] 无硬编码密钥 / 无危险命令

**B. 对外发布（上架市场）**
- [ ] README.md 存在（含安装说明 + 购买链接）
- [ ] LICENSE 存在
- [ ] zip 内含 `SKILL.md` 根文件（市场硬性要求）
- [ ] 脚本 `chmod +x`、有错误处理、常量有注释
- [ ] 通过 `skill-validator check --strict` 或 `npx skills-ref validate`
- [ ] 中文版 / 双语文案备好

**C. 高风险 skill（执行命令/碰文件/网络）**
- [ ] 8 点安全扫描全过（危险命令/密钥/注入/外泄/混淆/凭据/提权）
- [ ] 外部抓取在描述里写明用途
- [ ] Known Limitations 提前声明真实限制

### 校验工具链（可选）
| 工具 | 语言 | 安装 | 用途 |
|---|---|---|---|
| `skill-validator` | Go | `brew tap agent-ecosystem/tap && brew install skill-validator` | 最全：spec + 链接解析 + token 数 + LLM 打分 + 13 平台 pre-commit hooks |
| `skills-ref` | Node | `npx skills-ref validate ...` | 轻量 spec 合规检查 |
| `skillcheck` | Python | `pip install skillcheck` | 跨 agent 问题检测 |
> 先用工具跑自动检查，再人工过一遍（工具抓不到 voodoo 常量/废话/时效性内容）。

---

## Pitfalls（全踩过的坑）

- ❌ 把「没有直接竞品」当蓝海——可能是没市场，必须同时有付费证据
- ❌ 不查竞品就上架（机会评估类任务的默认动作就是查）
- ❌ 弃用平台后残留旧购买链接——README/落地页/各市场描述全搜一遍同步到当前收银台
- ❌ 把免费版当「白送」——免费版是获客成本（免费→付费转化约 4%）
- ❌ 一个 skill 打天下——组合打法（1 免费 + 3-5 中价 + 1-2 高价）才能放大
- ❌ 卖通用 skill——只做「窄、痛、难复制」的（框架特定/合规审查/垂直职业）
- ❌ 上架 ≠ 有人买——市场只给货架和支付，流量靠自己带（Reddit/SEO/社区）

## IS NOT

本 skill 不做：客户访谈/真实用户验证替代、投资级尽调、财务模型构建。它做的是：快速、有依据地把方法论变成可售 skill 并走完上架收款链路。真实付费意愿最终靠落地页/访谈/预售确认。

## 参考

- `references/marketplace-listing-fields.md` —— Skill 市场上架表单逐字段填写指南（Agensi/PromptBase 通用）
- `references/platforms-china-payout.md` —— 大陆个人收款通道对比
- `references/waffo-webhook-fields.md` —— 自动发货 Webhook 字段与配置
- 实战案例：opportunity-validation（从方法论到 $19 付费 skill，Agensi 在售）

# Skill Go-To-Market PRO — China-Safe Playbook for Selling AI Agent Skills (with Real Payout Data)

> A decision-grade, battle-tested playbook for turning a methodology into a sellable SKILL.md and getting paid — built from an actually-shipped product (free Lite on GitHub + $19 Pro live on Agensi). This is NOT generic advice: the market matrix, payout routes, KYB pain points, and webhook field tables below are measured from real registrations and real orders.

## 0. Why this playbook can't be guessed (read this first)

Everything below is learned by shipping, not by thinking:

- **Real marketplace payout reality (measured)**: Stripe Connect — the default payout for overseas skill marketplaces — does NOT support mainland China. That single fact blocks ~90% of Chinese devs from ever getting paid. The only working routes are crypto (USDC) withdrawals and MoR platforms.
- **Real MoR fee tables** (measured at registration): Waffo Pancake 3.9% + $0.5 (Alipay direct), Creem 3.9% + $0.4 (Alipay ≤5万 CNY per transfer), Anyway (Alipay + mainland bank, min $50). No mainstream guide lists these.
- **Real conversion benchmark**: free Lite → paid Pro converts at roughly 4% — treat your free version as a customer-acquisition cost, not a giveaway.
- **Real KYB review pain points**: reviewers click your links and verify. Missing revocable license + termination clause in TOS = guaranteed rejection loop.
- **Real pitfalls**: leftover dead buy links after switching payment channels; "no direct competitor" being mistaken for blue ocean; marketplace listing ≠ traffic (you bring your own).

## 1. The 5-Step Pipeline (compressed)

```
Package → Traffic (GitHub) → List (marketplace) → Payout → Verify & Iterate
```

### Step 1 — Package
- Structure: `SKILL.md` (frontmatter name + description) + optional `references/` (data baselines — often the paid value) + optional `scripts/` (no hardcoded keys)
- Iron rules: name lowercase + hyphens; description 1-1024 chars with ≥3 trigger phrases; imperative voice ("Read X. Run Y."); dense ≤500 lines; no time-sensitive claims (or isolate in an "Old patterns" section)
- ⚠️ The zip MUST contain a file literally named `SKILL.md` (not SKILL-selfcontained.md)

### Step 2 — Traffic (GitHub free Lite)
- Public repo = free Lite (methodology only) → README carries the paid buy link
- Repo layout: SKILL.md at `.claude/skills/<name>/SKILL.md`; README/LICENSE at root
- "Import from GitHub" marketplaces need the URL pointing to the skill folder, not repo root

### Step 3 — List (marketplace matrix, measured Oct 2026)
| Platform | Split | China payout | Verdict |
|---|---|---|---|
| Agensi | 70% | USDC (Solana via Zoneless) ✓ tested | Primary — list first |
| PromptBase | 80-100% | USDC (Solana via Zoneless) ✓ tested | Same channel, add |
| SkillExchange | 85% | Stripe Connect ✗ mainland | Highest split but payout trap — skip |
| MCP Market | 80% | Stripe ✗ mainland | Deprecated (no seller API) |

- Permission minimization: Read Files ON (if references/ is your value), Env Var / Browser / Write OFF (a selling point)
- Field notes: Notes in English with "No credentials / no user data accessed"; Known Limitations = ~5 real constraints (freshness/blind spots), not the auto-inferred ones; FAQ filled manually with refund terms matching your store; Documentation Link = PUBLIC repo README

### Step 4 — Payout (two routes, both tested)
| Route | Platforms | Mainland withdrawal |
|---|---|---|
| Marketplace distribution | Agensi + PromptBase (USDC/Solana) | USDC → OKX C2C → Alipay (test 1 USDC first; 99%+ trusted merchants to avoid frozen cards) |
| Self-hosted cashier (MoR) | Waffo Pancake / Anyway / Creem | ✅ Alipay direct (MoR acts as legal seller for tax) |

- USDC iron rules: test with 1 USDC first; network = Solana SPL (wrong network = lost coins); keep TXID/screenshots

### Step 5 — Verify & Iterate
- `curl -s -o /dev/null -w "%{http_code}" -L <buy-url>` must be 200; spot-check price/description live
- Manual first delivery (see order → send file) before webhook automation
- Dogfood every upgrade before shipping (catches misjudgments — e.g. "Chinese vacuum" that was actually just English SaaS with Chinese localization)
- Watch the price band: low-cost clones appearing = demand confirmed + price dropping → differentiation must get stronger

## 2. Pre-Publish A/B/C Checklist

**A. Minimum (every skill)**: name matches folder (case-sensitive) · name lowercase+hyphens · description 1-1024 chars with ≥3 triggers · frontmatter starts `---` at line 1 · imperative voice · ≤500 lines / ~5k tokens · references one-level deep · all links resolve · no hardcoded keys / dangerous commands

**B. External publish**: README.md (install + buy link) · LICENSE · zip contains root `SKILL.md` · scripts chmod +x with error handling · passes `skill-validator check --strict` or `npx skills-ref validate` · Chinese/bilingual copy ready

**C. High-risk (run commands / touch files / network)**: 8-point security scan all green (dangerous commands / hardcoded keys / prompt injection / data exfiltration / obfuscation / credential access / privilege escalation) · external fetching declared · Known Limitations declared

## 3. KYB / Platform-Review Pain Points (measured)

- What reviewers verify: GitHub repo, independent site, real product, real price — they click your links. Never fabricate credentials.
- TOS must include: revocable license (no resale/sharing), Term & Termination with consequences (immediate termination + delete copies + no refund + legal recourse), IP clause (license only, no ownership transfer)
- One-time pricing: describe honestly as "one-time license" + free Lite/paid Pro tier; don't invent a subscription to match platform examples
- Submit in English (international review teams read English), keep Chinese version for your own records

## 4. Webhook Auto-Delivery Field Table (real, from Waffo 2026-10)

- Order events: `order.completed` (one-time pay success); refund: `refund.succeeded/failed`
- Fields: payment = `chargedAmount` (actual received) + `listPrice` (list price); refund = `refundedAmount` + `originalPayment`; subscription = `planPrice`
- ⚠️ Legacy 6-field (amount/total/subtotal/taxAmount/taxRate/taxName) is deprecated — read the new named fields only
- Verify signature (Raw format carries `X-Waffo-Signature`, RSA-SHA256) — no verification = anyone can forge payment notices
- Test env (TEST key) / prod env (LIVE key) fully isolated; every event has `mode`; test events must never trigger real delivery
- Delivery options: A) email the file on order.completed (e.g. Resend free tier); B) one-time signed download link from private storage

## 5. Pitfalls (every one we hit)

- ❌ "No direct competitor" as blue ocean — may mean no market; require payment evidence too
- ❌ Listing without a competitor check (for opportunity-evaluation skills, checking IS the job)
- ❌ Dead buy links after switching channels — grep README / landing page / every marketplace description, sync to the current cashier
- ❌ Free version treated as giveaway — it's acquisition cost (~4% free→paid)
- ❌ One skill to rule them all — portfolio play (1 free + 3-5 mid + 1-2 high price) scales better
- ❌ Selling generic skills — build "narrow, painful, hard-to-copy" only
- ❌ Listing ≠ sales — marketplaces give shelf + payment; traffic is on you (Reddit / SEO / community)

## 6. Reusable Templates (copy-paste ready)

### 6a. Marketplace decline dispute letter (works on PromptBase/Agensi)
> Dear Review Team,
> I'd like to dispute the decline of "<skill name>."
> I believe it was declined because it reads like general advice at a glance — but the actual file is a battle-tested SKILL.md methodology with content that is NOT guessable: [list 3-5 specific assets: real payout matrix, measured fee tables, KYB pain points, webhook field tables, live-product proof].
> The value is accumulated operational knowledge, not a single clever prompt.
> Could you please re-review with the SKILL.md content in mind?
> Thank you.

### 6b. First-sale manual delivery SOP
1. See order in dashboard (verify payment, check amount vs list price)
2. Send the SKILL.md file / grant private-repo access to the buyer email
3. Log the delivery (order ID, buyer, date)
4. Then automate: test webhook env → prod

### 6c. Landing-page buy-button pattern
- Each product = one `.product` block with id anchor; EN selling points + bilingual title/price + Waffo buy button; FAQ bilingual; SEO: title/description/OG/canonical/JSON-LD Store schema with per-product offers

## 中文版（Chinese version）

技能出海工具箱 PRO · 把方法论变成能收钱的 AI skill（含真实收款数据）：
- 实测市场分成表（Agensi 70% / PromptBase 80-100% / SkillExchange 85% 大陆不通）
- 大陆收款两条路线实测：市场 USDC(Solana) + MoR 收银台（Waffo 3.9%+$0.5 / Creem 3.9%+$0.4 / Anyway 支付宝直提）
- Stripe Connect 不支持大陆个人——出海卖 skill 第一大暗坑
- KYB 审核卡点 + TOS 必备条款（可撤销授权 + 违约终止）
- Webhook 自动发货字段表（真实字段：chargedAmount/listPrice）
- A/B/C 分级发布清单 + 8 点安全扫描 + 7 条全踩过的坑
- 申诉信模板（被市场拒了怎么申诉）
- 实战证明：opportunity-validation（免费 Lite GitHub + $19 Pro Agensi 在售）

适用：有一整套方法论、想把 AI 能力变现的个人开发者与一人公司（尤其大陆）。

# Reddit 帖 ×2（self-post，正文零外链）

> 适用 subreddit：`r/industrialautomation`（首选）`r/AskElectricians` `r/plc` `r/Engineering`（规则严，慎）`r/manufacturing`
> 发帖前必读该版块规则；新账号前 2 周先评论 10+ 条再做主帖。
> **正文不放任何链接**，外链在评论区第一条（两套话术见下文）。

---

## 帖 A｜提问型（最稳，不易被判广告）

**Title（任选其一）**
- What's your actual rule of thumb for sizing control cabinet cooling, and where do yours usually come out?
- Panel builders: what heat load methods do you use when a customer won't give you the drive list?
- Every commission I go to has an undersized cabinet AC somewhere. How do you all catch it at RFQ stage?

**Body（复制）**

Not a troll post — I commission panel cooling for a living and I keep seeing the same sizing gap between what the RFQ says and what the cabinet actually does in July. Curious how other people handle it.

The calculation I end up doing most often (metric, but easy to convert):

Q_total = 1.1 × (Q_i + 5.5 × A × ΔT)

- Q_i = heat dissipated by components inside the cabinet, W
- A = cabinet surface area, m²
- ΔT = ambient − target internal temperature

Two stories from the field that convinced me the formula matters less than the inputs:

1. A customer sized from the main isolator's full-load current. The panel came out ~20× over-cooled. Nobody noticed for a year, then the compressor started short-cycling on a non-optimized control curve and they had a warranty conversation instead of a cooling conversation.

2. A cabinet in a foundry, 38 °C ambient, target 26 °C. The envelope load alone (5.5 × 39.5 m² × 12 °C) was ~2.6 kW before anyone switched anything on. The component load was smaller than the box. That's the part that surprises people.

What I want to know:

- Do you get the component heat load from the drive list, or do you estimate from total power?
- How much margin do you actually add, and does it change for outdoor cabinets?
- Has anyone here had luck getting accurate dissipation figures out of drive vendors? Half the datasheets I get quote input power, not losses, which makes the arithmetic guesswork.
- What's your experience with control cabinets in 50 °C+ ambient — is a cooled cabinet realistic there or do people switch to something else entirely?

Disclosure: I work in this industry, so I'm not asking purely out of curiosity. Happy to share the worked calculation I use, but I'd rather hear how other shops do it first.

**评论区第一条（放链接用）**

Two questions asked, two answers that might help the next person:
- worked sizing example in W and BTU/hr: [how to size a cabinet air conditioner](https://www.zjhcc.com/en/blog/cabinet-ac-cooling-capacity-sizing.html)
- the sizing calculator I use: [zjhcc.com/en/calculator.html](https://www.zjhcc.com/en/calculator.html)

If the mods would rather I not link at all, say the word and I'll strip it.

---

## 帖 B｜干货型（要求版块允许技术分享帖）

**Title**
- The three ways cabinet AC sizing goes wrong (with the actual heat load formula, and a worked example that surprised me)

**Body（复制）**

Cabinet cooling gets specified as a refrigeration problem. It is mostly a heat-balance bookkeeping problem, and the bookkeeping is where the money goes.

**The formula**

Q_total = 1.1 × (Q_i + 5.5 × A × ΔT)

Q_i = component heat load (W)
A = cabinet surface area (m²)
ΔT = ambient − target internal temp (°C)

In imperial terms people usually work in BTU/hr (W × 3.412).

**Mistake 1 — sizing from nameplate current**

Multiplying full-load amps by voltage treats the isolator, the terminal block and the PLC supply as heat sources. They mostly aren't. Correct approach is to add up dissipation of the components that actually turn heat into heat: drives (input power × ~4 %), soft starters, power supplies ((1 − efficiency) × output), transformers, braking resistors on a duty cycle.

Same 800 A panel: FLA method → ~1.3 M BTU/hr. Component method → ~50 k BTU/hr. Twenty times apart on the same cabinet.

**Mistake 2 — ignoring the envelope**

5.5 × A × ΔT is not decoration. A 2.2 × 0.8 × 1.2 m cabinet in a 38 °C hall targeting 26 °C has ~39.5 m² of surface and ~2.6 kW of heat gain through the walls alone. For a small PLC cabinet that is frequently larger than the components.

**Mistake 3 — no site adjustment**

| Condition | Adjustment |
|---|---|
| Direct sun on the cabinet | +10–30 % |
| Ambient > 40 °C | derate unit 10–20 % |
| Altitude > 1,000 m | derate ~3 % / 100 m |
| Cabinet sealed, no circulation | add margin, map the temperature |

**Worked example**

Cabinet 39.5 m², ambient 38 °C, target 26 °C, component load 2,960 W (two big drives).

Q_env = 5.5 × 39.5 × 12 = 2,607 W
Q_total = 1.1 × (2,960 + 2,607) = 6,124 W → two 3,200 W units.

**The symptom to look for**

An undersized unit doesn't fail loudly. It runs at 100 % duty all summer. Capacity of a compressor system is worst exactly when the duty is 100 %, which is why the cabinet gets hot in the worst week of the year and the drive trips on its own thermal cutoff before the AC ever looks wrong.

If your installed unit logged 100 % duty last August, size up. Cycling capacity is cheaper than the downtime.

Disclosure: I work with enclosure cooling units, so I have skin in this. The formula above is standard practice and not proprietary — use it, check it against your own numbers, tell me where it breaks.

**评论区第一条（放链接用）**

Full worked version, both metric and imperial, plus the derating tables I referenced: [zjhcc.com/en/blog/cabinet-ac-cooling-capacity-sizing.html](https://www.zjhcc.com/en/blog/cabinet-ac-cooling-capacity-sizing.html)

Mods, tell me if you'd prefer this without the link and I'll leave it up.

---

## 版块选择与风险提示

| Subreddit | 建议 | 风险 |
|---|---|---|
| r/industrialautomation | 帖 A 首发 | 中等：允许技术讨论，反广告强 |
| r/AskElectricians | 帖 A 备选 | 中：禁Self-promo，正文零链即可 |
| r/plc | 帖 A 备选 | 高：对厂商身份敏感，建议不署名行业 |
| r/Engineering | 帖 B | 高：要求 flair，删帖快，慎 |
| r/manufacturing | 帖 B 备选 | 中 |

**通用纪律**
- 标题不写 brand、不写 "we"，不写 "best"。
- 正文不出现任何 competitor 品牌名（Rittal / Schroff / APC / Vertiv 等一律不提）。
- 第一句必须直接回答问题或陈述事实，不写 "In today's modern industrial landscape"。
- 发后 90 分钟内在线回评，回复速度直接影响排名。
- 若被删：不申诉、不重发同版块，换版块改标题重发（隔 3 天）。

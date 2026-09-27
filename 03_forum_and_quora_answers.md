# 论坛回帖 ×3 + Quora 答案 ×2

> 目标：把已有真实提问回掉。回帖前先在目标站搜一次原问题（关键词用下面的 "Search phrase"）。
> **一律首句直接答问，末句可带 1 条链接，正文不提任何竞品名。**
> 措辞与 LinkedIn/Reddit 不重复（否则判定搬运）。

---

## 回帖 1｜How to size a cabinet air conditioner (BTU / heat load)

**适用站**：Engineering.com 论坛、Control.com、欧盟国家机械论坛（DE/FR/ES 亦可英 posting）、Reddit 帖 A 下
**Search phrase**：`sizing cabinet air conditioner BTU heat load enclosure`

**回帖（复制）**

Two things before you look at BTU numbers:

**1. The enclosure contributes heat, not just your components.**

Q_envelope = 5.5 × A × ΔT

A = cabinet surface area in m², ΔT = ambient − target internal temperature in °C.

Worked example that usually opens eyes: a 2.2 × 0.8 × 1.2 m cabinet (≈39.5 m²), ambient 38 °C, target 26 °C → Q_envelope ≈ 2,600 W ≈ 8,900 BTU/hr, *before any component is powered.*

**2. Don't size from full-load current.**

If you multiply main isolator amps by voltage you are sizing for the copper, not for the heat. A panel with an 800 A @ 480 V main looks like 384,000 W. Add up actual dissipation instead — drives ≈ input power × 4 %, power supplies ≈ output × (1 − efficiency), transformers and braking resistors separately, everything on its duty cycle.

Same panel, component method → ~15,000 W ≈ 51,000 BTU/hr. That's a ~20× difference, and the over-cooled version is the one you'll be servicing.

**Formula I use:**

Q_total = 1.1 × (Q_components + Q_envelope)

Then adjust for site: direct sun +10–30 %, ambient above 40 °C derate the unit 10–20 %, above 1,000 m add ~3 % per 100 m.

Why sizing short is worse than sizing long: the unit runs at 100 % duty all summer, and compressor capacity is at its worst at 100 % duty. The cabinet gets hot exactly in the worst week, and the drive trips on its own thermal cutoff long before the AC looks like the problem.

Derating and the full worked version are here if useful: https://www.zjhcc.com/en/blog/cabinet-ac-cooling-capacity-sizing.html

---

## 回帖 2｜PLC cabinet keeps overheating / tripping / alarms

**适用站**：r/plc、r/AskElectricians、Control.com、EEVblog、任何电气论坛
**Search phrase**：`PLC cabinet overheating alarms temperature trip cooling unit`

**回帖（复制）**

Before you buy anything, spend 40 minutes on two measurements. Most "the AC is too small" cases are airflow cases.

**1. Map the temperature.** One probe at the bottom, one at the top of the cabinet, one at the hottest component. If spread is >10 °C, air is short-circuiting — cold air leaving the unit and being sucked straight back into the intake, never reaching the far corner. Common causes: unit mounted on the door, baffles missing, components packed against the intake side, cable duct blocking the return path.

**2. Log the duty cycle.** If the unit ran 100 % of the time last summer it is undersized, full stop. If it cycled fine and the cabinet was still hot, you have an input problem (heat load, ambient, or envelope), not a capacity problem.

**If it is genuinely undersized:** add capacity, but add it as spare cycling headroom rather than a bigger load. A 6,000 W unit that runs flat out is worse than two 3,000 W units that alternate.

**Also check the cheap stuff first:**
- Filter clogged / condenser coil dusty — this is the most common "capacity loss" in sheltered indoor cabinets
- Setpoint vs actual: setpoint 30 °C with a 40 °C-rated drive is not protection, it's a suggestion
- Ambient rating: indoor units rated to 45 °C are a different machine from an outdoor-wide-temperature unit in a 50 °C climate

One caution that gets missed: a filtered fan pushes positive pressure into the cabinet, and it will find the tiniest seal gap and push dust straight onto the boards. In a dirty environment the fan is usually the thing causing the contamination failure, not solving the heat one.

---

## 回帖 3｜Fan vs heat pipe vs compressor cabinet cooling — which to pick

**适用站**：r/industrialautomation、Engineering.com、任何 HVAC/控制论坛
**Search phrase**：`cabinet cooling fan versus heat exchanger versus compressor which`

**回帖（复制）**

The decision isn't really about cooling capacity. It's whether outside air is allowed into the cabinet.

**Filtered fan** — cheapest, no compressor, good in a clean control room at normal ambient. Fails in dusty, salty, oily or humid surroundings. As soon as it pressurises the cabinet it routes airborne contaminant through every seal gap you own.

**Heat pipe / liquid heat exchanger** — two isolated circuits, ambient air never mixes with cabinet air, near-zero power, easy to reach high IP, almost no maintenance. Cannot go below ambient, usually only a few degrees. Ideal when contamination is the real constraint and your internal heat can live at ambient.

**Compressor unit** — the only option that holds a setpoint below ambient, and the only one that handles high internal heat plus high ambient plus a sealed dusty cabinet at the same time. Costs more, has a rotating part to service, needs condensate handled.

Short version of the decision rule I use:

- clean room, low heat → fan
- dust / corrosion / humidity is the enemy, target can sit at ambient → heat exchanger
- must go below ambient, or the load is high → compressor unit
- battery room, telecom cabinet, outdoor prefab, high-heat drive cabinet → compressor unit, rated for continuous 24/7 duty

Worth adding: if you choose a compressor unit, decide how the condensate leaves during the design review. A tightly sealed cabinet assembled indoors keeps the moisture from the assembly day, and a unit with no drainage path is a water problem waiting for a humidity spike.

---

## Quora 答案 1｜Why does my electrical cabinet get condensation inside even in summer?

**Quora 答案（复制）**

Because the condensation isn't from outside air — it's from the air already inside the cabinet.

Here is the sequence:

1. The cabinet is assembled indoors. Trapped air carries whatever humidity the shop had that day.
2. The unit cools the internal air below that air's dew point.
3. Moisture leaves the air and condenses on the evaporator. That is the water in the drip tray — normal operation, not a leak.

Three conditions make it worse:

**Low setpoint.** A 20 °C setpoint on a 30 °C ambient cabinet gives a 10 °C spread for condensed water to form. A 28 °C setpoint on the same cabinet collects almost nothing. You usually don't need the cooler cabinet — you need the components inside their rated range.

**-poor circulation.** Cold air pools at the bottom while warm humid air sits on top near the hottest components. You get local condensation and local overheating at the same time.

**Short-cycling.** Every off-cycle lets warm moist air mix back in, so each restart condenses again.

What actually helps, in order: fix the setpoint and the airflow first (free), then check cabinet sealing and drainage path, and only then look at whether the unit needs to be larger. A larger unit that cycles harder will make the condensation worse, not better.

Related: if the cabinet has no drain and no way to dry the tray, that's a design issue to raise before commissioning, not after the first failed insulation test.

---

## Quora 答案 2｜What's the practical difference between a cabinet air conditioner and a normal air conditioner?

**Quora 答案（复制）**

They look related and they behave completely differently. The difference is one thing: whether outside air is allowed inside.

**A normal air conditioner** moves room air. It takes the room's air, cools it, returns it to the room. Its job is to make a large space comfortable.

**A cabinet air conditioner** moves heat out of a sealed box. It runs two isolated air circuits — cabinet air circulates through an evaporator, ambient air goes across the condenser — and the two never mix. Its job is to hold a small space at a set temperature below ambient, and to keep whatever is in the room outside.

Why that matters:

| | Room AC | Cabinet AC |
|---|---|---|
| Air path | room air recirculated | cabinet air isolated from ambient |
| Can go below ambient | yes, relative to the room | yes, relative to the cabinet |
| Dust / moisture ingress | not a design goal | explicitly prevented |
| Duty | intermittent, room comfort | continuous 24/7 industrial duty |
| Filter | none needed | often IP54+/coated coils for dirty air |
| Size | wall-mounted, BTU in the thousands | panel-mounted, watts commonly 300–7,500 |

The rule of thumb people get wrong: a room air conditioner pointed at a cabinet will cool the air around the cabinet, not inside it, and it will drag room dust and humidity along with it. Cabinet cooling exists precisely because the alternative is putting your PLC in the same air you're trying to keep clean.

If you're specifying one: the number that matters is the heat load in watts or BTU/hr, not the cabinet size. An empty cabinet in a hot plant can demand more cooling than a packed one in a cool office.

---

## 执行备注

| 项 | 说明 |
|---|---|
| 搜索 | 每条先用 "Search phrase" 在目标站搜一遍，确认问题还没被好答案占住 |
| 改词 | 回帖必须按原提问者的具体参数改写首段（型号/功率/环境），不能整段粘贴 |
| 频率 | 同一账号每天最多 2 条回帖，多则判 spam |
| 链接 | 只在回帖末尾出现 1 条；若版块规则禁止，就删链接继续回 |
| 品牌 | 五段文字中零品牌名；HCK 只在你自己签名档出现 |

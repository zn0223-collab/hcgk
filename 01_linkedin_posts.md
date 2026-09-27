# LinkedIn 英文帖 ×3（可直接粘贴发布）

> 用法：正文直接粘；**链接放"第一条评论"，不要放正文**。
> 三帖主题互不重复，可分三周发（建议周一/周三/周五，勿同日）。
> 账号：优先用公司页 + 2–3 位工程师个人号交叉发（不要全用同一人）。

---

## 帖 1｜选型：机柜空调被"算小"的三种方式

**标题（LinkedIn 前 3 行决定一切，下面首段即折叠前可见部分）**

Sizing a cabinet air conditioner usually goes wrong in one of three places — not in the cooling capacity number itself.

**正文**

Sizing a cabinet air conditioner usually goes wrong in one of three places — not in the cooling capacity number itself.

Over the last few years of talking to system integrators and panel builders, the same three mistakes keep showing up on commissioning day.

**1. Sizing from nameplate current instead of heat dissipation**

The most expensive mistake, and the most common.

A panel with an 800 A main isolator looks like it needs roughly 384,000 W of cooling if you multiply FLA × voltage. It does not. A isolator barely dissipates anything. What you want is the thermal load of the *actually heat-producing* components — drives, soft starters, power supplies, transformers, braking resistors.

Rule of thumb that holds up in practice: heat dissipation ≈ total loaded power × 3–5 %, depending on how much of the load is electronics versus resistance.

Do it that way and the same panel lands around 15–20 kW instead of 384 kW. Same cabinet, same room, ~20× difference in the answer.

**2. Forgetting the envelope**

The cabinet itself is a heat source. The standard enclosure heat-gain term is:

Q_env = 5.5 × A × ΔT

where A is the cabinet surface area in m² and ΔT is (ambient − target internal temperature).

A 2.2 × 0.8 × 1.2 m cabinet sitting in a 38 °C plant with a 26 °C target is not a small number. Surface area ≈ 39.5 m², so Q_env ≈ 2,600 W before a single component is switched on.

**3. Skipping the multipliers**

Once you have the component load Q_i and the envelope load Q_env:

Q_total = 1.1 × (Q_i + Q_env)

…and then you still apply site conditions:

| Condition | Adjustment |
|---|---|
| Direct solar on the cabinet | +10–30 % |
| Ambient > 40 °C | derate 10–20 % |
| Altitude > 1,000 m | derate ~3 % per 100 m |
| Enclosed, poor air circulation | treat as higher risk, add margin |

Undersized units give away the whole game in a specific way: they never stop running. Capacity drops when the compressor is at 100 % duty — so the cabinet gets warm precisely in the summer week it can least afford it, and the drive trips on its thermal cutoff.

A slightly oversized unit that cycles is almost always the better economic choice.

If you are sizing one of these right now and want the worked version of the calculation with a second example in imperial units, I put it here: https://www.zjhcc.com/en/blog/cabinet-ac-cooling-capacity-sizing.html

— HCK, enclosure cooling

#ControlPanels #IndustrialAutomation #PanelBuilders #EnclosureCooling #ThermalManagement #ElectricalEngineering #SystemIntegration

---

## 帖 2｜温度每升 10℃，你在为多少寿命买单

**首段（折叠前可见）**

Nobody measures what a 15 °C rise inside a control cabinet costs until the drive fails. Then the invoice arrives.

**正文**

Nobody measures what a 15 °C rise inside a control cabinet costs until the drive fails. Then the invoice arrives.

The physics is unglamorous but it is not negotiable. Electrolytic capacitors, cooling fans, relay coils and most industrial electronics are rated for a 40 °C ambient reference. Above that, reaction rates climb roughly 2× per +10 °C, which engineers shorten to the rule: **every +10 °C cuts expected life by about half.**

So a cabinet running at 55 °C internal is not "a bit warm". Against a 25 °C design point it is roughly 4× the accelerated wear.

**Why cabinets get hot in the first place**

The list is short, and the items are all avoidable at design stage:

1. Heat-generating components packed on one side or one door
2. Cold air leaving the unit and never reaching the far corner
3. The unit mounted so its intake faces the cabinet's hot side
4. Ambient above what the unit is rated for (outdoor cabinets in a 50 °C climate are a different machine from an indoor one)
5. Filters that have never been changed (dirty coils = lost capacity, not lost airflow that you notice)

**Two cheap checks you can do this week**

- Temperature mapping: one probe at the top, one at the bottom, one at the hottest component. If the spread is > 10 °C, your airflow is the problem, not your cooling capacity.
- Duty-cycle logging: if the unit ran 100 % of the time last July, size up. Cycling is what you paid for.

**On the "just add a fan" reflex**

A filtered fan pushes positive pressure into the cabinet, and it will find the smallest seal leak and push dust straight through it. It works fine in a clean control room with a dust-free environment. In a foundry, a woodworking shop, or a concrete plant, it moves abrasive material onto your PCBs.

Closed-loop cooling exists for exactly that reason: heat out, ambient air never in.

More on where each method fits, with the trade-off table: https://www.zjhcc.com/en/solutions.html

— HCK, enclosure cooling

#IndustrialAutomation #PredictiveMaintenance #ElectricalEngineering #ControlCabinet #ThermalManagement #Reliability

---

## 帖 3｜密闭机柜散热三选一：压缩式 / 热交换型 / 风扇

**首段（折叠前可见）**

"How do I cool this cabinet?" usually opens as a cooling-capacity question. It's rarely that. It's a "can outside air legally get in?" question.

**正文**

"How do I cool this cabinet?" usually opens as a cooling-capacity question. It is rarely that. It is a *can outside air get in?* question.

Once you separate those two questions, the choice almost makes itself.

**Fan / filtered fan**

- Moves air from the room into the cabinet
- Cheapest, no moving refrigeration parts, decent for a clean control room at moderate ambient
- Fails when the room is dusty, salty, oily or humid
- Positive pressure finds every seal gap and pushes contaminant right at the components

**Heat pipe / heat exchanger (no compressor)**

- Two isolated circuits: cabinet air and ambient air never mix
- Very low power, essentially maintenance-free, easy to reach high IP ratings
- Limited to roughly ambient or a few degrees below it — cannot cool below ambient
- Right answer for moderate internal heat, moderate ambient, and contamination is the real constraint

**Compressor-based cabinet air conditioner**

- The only option that holds a target temperature *below* ambient
- Handles high internal heat load, high ambient, and sealed/dusty environments at the same time
- Costs more, adds a rotating component that needs servicing, needs condensate management
- This is the one for outdoor cabinets, energy storage containers, and high-heat drive cabinets

**A quick decision rule I use**

| Cabinet reality | Go with |
|---|---|
| Clean room, low heat, ambient OK | Fan |
| Dust / corrosion / humidity is the enemy, heat can live at ambient | Heat pipe / exchanger |
| Must go below ambient, or heat load is high | Compressor unit |
| Battery room, telecom cabinet, prefab substation | Compressor unit, 24/7 rated |

One nuance worth remembering: with a compressor unit, a cabinet that is *sealed too tightly* can be a problem for condensate. Air left inside from assembly carries moisture. That is why condensate drainage and proper cabinet sealing specs belong in the design review, not in the field.

Full comparison and the sizing flow behind it: https://www.zjhcc.com/en/whitepaper.html

— HCK, enclosure cooling

#IndustrialAutomation #EnclosureCooling #HeatTransfer #HVAC #ElectricalEngineering #DesignEngineering

---

## 发布备注

| 项 | 说明 |
|---|---|
| 首段 | LinkedIn 折叠约在第 3 行（~210 字符），首段必须自成一句结论 |
| 链接 | 一律 commented-link，不要放正文（LinkedIn 会降权带链帖） |
| 重发 | 同一帖 4 周内不重发到同一账号；换账号需改 ≥ 40 % 文字 |
| 互动 | 发后 2 小时内回复所有评论，回复里可自然带第二次链接 |
| 品牌 | 三帖各出现 1 次 HCK，均在署名行，正文零品牌 |

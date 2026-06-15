# 使用说明 / Instructions — 氢能价值链经济性模拟器 / Hydrogen Value Chain Simulation

> 本文档为**中英文对照**。每段中文后紧跟对应英文。
> This document is **bilingual (Chinese / English)**. Each Chinese passage is followed by its English equivalent.

完整的逐页签、逐参数操作指南。配合 [README.md](./README.md) 阅读。
A complete, tab-by-tab, parameter-by-parameter guide. Read alongside [README.md](./README.md).

---

## 0. 打开与界面布局 / Opening & layout

**中文** — 打开 `index.html` 后,界面分三块:
**English** — After opening `index.html`, the interface has three parts:

- **左侧导航 / Left nav** — 5 个页签(制氢、风光电、全链条、衍生品、敏感性)和来源文件列表。 / The 5 tabs (H2, Power, Value Chain, PtX, Sensitivity) and a list of source files.
- **中间输入 / Center inputs** — 滑块 + 数字框,可拖动也可直接输入数字。 / Sliders plus number boxes; drag or type an exact value.
- **右侧结果 / Right results** — 实时更新的指标卡和图表。 / Live-updating metric cards and charts.

**中文** — 右上角有「场景预设(Scenario)」下拉和「汇率(Exchange rate)」,影响美元折算。所有改动即时生效、无需保存;刷新页面即回到默认值。

**English** — The top-right has a **Scenario** preset dropdown and an **Exchange rate** field (drives the USD conversion). All edits apply instantly with no save; refreshing the page restores defaults.

> 输入与输出都是中英双语,单位直接标在标签上(元/RMB、kWh、Nm³、kg、欧元/EUR 等)。 / Inputs and outputs are bilingual, with units printed on each label.

---

## 1. 制氢成本 / H2 Cost 页签 / tab

**中文** — 测算电解制氢的平准化成本(LCOH)与项目财务回报。
**English** — Computes the levelized cost of hydrogen (LCOH) and project financials.

### 主要输入 / Key inputs

| 参数 / Parameter | 含义 / Meaning | 备注 / Notes |
|---|---|---|
| 电解槽产能 / Capacity | Nm³/h 或 kW 双口径 / In Nm³/h or kW | 两者通过系统电耗自动换算 / The two convert automatically via energy intensity |
| 系统电耗 / Energy intensity | kWh/Nm³ H₂ | 系统级(含 BOP),非单纯电堆 / System-level incl. BOP, not bare stack |
| 电价 / Power price | 元/kWh / RMB/kWh | 制氢成本最敏感的单一变量 / The single most sensitive driver |
| 设备成本 / Equipment CAPEX | 元 / RMB | 见下方设备成本路线 / See equipment-cost routes below |
| 基建成本 / Infrastructure CAPEX | 元 / RMB | 厂房、配套等 / Buildings and balance-of-plant |
| 项目寿命 / Life | 年 / years | 用于 CRF、NPV、IRR / Used for CRF, NPV, IRR |
| 折现率 / Discount rate | % | 资本成本 / Cost of capital |
| 运行天数 / 小时 / Operating days / hours | 天、小时/天 / days, hours/day | 决定年利用小时 / Sets annual operating hours |
| 大修比例 / 周期 / Overhaul ratio / interval | % of 设备、小时 / % of equipment, hours | 周期性大修折旧 / Periodic overhaul charge |
| 人工 / 维护 / 水耗 / 水价 / Labor / maintenance / water use / water price | 元、L/kg、元/L / RMB, L/kg, RMB/L | 运营成本项 / Operating-cost items |

**设备成本路线 / Equipment cost routes**(下拉选择,自动填 CAPEX / dropdown, auto-fills CAPEX):

- **ALK 低位 / ALK low** — 约 1200 元/kW(含电源+BOP),正常成交带下沿。 / ~RMB 1,200/kW incl. rectifier + BOP, lower end of the sustainable band.
- **ALK 高位 / ALK high** — 约 1600 元/kW,常规配置或非压价场景。 / ~RMB 1,600/kW, standard configuration or non-aggressive pricing.
- **PEM 系统 / PEM system** — 约 3000 元/kW(成交带 2800–3200)。 / ~RMB 3,000/kW (band 2,800–3,200).
- **自定义 / Custom** — 手动输入设备总成本。 / Enter equipment cost manually.

### 主要输出 / Key outputs

- **LCOH(元/kg)/ LCOH (RMB/kg)** — 平准化制氢成本,核心指标;同时给出美元折算。 / Levelized hydrogen cost, the headline metric; USD value also shown.
- **年产量 / Annual output**(kg、Nm³ / kg, Nm³)。
- **NPV、IRR、回收期 / Payback** — 基于逐年现金流。 / Based on yearly cash flows.
- **EBITDA、单位电费、单位水费等成本拆解,外加现金流柱状/折线图。** / EBITDA, unit power and water cost breakdowns, plus a cash-flow bar/line chart.

> 计算逻辑:`年化CAPEX = (设备+基建) × CRF(折现率, 寿命)`;`LCOH = (年化CAPEX + 年运营) / 年产量`。 / Logic: `annualized CAPEX = (equipment + infra) × CRF(rate, life)`; `LCOH = (annualized CAPEX + annual opex) / annual output`.

---

## 2. 风光电成本 / Power LCOE 页签 / tab

**中文** — 分别测算光伏与风电的度电成本(LCOE)。
**English** — Computes solar PV and wind LCOE separately.

### 主要输入 / Key inputs（PV 与 Wind 各一组 / one set each for PV and Wind）

- **装机容量 / Capacity**(MW)
- **利用小时 / Full-load hours**(h/yr)
- **单位 CAPEX / Unit CAPEX**(元/kW / RMB/kW)
- **年衰减率 / Degradation**(%/yr)— 逐年发电量递减 / annual generation declines year over year
- **运维率 / 保险率 / Repair & insurance rates**(占 CAPEX 的 % / % of CAPEX)
- **材料费 / 其他费 / Material & other costs**(元/MW / RMB/MW)
- **寿命 / 折现率 / Life & discount rate**

### 输出 / Outputs

- **LCOE(元/kWh)/ LCOE (RMB/kWh)** — 贴现总成本 ÷ 贴现总发电量。 / Discounted total cost ÷ discounted total generation.
- **年发电量、年运维成本、总 CAPEX / Annual generation, annual O&M, total CAPEX。**

> 退役成本按 CAPEX 的 2% 在寿命末期贴现计入。这一页的 LCOE 可作为制氢页电价的参考绿电成本。 / Decommissioning is included at 2% of CAPEX discounted at end of life. This LCOE can feed the "power price" on the H2 tab.

---

## 3. 全链条经济性 / Value Chain 页签 / tab

**中文** — 把制氢成本接上「运输 → 认证 → 转化 → 贸易加价 → 欧洲碳价政策」,得到对接欧洲市场的净经济性。

**English** — Extends H2 cost through transport → certification → conversion → trading margin → EU carbon policy to give the net economics into the EU market.

### 应用场景一键预设 / Application presets

**中文** — 选择场景会自动带出该场景的碳价、政策覆盖率、罚则乘数、支付意愿(WTP)、转化费:
**English** — Selecting an application auto-fills its carbon price, policy coverage, penalty multiplier, willingness-to-pay (WTP), and conversion cost:

- **炼化 RFNBO / Refining**(RED III)
- **航运 / Shipping**(FuelEU Maritime,罚则约 640 €/tCO₂e / penalty ~EUR 640/tCO₂e)
- **航空 eSAF / Aviation**(ReFuelEU,支付意愿最高 / highest WTP)
- **绿氨出口欧洲 / Ammonia export to Europe**
- **钢铁绿钢溢价 / Steel green premium**

### 其他输入 / Other inputs

- **运输方式 / Transport** — 内置 20MPa 长管拖车 50–500 km 的成本曲线(4.19 → 20.38 元/kg),或手动输入。 / Built-in 20 MPa tube-trailer cost curve 50–500 km (RMB 4.19 → 20.38/kg), or manual entry.
- **认证费、转化费、贸易加价、欧元汇率、避免排放量、支付意愿。** / Certification cost, conversion cost, trading margin, EUR rate, avoided emissions, WTP.

### 输出 / Outputs

- **直接成本 / 到岸成本 / Delivered cost**(含贸易加价 / incl. trading margin)
- **碳价价值 / Carbon value**(减排收益 / emissions-avoidance benefit)
- **净有效成本 / Net effective cost**
- **毛利 / Margin、年价值 / Annual value**
- **打平碳价 / Break-even carbon price** — 让项目刚好打平所需的碳价。 / The carbon price at which the project exactly breaks even.

> 碳价价值 = 避免排放(t) × 碳价(€/t) × 汇率 × 罚则乘数 × 政策覆盖率,折算为每 kg 氢。 / Carbon value = avoided CO₂ (t) × carbon price (€/t) × FX × penalty multiplier × policy coverage, per kg H₂.

---

## 4. 衍生品联动 / PtX Linkage 页签 / tab

**中文** — 由氢价联动测算绿氨、绿色甲醇、eSAF 每吨产品的成本。
**English** — Computes per-tonne cost of green ammonia, methanol, and eSAF, linked to the hydrogen price.

### 氢价来源（联动模式）/ Hydrogen-cost basis

- **联动制氢页 / Linked** — 直接用制氢页算出的 LCOH。 / Uses the LCOH computed on the H2 tab.
- **本页绿电重算 / Recalc from this page** — 用本页绿电价重新跑一遍 LCOH。 / Recomputes LCOH from this page's green-power price.
- **手填氢价 / Manual** — 直接输入氢价。 / Enter the hydrogen price directly.

### 工艺路线 / Process routes（各产品可选 / selectable per product）

- **绿氨 / Ammonia**:电解氢+空分全电 HB、余热回收 HB、柔性模块化 HB。 / Electrolytic H₂ + ASU all-electric HB, heat-recovery HB, flexible modular HB.
- **甲醇 / Methanol**:CO₂ 直接加氢、RWGS+合成气。 / Direct CO₂ hydrogenation, RWGS + syngas.
- **eSAF**:RWGS+FT、直接 CO₂-FT/高温共电解、甲醇制航煤 MtJ。 / RWGS + FT, direct CO₂-FT / high-temperature co-electrolysis, methanol-to-jet (MtJ).

**中文** — 选路线会自动带出该路线的氢耗(kg/t)、CO₂ 用量(t/t)、辅助电耗(kWh/t)、其他成本(元/t),也可手动覆盖。还有「项目基准 / 理论化学计量下限」等预设。

**English** — Selecting a route auto-fills its H₂ use (kg/t), CO₂ use (t/t), aux power (kWh/t), and other cost (RMB/t) — all overridable. Presets include a project base case and a stoichiometric lower bound.

### 输出 / Outputs

**中文** — 每个产品给出单位成本拆解:氢成本 + CO₂ 成本 + 辅助电成本 + 其他成本 = 每吨总成本。
**English** — Per-product cost breakdown: H₂ + CO₂ + aux power + other = total cost per tonne.

---

## 5. 敏感性对比 / Sensitivity 页签 / tab

**中文** — 扫描关键变量(主要是电价),对比 LCOH 与三种衍生品成本如何随之变化,以图表呈现。用于快速看清「哪个变量最致命」。

**English** — Sweeps a key variable (mainly power price) and charts how LCOH and the three product costs respond — a quick way to see which lever matters most.

---

## 6. 场景预设 / Scenario presets（右上角 / top-right）

- **低电价 / Low power** — 低电价 + 对应售价。 / Low power price plus matching selling price.
- **高利用率 / High utilization** — 更多运行天数/小时。 / More operating days/hours.
- **压力测试 / Stress** — 高电价 + 高 CAPEX + 低售价,看最坏情况。 / High power price + high CAPEX + low selling price, the worst case.

> 一键切换即可对比不同假设下的结果。 / Switch in one click to compare outcomes under different assumptions.

---

## 7. 实用技巧 / Tips

1. **先定电价,再调其他**:制氢成本里电费往往占大头,先把电价/电耗调到真实区间。 / **Set power price first**: electricity usually dominates LCOH, so pin power price/intensity to a realistic range before anything else.
2. **产能两种口径互通**:改 Nm³/h 或 kW 任一个,另一个按系统电耗自动换算。 / **Two capacity units are linked**: change Nm³/h or kW and the other follows via energy intensity.
3. **数字框可直接输入**:不必拖滑块,点数字框输入精确值。 / **Type exact values**: click the number box instead of dragging the slider.
4. **美元折算看右上汇率**:改汇率影响所有 USD 显示。 / **USD figures follow the top-right FX rate**: changing it updates every USD value.
5. **想保存某套假设**:目前不内置存档,可截图,或把 `index.html` 里的 `*Defaults` 常量改成你的值后另存一份。 / **To save an assumption set**: there's no built-in save — screenshot it, or edit the `*Defaults` constants in `index.html` and keep your own copy.
6. **复核公式**:右键查看源代码,搜索 `h2Model`、`powerModel`、`chainModel`、`productModelAtPowerPrice` 即是四段核心算法。 / **Verify the formulas**: view source and search for `h2Model`, `powerModel`, `chainModel`, `productModelAtPowerPrice` — the four core routines.

---

## 8. 常见问题 / FAQ

**Q：默认场景为什么是亏损的？/ Why is the default scenario loss-making?**
中文 — 默认数字只是占位示例。若默认电价/电耗偏高、售价偏低,单位电费可能超过售价,项目自然亏损。换成你项目的真实参数即可。
English — The defaults are placeholders. If the default power price/intensity is high and the selling price low, unit electricity cost can exceed the price, so the project loses money. Swap in your real numbers.

**Q：需要联网吗？/ Does it need an internet connection?**
中文 — 不需要。全部计算在浏览器本地完成,不上传任何数据。
English — No. Everything runs locally in the browser; nothing is uploaded.

**Q：数据会被发到服务器吗？/ Is any data sent to a server?**
中文 — 不会。但任何能打开页面的人都能在源码看到公式和默认假设——敏感场景请用私有仓库或加访问控制。
English — No — but anyone who opens the page can read the source. Use a private repo / access control for sensitive assumptions.

**Q：用什么浏览器？/ Which browser?**
中文 — 任意现代浏览器(Chrome / Edge / Safari / Firefox)。无需安装、无依赖。
English — Any modern browser (Chrome / Edge / Safari / Firefox). No install, no dependencies.

---

许可证 / License: [MIT](./LICENSE) © 2026 YC

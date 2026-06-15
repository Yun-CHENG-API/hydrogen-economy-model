# 氢能价值链经济性模拟器 / Hydrogen Value Chain Simulation

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
![Static site](https://img.shields.io/badge/runs-100%25%20in%20browser-success)
![No backend](https://img.shields.io/badge/backend-none-lightgrey)

一个**完全在浏览器中运行**的氢能价值链经济性测算工具。从绿电、制氢，到跨境运输、欧洲碳价政策，再到绿氨 / 绿色甲醇 / eSAF，一个界面端到端把每一段成本算清楚。打开 `index.html` 即可使用——没有后端、没有安装、没有数据上传。

A **fully client-side** techno-economic simulator for the green-hydrogen value chain — from renewable power and electrolysis, through cross-border transport and EU carbon-price policy, to downstream products (ammonia, methanol, eSAF). Open `index.html` and go: no backend, no install, nothing uploaded anywhere.

> 详细的逐参数操作说明见 **[INSTRUCTIONS.md](./INSTRUCTIONS.md)**。
> For a full, parameter-by-parameter walkthrough, see **[INSTRUCTIONS.md](./INSTRUCTIONS.md)**.

---

## 30 秒上手 / 30-second start

不想读文档,三步即可:

1. 点绿色 **Code → Download ZIP**(或 `git clone`),解压。
2. 双击 `index.html`,用任意现代浏览器打开。
3. 左侧切换 5 个页签,拖动滑块,右侧结果实时更新。

Don't want to read docs:

1. **Code → Download ZIP** (or `git clone`), unzip.
2. Double-click `index.html` in any modern browser.
3. Switch between the 5 tabs on the left, drag the sliders, watch the results update live.

```bash
git clone https://github.com/Yun-CHENG-API/hydrogen-economy-model.git
cd hydrogen-economy-model
open index.html       # macOS;  Windows: 双击 index.html;  Linux: xdg-open index.html
```

如果开了 GitHub Pages,直接在线打开(无需下载):
If GitHub Pages is enabled, open it online (no download needed):

**https://yun-cheng-api.github.io/hydrogen-economy-model/**

---

## 五个页签 / The five tabs

| 页签 / Tab | 算什么 / What it computes | 关键输出 / Key outputs |
|---|---|---|
| **制氢成本 / H2 Cost** | 电解制氢的单位成本与项目财务 | LCOH(元/kg)、NPV、IRR、回收期 |
| **风光电成本 / Power LCOE** | 光伏与风电的度电成本 | LCOE(元/kWh)、年发电量、年运维 |
| **全链条经济性 / Value Chain** | 运输+认证+转化+贸易+碳价,对接欧洲市场 | 到岸成本、碳价价值、净成本、毛利、打平碳价 |
| **衍生品联动 / PtX Linkage** | 绿氨 / 绿色甲醇 / eSAF 的单位成本 | 每吨产品成本拆解(氢耗/CO₂/辅电/其他) |
| **敏感性对比 / Sensitivity** | 电价等关键变量扫描 | 成本随电价变化的对比图 |

---

## 能调什么 / What you can change

- **制氢**:产能(Nm³/h 或 kW 双口径)、系统电耗、电价、设备/基建 CAPEX、寿命、折现率、运行小时、大修周期、人工/维护、水耗。设备成本内置 **ALK 低/高位、PEM、自定义**四条成本路线。
- **绿电**:光伏 / 风电的装机、利用小时、单位 CAPEX、衰减率、运维/保险/材料费、寿命、折现率。
- **价值链**:应用场景(炼化 / 航运 / 航空 / 绿氨出口 / 绿钢)一键带出对应的碳价、政策覆盖率、支付意愿;运输距离(20MPa 长管拖车 50–500 km 内置成本)、认证费、转化费、贸易加价、欧元汇率。
- **衍生品**:绿氨 / 甲醇 / eSAF 各自的工艺路线(如电解氢+空分全电 HB、CO₂ 直接加氢、RWGS+FT 等),以及氢耗、CO₂ 用量、辅助电耗、其他成本。
- **场景预设**:低电价 / 高利用率 / 压力测试 等一键切换。

> ⚠️ **关于默认数字 / About the defaults**:界面里的默认数值只是占位示例,用于演示,**不是经过核实的正式输入**。请用你自己项目的真实参数替换后再做决策。
> The default numbers are placeholder examples for demonstration — **not validated inputs**. Replace them with your own project assumptions before drawing conclusions.

---

## 方法学速览 / Methodology at a glance

- **LCOH / LCOE**:年化资本回收(CRF)+ 运营成本,除以年产量/年发电量,得到平准化单位成本。
- **NPV / IRR**:按项目寿命逐年现金流贴现;IRR 用二分法求解。
- **碳价价值**:按避免的 CO₂ 排放 × 碳价 × 政策覆盖率 × 罚则乘数折算为每 kg 氢的减排收益。
- 全部公式都写在 `index.html` 源码里,任何人都能查看、复核、修改。

LCOH/LCOE use an annualized capital-recovery factor plus operating costs over annual output. NPV discounts the yearly cash flows over project life; IRR is solved by bisection. Carbon value is avoided CO₂ × carbon price × policy coverage × penalty multiplier per kg of H₂. Every formula lives in the `index.html` source — fully inspectable.

---

## 仓库结构 / Repository layout

```
hydrogen-economy-model/
├── index.html        # 模型本体 / the model (single self-contained file)
├── README.md         # 本文件 / this file
├── INSTRUCTIONS.md   # 详细使用说明 / full usage guide
├── LICENSE           # MIT
└── _headers          # 静态托管安全响应头 / security headers for Pages/Netlify
```

## 部署 / Deploy

本仓库即一个静态站点,可原样部署到 **GitHub Pages、Cloudflare Pages、Netlify**。`_headers` 提供基础安全响应头(Cloudflare Pages / Netlify 生效)。
This repo is a static site and deploys as-is to GitHub Pages, Cloudflare Pages, or Netlify. `_headers` sets basic security headers (Cloudflare Pages / Netlify).

## 隐私 / Privacy

所有计算都在你的浏览器本地完成,不向任何服务器发送数据。注意:**任何能打开页面的人都能在源码里看到公式和默认假设**。若假设敏感,请用私有仓库或加访问控制。
All computation runs locally in your browser; nothing is sent to any server. Note that **anyone who can open the page can read the formulas and default assumptions in the source** — keep the repo private or add access control if the assumptions are sensitive.

## 许可证 / License

[MIT](./LICENSE) © 2026 YC — 可自由使用、修改、商用,保留版权声明即可。
Free to use, modify, and commercialize; just keep the copyright notice.

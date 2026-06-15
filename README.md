# 氢气经济模型交互界面 / Hydrogen Economy Model — Interactive Interface

一个完全在浏览器中运行的氢能经济性测算工具，覆盖**制氢成本 (LCOH)**、**光伏/风电度电成本 (LCOE)**、**碳价价值链**，以及**绿氨 / 绿色甲醇 / eSAF** 单位成本。打开 `index.html` 即可使用，无需后端、无需安装。

A fully client-side techno-economic model for green hydrogen. It covers levelized cost of hydrogen (LCOH), solar/wind LCOE, a carbon-price value chain, and downstream products (green ammonia, green methanol, eSAF). Just open `index.html` — no backend, no install.

## 在线使用 / Quick start

下载或克隆本仓库后，直接用浏览器打开 `index.html`。所有计算与默认假设都在该 HTML 文件中，可在源码里查看公式。

Clone or download, then open `index.html` in any modern browser. All formulas and default assumptions live in that single file.

```bash
git clone https://github.com/<your-account>/hydrogen-economy-model.git
cd hydrogen-economy-model
open index.html   # macOS；Windows 直接双击 index.html
```

## 功能 / What it computes

- **制氢 / Hydrogen**: 产能、电耗、CAPEX/OPEX、大修折旧，输出 LCOH、NPV、IRR、回收期。
- **绿电 / Power**: 光伏与风电的 LCOE（含衰减、运维、退役）。
- **价值链 / Chain**: 物流、认证、转化、贸易加价，叠加碳价价值与支付意愿 (WTP)。
- **下游产品 / Products**: 绿氨、绿色甲醇、eSAF 的单位成本拆解（氢耗、CO₂、辅助电、其他）。

> 说明 / Note: 界面中的默认数字仅为占位示例，并非正式输入参数。请以你自己的项目参数为准。
> The default numbers are placeholder values for demonstration, not validated inputs. Replace them with your own project assumptions.

## 部署为静态网站 / Deploy as a static site

本仓库就是一个静态站点，可直接部署到 GitHub Pages、Cloudflare Pages、Netlify 等。`_headers` 文件提供了基础安全响应头（适用于 Cloudflare Pages / Netlify）。

This repo is a static site and deploys as-is to GitHub Pages, Cloudflare Pages, or Netlify. The `_headers` file sets basic security headers (Cloudflare Pages / Netlify).

## 许可证 / License

[MIT](./LICENSE) © 2026 YC — 可自由使用、修改、商用，保留版权声明即可。

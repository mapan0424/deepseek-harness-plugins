# `@anarkhgatsby/deepseek-harness-insights`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-insights.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-insights)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

A bundled Cordis plugin for **DeepSeek Harness**. It adds a local-first **Usage insights** settings page without modifying upstream Harness source.

> ⚠️ **Unofficial Disclaimer**: This project is developed and maintained independently by the open-source community. It is **NOT** an official DeepSeek product.

---

## 📊 Preview

The plugin adds a **Usage insights** page under Harness settings, with token activity, model usage, active sessions, cache hit rate, activity breakdown, and the most frequently used tools.

* **Dual-Theme Support**:
  * ☀️ **Light Mode**: Pure classic emerald/forest green gradient.
  * 🌙 **Dark Mode**: Codex-inspired deep obsidian canvas with vibrant neon hot-pink/magenta (`#ff3388`) saturation curve.
* **Golden Ratio Heatmap Matrix**: Dense, breathable 2.7px grid spacing with enlarged cells.

![Harness Insights usage dashboard](https://raw.githubusercontent.com/mapan0424/deepseek-harness-plugins/main/packages/harness-insights/assets/screenshots/usage-insights-en.png)

---

## 📥 Installation

The package follows the official Harness bundle manifest and can be installed into a profile with `dsh plugin`:

```bash
# Install into default profile
dsh plugin add @anarkhgatsby/deepseek-harness-insights

# Or install into a specific profile
dsh plugin --profile demo add @anarkhgatsby/deepseek-harness-insights
dsh --profile demo
```

To remove it later:
```bash
dsh plugin --profile demo remove @anarkhgatsby/deepseek-harness-insights
```

For local development:
```bash
dsh plugin --profile demo add ./packages/harness-insights
```

---

## 🔒 Data Boundary & Privacy

Harness Insights folds only structured session metadata:

* `assistant/message.data.usage`
* `assistant/message.data.message.source.provider/model`
* `tool/call.data.name`
* Event timestamps and session projection identity

It **never** requests session history in the browser, stores message content, reads API keys, or uploads usage data. Historical aggregation runs through Harness's official `sessionProjectionCache.coldSnapshot()` path and persists only the projection checkpoint owned by Harness.

---

## 🎨 Tool Icon Assets

The UI includes a Codex-style Harness tool icon set: 26 matching SVG pairs for light and dark interfaces. The build embeds the optimized pairs into the client bundle; the UI switches them through Harness's `body[data-ds-dark-theme]` contract without its own theme preference.

---

## 📄 License

[MIT License](./LICENSE)

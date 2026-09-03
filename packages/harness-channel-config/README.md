# `@anarkhgatsby/deepseek-harness-channel-config`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-config.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Visual channel settings center for **DeepSeek Harness** (Feishu / WeCom / iMessage / Telegram / DingTalk, etc.).

> ⚠️ **Unofficial Disclaimer**: This project is developed and maintained independently by the open-source community. It is **NOT** an official DeepSeek product.

---

## 🌟 Key Features

`@anarkhgatsby/deepseek-harness-channel-config` provides a unified graphical configuration center integrated directly into the DeepSeek Harness settings UI:

* 🎛️ **Zero YAML/JSON Editing**: Configure channel credentials and parameters directly via an intuitive Web interface.
* 🔍 **Smart Channel Auto-Detection**: Dynamically scans installed channel plugins in your runtime and only renders configuration forms for active channels.
* ⚡ **Hot-Reloading**: Update App IDs, Secrets, Tokens, and endpoints with instant live updates—no process restart required.
* 🔒 **Sensitive Credential Masking**: Built-in secret masking prevents accidental exposure during screen sharing or recording.
* 🎨 **Native Design Integration**: Perfectly inherits the Harness UI design tokens and automatically adapts to Light and Dark modes.

---

## 📥 Installation

Install via the `dsh plugin` CLI:

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-config
```

*(Note: This package provides the visual configuration UI. To use specific channels, install their respective plugins as well, e.g., `@anarkhgatsby/deepseek-harness-channel-feishu`)*.

---

## 🚀 Quick Start Guide

### Step 1: Install Channel Config & Channels
```bash
# Example: Install config panel + Feishu & WeCom channels
dsh plugin add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin add @anarkhgatsby/deepseek-harness-channel-wecom
```

### Step 2: Open DeepSeek Harness Settings
1. Start DeepSeek Harness (`dsh` or via Desktop App);
2. Open **Settings ➔ Channel Configuration (渠道设置)** in the navigation menu;
3. Fill in your bot credentials (e.g., Feishu App ID & App Secret);
4. Click **Save & Connect**—your bot goes online immediately!

---

## 📄 License

[MIT License](./LICENSE)

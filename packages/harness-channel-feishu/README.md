# `@anarkhgatsby/deepseek-harness-channel-feishu`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-feishu.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-feishu)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Feishu / Lark bot channel integration for **DeepSeek Harness** (powered by WebSocket long-connection and unified `GatewayCore`).

> ⚠️ **Unofficial Disclaimer**: This project is developed and maintained independently by the open-source community. It is **NOT** an official DeepSeek or Feishu/Lark product.

---

## 🌟 Key Features

* 🚀 **No Public IP or Webhook Needed**: Connects directly via Feishu's native WebSocket long-connection mode—works perfectly in home networks, local machines, or private VPCs.
* ⚡ **Streaming Card Typing**: Real-time streaming response directly updates Feishu interactive message cards with smooth typing animation.
* 💬 **Direct Messages & Group Chats**: Supports private 1-on-1 chats and group mentions (`@Bot`).
* 🛡️ **Built-in Deduplication**: Backed by `@anarkhgatsby/deepseek-harness-core` to eliminate duplicate responses caused by network retries.
* 🖼️ **Rich Markdown Rendering**: Automatically formats tables, code blocks, and lists for optimal display on desktop and mobile Lark apps.

---

## 📥 Installation

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-feishu
```

*(Recommended: Also install `@anarkhgatsby/deepseek-harness-channel-config` to configure credentials via Web UI)*.

---

## 🚀 Feishu Open Platform Setup (3-Minute Guide)

1. Go to the [Feishu Open Platform Developer Console](https://open.feishu.cn/app/) and create a **Custom Enterprise App**.
2. **Add Bot Capability**: Navigate to **Add Features ➔ Bot** and enable the robot.
3. **Enable WebSocket Mode**:
   * Go to **Event Subscriptions**;
   * Select **Use long connection to receive events (WebSocket)**.
4. **Grant Permissions**:
   * Navigate to **Permissions Management**;
   * Grant `im:message` (Read and send messages) and `im:chat` (Obtain group chat info).
5. **Publish Version**: Create and release the initial version in **Version Management & Release**.
6. **Obtain Credentials**:
   * Copy the **App ID** (starts with `cli_...`) and **App Secret** from **Credentials & Basic Info**.

---

## ⚙️ Configuration

### Method 1: Via Visual Settings (Recommended)
Open DeepSeek Harness ➔ **Settings ➔ Channel Configuration** ➔ Enter your `App ID` and `App Secret` ➔ Click **Save & Connect**.

### Method 2: Via Configuration YAML
```yaml
"@anarkhgatsby/deepseek-harness-channel-feishu":
  appId: "cli_a1b2c3d4e5f6"
  appSecret: "your_app_secret_here"
  encryptKey: ""
  verificationToken: ""
  connectionMode: "websocket"
```

---

## 📄 License

[MIT License](./LICENSE)

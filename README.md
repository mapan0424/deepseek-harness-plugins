# 🧩 DeepSeek Harness Plugins (Unofficial Community Monorepo)

[English](README.md) | [简体中文](README.zh-CN.md)

[![CI](https://github.com/mapan0424/deepseek-harness-plugins/actions/workflows/ci.yml/badge.svg)](https://github.com/mapan0424/deepseek-harness-plugins/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![pnpm workspace](https://img.shields.io/badge/pnpm-workspace-orange.svg)](https://pnpm.io/workspaces)

A curated collection of **unofficial community plugins** for **DeepSeek Harness** (supporting Web, Docker, and Desktop runtimes).

> ⚠️ **Unofficial Disclaimer**: This project is developed and maintained independently by the open-source community. It is **NOT** an official DeepSeek product, and is not sponsored, endorsed, or affiliated with DeepSeek in any way.

---

## 📑 Table of Contents

- [Plugin Marketplace Directory](#-plugin-marketplace-directory)
  - [1. Core & Infrastructure](#1-core--infrastructure)
  - [2. Messaging & Collaboration Channels](#2-messaging--collaboration-channels)
  - [3. Analytics & Insights](#3-analytics--insights)
  - [4. UI & Localization](#4-ui--localization)
- [How to Install Plugins](#-how-to-install-plugins)
- [Configuration & Usage Examples](#-configuration--usage-examples)
- [Local Development & Contribution](#-local-development--contribution)
- [License](#-license)

---

## 📦 Plugin Marketplace Directory

### 1. Core & Infrastructure

| Package Name | Version | Description | Quick Install | npm |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-core`** | `0.1.0` | Unified `GatewayCore` message bus routing, deduplication, and multi-channel dispatch hub. | `pnpm add @anarkhgatsby/deepseek-harness-core` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-core)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-core) |
| **`@anarkhgatsby/deepseek-harness-channel-config`** | `0.1.4` | Visual channel settings UI inside the Harness Web interface (Feishu / WeCom / iMessage). | `pnpm add @anarkhgatsby/deepseek-harness-channel-config` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-config)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config) |

---

### 2. Messaging & Collaboration Channels

| Package Name | Version | Description | Quick Install | npm |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-channel-feishu`** | `0.1.0` | Feishu / Lark bot integration with WebSocket long-connection mode, rich cards, and streaming typing. | `pnpm add @anarkhgatsby/deepseek-harness-channel-feishu` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-feishu)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-feishu) |
| **`@anarkhgatsby/deepseek-harness-channel-wecom`** | `0.1.1` | WeCom (Enterprise WeChat) bot and application integration. | `pnpm add @anarkhgatsby/deepseek-harness-channel-wecom` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-wecom)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-wecom) |
| **`@anarkhgatsby/deepseek-harness-channel-imessage`** | `0.1.1` | Native local iMessage integration on macOS (reads `Messages.app` SQLite DB with secure dispatch). | `pnpm add @anarkhgatsby/deepseek-harness-channel-imessage` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-imessage)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage) |

---

### 3. Analytics & Insights

| Package Name | Version | Description | Quick Install | npm |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-insights`** | `0.1.4` | Local-first usage statistics, token consumption breakdowns, conversation heatmaps, and analytics charts. | `pnpm add @anarkhgatsby/deepseek-harness-insights` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-insights)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-insights) |

---

### 4. UI & Localization

| Package Name | Version | Description | Quick Install | npm |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-locale-pack`** | `0.1.1` | Multi-language and ethnic minority language pack (Tibetan, Mongolian, Uyghur, Nuosu Yi, Traditional Chinese, Japanese, Korean, etc.). | `pnpm add @anarkhgatsby/deepseek-harness-locale-pack` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-locale-pack)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-locale-pack) |

---

## 📥 How to Install Plugins

In your DeepSeek Harness workspace runtime:

### Step 1: Install via npm / pnpm
```bash
# Example: Install Feishu Channel & Visual Config Panel
pnpm add @anarkhgatsby/deepseek-harness-channel-feishu @anarkhgatsby/deepseek-harness-channel-config
```

### Step 2: Register in `cordis.patch.yml` or Harness Config
Add the installed plugin to your runtime plugins list:
```yaml
plugins:
  "@anarkhgatsby/deepseek-harness-channel-feishu": {}
  "@anarkhgatsby/deepseek-harness-channel-config": {}
```

---

## ⚙️ Configuration & Usage Examples

### 1. Feishu / Lark Channel Configuration
In your Harness settings UI or configuration file:
```yaml
"@anarkhgatsby/deepseek-harness-channel-feishu":
  appId: "cli_a1b2c3d4e5f6"
  appSecret: "your_app_secret_here"
  encryptKey: ""
  verificationToken: ""
  connectionMode: "websocket" # Recommended: no public IP required
```

### 2. WeCom (Enterprise WeChat) Channel Configuration
```yaml
"@anarkhgatsby/deepseek-harness-channel-wecom":
  corpId: "ww1234567890abcdef"
  agentId: 1000002
  secret: "your_wecom_agent_secret"
  token: "your_callback_token"
  encodingAesKey: "your_aes_key"
```

### 3. Usage Insights Analytics
Once `@anarkhgatsby/deepseek-harness-insights` is enabled:
* Open your DeepSeek Harness web interface or desktop window;
* Click the **📊 Usage Insights** icon in the sidebar or top navigation;
* View real-time daily active tokens, cost projection, session distributions, and tool call traces.

### 4. Language Pack (Locale Pack)
Once `@anarkhgatsby/deepseek-harness-locale-pack` is loaded:
* Go to **Settings ➔ General ➔ Language**;
* Select from expanded options: Tibetan (བོད་ཡིག), Uyghur (ئۇيغۇرچە), Mongolian (Монгол хэл), Nuosu Yi (ꆈꌠ꒿), Traditional Chinese (繁體中文), Japanese (日本語), Korean (한국어), etc.

---

## 🛠️ Local Development & Contribution

This repository uses **pnpm Workspaces** and **Changesets** for modular development.

### 1. Clone & Install
```bash
git clone https://github.com/mapan0424/deepseek-harness-plugins.git
cd deepseek-harness-plugins
pnpm install
```

### 2. Run Tests
```bash
pnpm test
```

### 3. Create a Changeset for Release
```bash
pnpm changeset
```

### 4. Versioning & Publishing
```bash
# Bump version and generate changelog
pnpm version:packages

# Publish modified packages to npm
pnpm publish:packages
```

For detailed plugin architecture and authoring guides, see [docs/plugin-development-guide.md](./docs/plugin-development-guide.md).

---

## 📄 License

All plugins in this repository are licensed under the [MIT License](./LICENSE).

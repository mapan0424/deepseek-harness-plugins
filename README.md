# 🧩 DeepSeek Harness Plugins (Unofficial Community Monorepo)

[English](README.md) | [简体中文](README.zh-CN.md)

[![CI](https://github.com/mapan0424/deepseek-harness-plugins/actions/workflows/ci.yml/badge.svg)](https://github.com/mapan0424/deepseek-harness-plugins/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![pnpm workspace](https://img.shields.io/badge/pnpm-workspace-orange.svg)](https://pnpm.io/workspaces)

A curated collection of **unofficial community plugins** for **DeepSeek Harness** (compatible with Web UI, Docker deployments, and Desktop runtimes).

> ⚠️ **Unofficial Disclaimer**: This project is developed and maintained independently by the open-source community. It is **NOT** an official DeepSeek product, and is not sponsored, endorsed, or affiliated with DeepSeek in any way.

---

## 📑 Table of Contents

- [📦 Plugin Marketplace Directory](#-plugin-marketplace-directory)
  - [1. Core & Infrastructure](#1-core--infrastructure)
  - [2. Messaging & Collaboration Channels](#2-messaging--collaboration-channels)
  - [3. Analytics & Insights](#3-analytics--insights)
  - [4. UI & Localization](#4-ui--localization)
- [📥 How to Install Plugins via `dsh plugin`](#-how-to-install-plugins-via-dsh-plugin)
- [⚙️ Plugin Configuration & Usage](#️-plugin-configuration--usage)
- [🛠️ Monorepo Local Development & Publishing](#️-monorepo-local-development--publishing)
- [📄 License](#-license)

---

## 📦 Plugin Marketplace Directory

### 1. Core & Infrastructure

| Package Name | Version | Description | Install Command (`dsh plugin`) | npm |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-core`** | `0.1.0` | Unified `GatewayCore` message bus routing, deduplication, and multi-channel dispatch hub. | `dsh plugin add @anarkhgatsby/deepseek-harness-core` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-core)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-core) |
| **`@anarkhgatsby/deepseek-harness-channel-config`** | `0.1.4` | Visual channel settings UI inside the Harness Web interface (Feishu / WeCom / iMessage). | `dsh plugin add @anarkhgatsby/deepseek-harness-channel-config` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-config)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config) |

---

### 2. Messaging & Collaboration Channels

| Package Name | Version | Description | Install Command (`dsh plugin`) | npm |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-channel-feishu`** | `0.1.0` | Feishu / Lark bot integration with WebSocket long-connection mode (no public IP required), rich cards, and streaming typing. | `dsh plugin add @anarkhgatsby/deepseek-harness-channel-feishu` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-feishu)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-feishu) |
| **`@anarkhgatsby/deepseek-harness-channel-wecom`** | `0.1.1` | WeCom (Enterprise WeChat) bot and application integration. | `dsh plugin add @anarkhgatsby/deepseek-harness-channel-wecom` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-wecom)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-wecom) |
| **`@anarkhgatsby/deepseek-harness-channel-imessage`** | `0.1.1` | Native local iMessage integration on macOS (reads `Messages.app` SQLite DB with secure local dispatch). | `dsh plugin add @anarkhgatsby/deepseek-harness-channel-imessage` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-imessage)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage) |

---

### 3. Analytics & Insights

| Package Name | Version | Description | Install Command (`dsh plugin`) | npm |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-insights`** | `0.1.4` | Local-first usage statistics, token consumption breakdowns, conversation heatmaps, and analytics charts. | `dsh plugin add @anarkhgatsby/deepseek-harness-insights` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-insights)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-insights) |

---

### 4. UI & Localization

| Package Name | Version | Description | Install Command (`dsh plugin`) | npm |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-locale-pack`** | `0.1.1` | Multi-language and ethnic minority language pack (Tibetan, Mongolian, Uyghur, Nuosu Yi, Traditional Chinese, Japanese, Korean, etc.). | `dsh plugin add @anarkhgatsby/deepseek-harness-locale-pack` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-locale-pack)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-locale-pack) |

---

## 📥 How to Install Plugins via `dsh plugin`

All plugins in this repository follow the DeepSeek Harness official bundle manifest and can be managed directly via the `dsh plugin` CLI:

### 1. Install from npm
```bash
# Install to default profile
dsh plugin add @anarkhgatsby/deepseek-harness-insights

# Or install to a specific profile
dsh plugin --profile demo add @anarkhgatsby/deepseek-harness-channel-feishu
```

### 2. Start DeepSeek Harness
```bash
dsh --profile demo
```

### 3. Uninstall a Plugin
```bash
dsh plugin --profile demo remove @anarkhgatsby/deepseek-harness-insights
```

### 4. Install from Local Source (Development)
```bash
dsh plugin --profile demo add ./packages/harness-insights
```

---

## ⚙️ Plugin Configuration & Usage

### 1. Feishu / Lark Channel Configuration
Once installed, open the **Settings ➔ Channel Config** tab in Harness UI or configure via YAML:
```yaml
"@anarkhgatsby/deepseek-harness-channel-feishu":
  appId: "cli_a1b2c3d4e5f6"
  appSecret: "your_app_secret_here"
  encryptKey: ""
  verificationToken: ""
  connectionMode: "websocket" # WebSocket mode avoids needing a public IP/Webhook
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
* Open your DeepSeek Harness web interface or desktop window;
* Click the **📊 Usage Insights** entry in the settings menu;
* Explore real-time token metrics, cost forecasts, session distributions, and tool call traces.

### 4. Multi-Language Pack (Locale Pack)
* Go to **Settings ➔ General ➔ Language (界面语言)**;
* Select from expanded options: Tibetan (བོད་ཡིག), Uyghur (ئۇيغۇرچە), Mongolian (Монгол хэл), Nuosu Yi (ꆈꌠ꒿), Traditional Chinese (繁體中文), Japanese (日本語), Korean (한국어), etc.

---

## 🛠️ Monorepo Local Development & Publishing

This repository uses **pnpm Workspaces** and **Changesets** for modular multi-package development.

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

### 3. Record Version Changes (Changeset)
```bash
pnpm changeset
```

### 4. Release to npm
```bash
# Bump version and generate changelogs
pnpm version:packages

# Publish updated packages to npm
pnpm publish:packages
```

For full plugin authoring details, see [docs/plugin-development-guide.md](./docs/plugin-development-guide.md).

---

## 📄 License

All plugins in this repository are licensed under the [MIT License](./LICENSE).

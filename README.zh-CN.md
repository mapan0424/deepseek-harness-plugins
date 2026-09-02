# 🧩 DeepSeek Harness Plugins (非官方社区插件库)

[English](README.md) | [简体中文](README.zh-CN.md)

[![CI](https://github.com/mapan0424/deepseek-harness-plugins/actions/workflows/ci.yml/badge.svg)](https://github.com/mapan0424/deepseek-harness-plugins/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![pnpm workspace](https://img.shields.io/badge/pnpm-workspace-orange.svg)](https://pnpm.io/workspaces)

面向 **DeepSeek Harness**（支持 Web 端、Docker 容器部署与 macOS/Windows 桌面端）的**非官方社区开源插件 Monorepo 大本营**。

> ⚠️ **非官方声明**：本项目由开源社区独立开发与维护，**不是 DeepSeek 官方产品**，未经 DeepSeek 官方赞助、认可或背书，亦不代表与 DeepSeek 存在隶属关系。

---

## 📑 目录

- [📦 社区插件矩阵目录](#-社区插件矩阵目录)
  - [1. 核心底座与配置 (Core & Config)](#1-核心底座与配置-core--config)
  - [2. 即时通讯与协同渠道 (Messaging Channels)](#2-即时通讯与协同渠道-messaging-channels)
  - [3. 数据分析与用量看板 (Analytics & Insights)](#3-数据分析与用量看板-analytics--insights)
  - [4. 界面增强与多语言包 (UI & Locales)](#4-界面增强与多语言包-ui--locales)
- [📥 插件安装与卸载指南 (`dsh plugin`)](#-插件安装与卸载指南-dsh-plugin)
- [⚙️ 各插件配置与使用示例](#️-各插件配置与使用示例)
- [🛠️ 本地开发与发包指南](#️-本地开发与发包指南)
- [📄 开源协议](#-开源协议)

---

## 📦 社区插件矩阵目录

### 1. 核心底座与配置 (Core & Config)

| 插件包名 | 最新版本 | 功能说明 | 安装命令 (`dsh plugin`) | npm 页面 |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-core`** | `0.1.0` | 统一 `GatewayCore` 消息总线路由中枢，负责消息去重、会话分发与渠道底层适配。 | `dsh plugin add @anarkhgatsby/deepseek-harness-core` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-core)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-core) |
| **`@anarkhgatsby/deepseek-harness-channel-config`** | `0.1.4` | 渠道可视化设置中心前端 UI，支持飞书/企微/iMessage 运行时参数在线配置与热重载。 | `dsh plugin add @anarkhgatsby/deepseek-harness-channel-config` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-config)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config) |

---

### 2. 即时通讯与协同渠道 (Messaging Channels)

| 插件包名 | 最新版本 | 功能说明 | 安装命令 (`dsh plugin`) | npm 页面 |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-channel-feishu`** | `0.1.0` | 飞书 / Lark 机器人渠道（支持 WebSocket 长连接免公网 IP、富文本/卡片/打字机流式输出）。 | `dsh plugin add @anarkhgatsby/deepseek-harness-channel-feishu` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-feishu)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-feishu) |
| **`@anarkhgatsby/deepseek-harness-channel-wecom`** | `0.1.1` | 企业微信应用及自建机器人接入渠道。 | `dsh plugin add @anarkhgatsby/deepseek-harness-channel-wecom` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-wecom)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-wecom) |
| **`@anarkhgatsby/deepseek-harness-channel-imessage`** | `0.1.1` | macOS 本地原生 iMessage 消息通道（直连 Messages.app 与本地 SQLite 数据库）。 | `dsh plugin add @anarkhgatsby/deepseek-harness-channel-imessage` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-imessage)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage) |

---

### 3. 数据分析与用量看板 (Analytics & Insights)

| 插件包名 | 最新版本 | 功能说明 | 安装命令 (`dsh plugin`) | npm 页面 |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-insights`** | `0.1.4` | 本地优先用量洞察面板：Token 消耗走势、模型花费分布、对话活动热力图与工具调用审计。 | `dsh plugin add @anarkhgatsby/deepseek-harness-insights` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-insights)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-insights) |

---

### 4. 界面增强与多语言包 (UI & Locales)

| 插件包名 | 最新版本 | 功能说明 | 安装命令 (`dsh plugin`) | npm 页面 |
| :--- | :---: | :--- | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-locale-pack`** | `0.1.1` | 多语言与民族语言包：支持藏文、维吾尔文、蒙古文、彝文、繁体中文、日文、韩文等。 | `dsh plugin add @anarkhgatsby/deepseek-harness-locale-pack` | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-locale-pack)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-locale-pack) |

---

## 📥 插件安装与卸载指南 (`dsh plugin`)

所有插件遵循 DeepSeek Harness 官方 bundle manifest 规范，可通过官方 `dsh plugin` CLI 命令直接管理：

### 1. 从 npm 在线安装
```bash
# 安装到当前默认 profile
dsh plugin add @anarkhgatsby/deepseek-harness-insights

# 或者安装到指定 profile
dsh plugin --profile demo add @anarkhgatsby/deepseek-harness-channel-feishu
```

### 2. 启动 Harness 生效
```bash
dsh --profile demo
```

### 3. 卸载/移除插件
```bash
dsh plugin --profile demo remove @anarkhgatsby/deepseek-harness-insights
```

### 4. 从本地源码目录安装（开发调试）
```bash
dsh plugin --profile demo add ./packages/harness-insights
```

---

## ⚙️ 各插件配置与使用示例

### 1. 飞书 / Lark 机器人配置
安装后可在前端 **设置 ➔ 渠道配置** 页面直接输入，或在配置中写入：
```yaml
"@anarkhgatsby/deepseek-harness-channel-feishu":
  appId: "cli_a1b2c3d4e5f6"
  appSecret: "你的飞书AppSecret"
  encryptKey: ""
  verificationToken: ""
  connectionMode: "websocket" # 强烈推荐：长连接模式，无需公网IP或Webhook回调
```

### 2. 企业微信配置
```yaml
"@anarkhgatsby/deepseek-harness-channel-wecom":
  corpId: "ww1234567890abcdef"
  agentId: 1000002
  secret: "你的企业微信自建应用Secret"
  token: "你的回调Token"
  encodingAesKey: "你的AESKey"
```

### 3. 用量洞察看板 (Usage Insights)
启用 `@anarkhgatsby/deepseek-harness-insights` 后：
* 打开 DeepSeek Harness 工作台页面；
* 点击设置中的 **📊 用量洞察 (Usage Insights)** 入口；
* 实时查看 Token 消耗折线图、会话消息量、模型花费与常用工具调用统计。

### 4. 多语言与民族语言包
加载 `@anarkhgatsby/deepseek-harness-locale-pack` 后：
* 进入 **设置 ➔ 通用 ➔ 界面语言 (Language)**；
* 下拉菜单中将解锁丰富语言选项：藏文 (བོད་ཡིག)、维文 (ئۇيغۇرچە)、蒙文 (Монгол хэл)、彝文 (ꆈꌠ꒿)、繁体中文 (繁體中文)、日文 (日本語)、韩文 (한국어) 等。

---

## 🛠️ 本地开发与发包指南

本项目使用 **pnpm Workspaces** 统一管理各子包依赖，并使用 **Changesets** 实现自动多包独立发包。

### 1. 克隆与安装依赖
```bash
git clone https://github.com/mapan0424/deepseek-harness-plugins.git
cd deepseek-harness-plugins
pnpm install
```

### 2. 运行测试
```bash
pnpm test
```

### 3. 记录变更日志 (Changeset)
当你修改或新增了一个插件时，在根目录下执行：
```bash
pnpm changeset
```
根据终端交互提示勾选涉及变动的插件，并选择版本升级类型（patch / minor / major）。

### 4. 自动化版本提升与发布
```bash
# 自动提升子包版本并生成 CHANGELOG.md
pnpm version:packages

# 将有版本变动的包一键发布至 npm
pnpm publish:packages
```

更详细的插件架构规范请参阅文档：[插件开发规范与指南 (docs/plugin-development-guide.md)](./docs/plugin-development-guide.md)。

---

## 📄 开源协议

本项目所有插件均遵循 [MIT License](./LICENSE) 开源协议。

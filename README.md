# 🧩 DeepSeek Harness Plugins (非官方社区插件库)

[![CI](https://github.com/mapan0424/deepseek-harness-plugins/actions/workflows/ci.yml/badge.svg)](https://github.com/mapan0424/deepseek-harness-plugins/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

面向 **DeepSeek Harness**（包含 Web 端、Docker 部署版与桌面端）的**非官方社区插件合集 (Unofficial Community Plugins Monorepo)**。

> ⚠️ **非官方声明**：本项目由第三方社区独立开发维护，**不是 DeepSeek 官方产品**，未经 DeepSeek 赞助、认可或背书，亦不代表与 DeepSeek 存在隶属关系。

---

## 📦 社区插件矩阵一览

| 插件包名 | 类型 | 最新版本 | 功能特性 | npm 页面 |
| :--- | :---: | :---: | :--- | :---: |
| **`@anarkhgatsby/deepseek-harness-core`** | ⚡ 基础设施 | `0.1.0` | 统一 GatewayCore 消息总线路由、消息去重与多渠道调度中枢 | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-core)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-core) |
| **`@anarkhgatsby/deepseek-harness-channel-config`** | 🎛️ 渠道设置中心 | `0.1.4` | 渠道配置前端 UI，支持飞书/企微/iMessage 运行时参数可视化配置 | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-config)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config) |
| **`@anarkhgatsby/deepseek-harness-channel-feishu`** | 💬 协同渠道 | `0.1.0` | 飞书 / Lark 机器人渠道（WebSocket 长连、富文本/卡片/流式打字机） | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-feishu)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-feishu) |
| **`@anarkhgatsby/deepseek-harness-channel-wecom`** | 💬 协同渠道 | `0.1.1` | 企业微信应用与自建机器人渠道集成 | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-wecom)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-wecom) |
| **`@anarkhgatsby/deepseek-harness-channel-imessage`** | 💬 本地渠道 | `0.1.1` | macOS 本地原生 iMessage 通道（读取 Messages.app 数据库与分发） | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-imessage)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage) |
| **`@anarkhgatsby/deepseek-harness-insights`** | 📊 洞察看板 | `0.1.4` | 本地优先用量统计、Token 消耗分布、对话活动热力与图表分析看板 | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-insights)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-insights) |
| **`@anarkhgatsby/deepseek-harness-locale-pack`** | 🌐 语言增强 | `0.1.1` | 多语言与民族语言包（藏文、蒙文、维文、彝文、繁中、日文、韩文等） | [![npm](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-locale-pack)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-locale-pack) |

---

## 🛠️ 本地开发与贡献指南

本项目使用 **pnpm Workspaces** + **Changesets** 驱动多包独立发布：

### 1. 安装依赖与建立软链
```bash
pnpm install
```
所有 `packages/*` 之间会自动建立软链接，修改底层插件（如 `harness-core`）上层插件即刻生效，无需繁琐的 `npm link`。

### 2. 运行测试套件
```bash
pnpm test
```

### 3. 创建版本更新记录 (Changeset)
当你修改或开发了一个插件后，在根目录下运行：
```bash
pnpm changeset
```
根据 CLI 交互提示选择有变动的插件包、选择版本升级类型（patch / minor / major）并填写更新说明。

### 4. 发布与同步到 npm
```bash
# 自动提升对应子包的版本号并生成各包 CHANGELOG.md
pnpm version:packages

# 发布有版本变动的包至 npm
pnpm publish:packages
```

---

## 📖 开发者接入指南
如需开发一个全新的 DeepSeek Harness 插件，请参阅：[插件开发规范与接入指南 (docs/plugin-development-guide.md)](./docs/plugin-development-guide.md)。

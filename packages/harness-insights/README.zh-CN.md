# `@anarkhgatsby/deepseek-harness-insights`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-insights.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-insights)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

面向 **DeepSeek Harness** 的非官方 Cordis 插件，为 Web UI 增加本地优先的「用量洞察」设置页面，不修改 Harness 上游源码。

> ⚠️ **非官方声明**：本项目由开源社区独立开发与维护，**不是 DeepSeek 官方产品**，未经官方赞助或背书。

---

## 📊 界面预览

插件会在 Harness 的设置中增加「用量洞察」页面，展示 Token 活动、模型调用、活跃会话、缓存命中率、活动统计和常用工具等信息。

* **双主题尊享调色**：
  * ☀️ **浅色模式**：经典自然翡翠绿阶梯，清新通透；
  * 🌙 **黑暗模式**：Codex 标志性深曜石夜空底色 + 高饱和霓虹电光热粉紫光阶（`#ff3388`）；
* **黄金比例热力图点阵**：方块饱满充实，2.7px 黄金呼吸感间距，消除空旷感。

![Harness Insights 用量洞察页面](https://raw.githubusercontent.com/mapan0424/deepseek-harness-plugins/main/packages/harness-insights/assets/screenshots/usage-insights-zh.png)

---

## 📥 快速安装

插件遵循 Harness 官方 bundle manifest，可以直接安装到 profile：

```bash
# 安装到默认环境
dsh plugin add @anarkhgatsby/deepseek-harness-insights

# 或安装到指定 profile
dsh plugin --profile demo add @anarkhgatsby/deepseek-harness-insights
dsh --profile demo
```

移除插件：
```bash
dsh plugin --profile demo remove @anarkhgatsby/deepseek-harness-insights
```

本地开发源码安装：
```bash
dsh plugin --profile demo add ./packages/harness-insights
```

---

## 🌟 核心功能

- 在设置中显示会话用量、模型调用、工具调用分布和活动趋势；
- 使用 Harness 官方 `session projection` 接口读取结构化元数据；
- 适配 Web UI 与桌面端（无任何架构原生二进制绑定，macOS arm64/x64、Windows 通用）；
- 不修改 DeepSeek Harness 上游任何源码。

---

## 🔒 数据边界与隐私安全

插件仅读取以下结构化会话元数据：

- `assistant/message.data.usage`
- `assistant/message.data.message.source.provider/model`
- `tool/call.data.name`
- 事件时间戳和会话 projection 标识

插件**绝不会**：
- 在浏览器中请求或保存完整对话聊天内容；
- 读取任何 API Key 或敏感凭据；
- 上传任何用量数据到第三方服务器。

---

## 📄 开源协议

遵循 [MIT License](./LICENSE) 开源协议。

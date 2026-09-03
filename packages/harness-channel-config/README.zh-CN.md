# `@anarkhgatsby/deepseek-harness-channel-config`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-config.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

面向 **DeepSeek Harness** 的即时通讯渠道可视化配置中心（支持飞书、企业微信、iMessage、钉钉、Telegram 等所有渠道）。

> ⚠️ **非官方声明**：本项目由开源社区独立开发与维护，**不是 DeepSeek 官方产品**，未经 DeepSeek 官方赞助或背书。

---

## 🌟 核心特性

`@anarkhgatsby/deepseek-harness-channel-config` 为 DeepSeek Harness 注入了原生的图形化渠道设置面板，彻底告别繁琐的手动编辑配置文件：

* 🎛️ **零代码可视化配置**：告别底层 `cordis.patch.yml` 或 JSON 手动编辑，在 Web 界面即可完成渠道接入；
* 🔍 **智能动态渠道探测**：自动感知当前环境安装了哪些渠道插件（如飞书、企微、iMessage 等），仅展示已激活渠道的专属设置卡片，界面纯粹清爽；
* ⚡ **参数在线热重载（Hot-Reload）**：修改 App ID、Secret、Token 等参数后即时保存生效，无需重启 Harness 进程；
* 🔒 **安全敏感字段脱敏**：密码、Secret 等关键信息前端自动掩码保护，防止录屏与分享时意外泄露；
* 🎨 **深度融入 Harness 原生 UI**：完美对齐官方设计系统与组件规范，自适应深色 / 浅色主题切换。

---

## 📥 安装指南

使用 DeepSeek Harness 官方 `dsh plugin` CLI 命令安装：

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-config
```

*(说明：本插件负责提供可视化设置面板。要使用具体渠道功能，请同时安装对应的渠道插件，例如 `@anarkhgatsby/deepseek-harness-channel-feishu`)*。

---

## 🚀 完整使用步骤

### 步骤 1：安装配置面板与渠道插件
```bash
# 示例：安装配置中心 + 飞书渠道 + 企业微信渠道
dsh plugin add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin add @anarkhgatsby/deepseek-harness-channel-wecom
```

### 步骤 2：打开 Harness 设置中心
1. 启动 DeepSeek Harness 服务或打开桌面端客户端；
2. 点击侧边栏或设置中心中的 **💬 渠道配置 (Channel Config)** 标签页；
3. 在对应的飞书或企微卡片中输入 App ID 与 App Secret；
4. 点击 **保存并连接**，机器人即刻上线运行！

---

## 📄 开源协议

遵循 [MIT License](./LICENSE) 开源协议。

# `@anarkhgatsby/deepseek-harness-channel-feishu`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-feishu.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-feishu)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

面向 **DeepSeek Harness** 的飞书 / Lark 机器人渠道插件（基于官方 WebSocket 长连接与 `GatewayCore` 消息总线中枢）。

> ⚠️ **非官方声明**：本项目由开源社区独立开发与维护，**不是 DeepSeek 或飞书官方产品**，未经官方赞助或背书。

---

## 🌟 核心杀手级特性

* 🚀 **免公网 IP / 免域名 / 免配置 Webhook**：基于飞书官方长连接（WebSocket）协议，家里的 Mac/PC、局域网或云服务器内网直接连通，零网络门槛！
* ⚡ **丝滑打字机流式卡片**：大模型生成的 Token 实时流式更新飞书交互卡片，极速响应，告别漫长等待；
* 💬 **单聊与群聊 @ 机器人全支持**：支持私信 1v1 畅聊以及在飞书群组中 `@机器人` 自动识别触发与多轮上下文记忆；
* 🛡️ **智能防重与幂等底座**：依托 `@anarkhgatsby/deepseek-harness-core`，内置滑动时间窗口去重，杜绝消息重发造成的二次回答；
* 🎨 **深度 Markdown 适配**：自动转译代码高亮块、结构化表格和引用块，适配飞书移动端与桌面端。

---

## 📥 快速安装

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-feishu
```

*(强烈建议同时安装渠道配置中心插件：`dsh plugin add @anarkhgatsby/deepseek-harness-channel-config`)*。

---

## 📋 飞书开放平台 3 分钟极速配置指南

只需 5 步，即可创建专属于你的飞书 AI 智能助理：

1. 登录 **[飞书开放平台开发者后台](https://open.feishu.cn/app/)**，点击「创建企业自建应用」；
2. **开通机器人能力**：进入应用详情，点击左侧「添加应用能力」➔ 开启「机器人」；
3. **开启 WebSocket 长连接**：
   * 点击左侧「事件与回调」➔「事件配置」；
   * 在接收方式中勾选 **「使用长连接接收事件 (WebSocket)」**（无需填写任何公网 URL 请求网址）；
   * 添加事件：`im.message.receive_v1`（接收消息）；
4. **开通必要权限**：
   * 点击左侧「权限管理」；
   * 开通 `im:message`（读取与发送单聊/群聊消息）、`im:chat`（获取群信息）；
5. **发布应用版本**：
   * 点击左侧「版本管理与发布」➔「创建版本」，提交审核并发布生效；
6. **获取凭据**：
   * 在「凭证与基础信息」中复制 `App ID`（形如 `cli_...`）和 `App Secret`。

---

## ⚙️ 接入与运行配置

### 方式 1：通过可视化渠道配置面板（推荐）
启动 DeepSeek Harness 后，打开 **设置 ➔ 渠道配置** 页面，在飞书卡片中填入 `App ID` 和 `App Secret`，点击保存即可实时上线！

### 方式 2：配置文件方式
```yaml
"@anarkhgatsby/deepseek-harness-channel-feishu":
  appId: "cli_a1b2c3d4e5f6"
  appSecret: "你的AppSecret"
  encryptKey: ""
  verificationToken: ""
  connectionMode: "websocket"
```

---

## 📄 开源协议

遵循 [MIT License](./LICENSE) 开源协议。

# `@anarkhgatsby/deepseek-harness-core`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-core.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-core)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

DeepSeek Harness 渠道生态的核心消息总线中枢与 **GatewayCore 底座**（由飞书、企业微信、iMessage、钉钉、Telegram 等所有渠道插件共享）。

> ⚠️ **非官方声明**：本项目由开源社区独立开发与维护，**不是 DeepSeek 官方产品**，未经 DeepSeek 官方赞助或背书。

---

## 🌟 核心特性与架构

`@anarkhgatsby/deepseek-harness-core` 抹平了各大即时通讯平台的协议差异，提供统一标准化的生命周期管理：

* 🔄 **统一 `GatewayCore` 会话路由**：抽象统一会话模型、消息接收/回复管道，统一多端打字机效果与流式输出；
* 🛡️ **智能消息防重与幂等（Deduplication）**：内置滑动时间窗口去重，彻底解决网络抖动与 Webhook 回调重试导致的大模型重复响应问题；
* ⚡ **多端自适应渲染转换**：自动将大模型 Markdown 输出转译为目标平台的专属富文本格式或互动卡片；
* 🎛️ **极简适配层**：新渠道开发者只需继承 `GatewayCore`，百行代码内即可完成全新即时通讯软件的接入。

---

## 📥 安装与引入

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-core
```

*(说明：当用户安装具体渠道插件如 `@anarkhgatsby/deepseek-harness-channel-feishu` 时，该包会自动作为底层依赖被加载)*。

---

## 🛠️ 渠道插件开发者接入示例

如果你想为 DeepSeek Harness 开发一个全新的自定义即时通讯渠道：

```javascript
import { Context, Schema } from '@deepseek-ai/cordis'
import { GatewayCore } from '@anarkhgatsby/deepseek-harness-core'

export const name = 'my-custom-channel'

export function apply(ctx) {
  // 初始化统一 GatewayCore 消息中枢
  const gateway = new GatewayCore(ctx, {
    channelId: 'my-custom-channel',
    dedupTtlMs: 60000,
  })

  // 监听来自三方平台的输入事件
  gateway.onIncomingMessage(async ({ senderId, text, reply }) => {
    const session = await gateway.createOrGetSession(senderId)
    const stream = await session.prompt(text)
    
    for await (const chunk of stream) {
      await reply.sendChunk(chunk)
    }
  })
}
```

---

## 📄 开源协议

遵循 [MIT License](./LICENSE) 开源协议。

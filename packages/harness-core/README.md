# `@anarkhgatsby/deepseek-harness-core`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-core.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-core)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

The shared message bus and unified **GatewayCore** routing hub for **DeepSeek Harness** channel plugins (Feishu / WeCom / iMessage / Telegram / DingTalk, etc.).

> ⚠️ **Unofficial Disclaimer**: This project is developed and maintained independently by the open-source community. It is **NOT** an official DeepSeek product.

---

## 🌟 Key Architecture & Features

`@anarkhgatsby/deepseek-harness-core` provides the foundational transport layer for all messaging channels in DeepSeek Harness:

* 🔄 **Unified `GatewayCore` Routing**: Normalizes platform-specific message events into a single standardized streaming interface.
* 🛡️ **Intelligent Deduplication**: Built-in sliding window message deduplication to prevent duplicate triggers from webhook retries and network reconnects.
* ⚡ **Streaming & Typing Synchronization**: Automatic conversion of LLM stream tokens into platform-specific rich cards, markdown messages, or typing indicators.
* 🎛️ **Extensible Adapter Architecture**: Author a new messaging channel (e.g., Discord or Slack) with fewer than 50 lines of adapter code.

---

## 📥 Installation

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-core
```

*(Note: When you install a channel plugin like `@anarkhgatsby/deepseek-harness-channel-feishu`, this package is automatically resolved as a dependency).*

---

## 🛠️ Developer Usage Example

If you are authoring a new channel plugin for DeepSeek Harness:

```javascript
import { Context, Schema } from '@deepseek-ai/cordis'
import { GatewayCore } from '@anarkhgatsby/deepseek-harness-core'

export const name = 'my-custom-channel'

export function apply(ctx) {
  // Initialize unified GatewayCore
  const gateway = new GatewayCore(ctx, {
    channelId: 'my-custom-channel',
    dedupTtlMs: 60000,
  })

  // Handle incoming messages from your platform
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

## 📄 License

[MIT License](./LICENSE)

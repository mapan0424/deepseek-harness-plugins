# `@anarkhgatsby/deepseek-harness-channel-imessage`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-imessage.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Native local iMessage channel plugin for **DeepSeek Harness** on macOS (100% private, zero-cloud relay, direct AppleScript & SQLite integration).

> ⚠️ **Unofficial Disclaimer**: This project is developed and maintained independently by the open-source community. It is **NOT** an official DeepSeek or Apple Inc. product.

---

## 🌟 Local-First & Privacy Design

* 🔒 **100% Local & Zero Cloud Relays**: Messages never touch any third-party cloud servers or external relay proxies.
* 📖 **Native SQLite Inbound Reading**: Inbound messages are polled read-only directly from macOS `~/Library/Messages/chat.db`.
* ✉️ **Native AppleScript Outbound Dispatch**: Outbound replies are sent via macOS `/usr/bin/osascript` controlling native `Messages.app`.
* 🛡️ **Built-in Message Deduplication**: Backed by `@anarkhgatsby/deepseek-harness-core` to ensure reliable idempotent message processing.
* 🧰 **No Third-Party CLI Required**: Works directly with native macOS system components without external dependencies like `imsg` or Photon.

---

## 📥 Installation

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-imessage
```

*(Recommended: Also install `@anarkhgatsby/deepseek-harness-channel-config` for visual settings)*.

---

## 🔐 Required macOS System Permissions

Because macOS protects iMessage data with system-level privacy sandboxing, you must grant the following permissions:

1. **Full Disk Access (FDA)**:
   * Open **System Settings ➔ Privacy & Security ➔ Full Disk Access**;
   * Add and enable **DeepSeek Harness** (or your Terminal / iTerm2 if running CLI).
   * *(Required to read `~/Library/Messages/chat.db`)*.
2. **Automation Permissions**:
   * Open **System Settings ➔ Privacy & Security ➔ Automation**;
   * Under **DeepSeek Harness** (or Terminal), ensure **Messages.app** is checked.
   * *(Required for AppleScript to send outbound replies)*.

---

## ⚙️ Configuration

### Method 1: Via Visual Settings (Recommended)
Open DeepSeek Harness ➔ **Settings ➔ Channel Configuration** ➔ iMessage tab.

### Method 2: Via Configuration YAML (`~/.dsh/settings.yaml`)
```yaml
imessage:
  chatDb: "~/Library/Messages/chat.db"
  defaultWorkspace: "/Users/you/dsh/default"
  autoReply: true
  streamReplies: false
```

---

## 🛠️ Global Agent Tool (`message_imessage`)

Autonomous agents can actively send iMessage texts to phone numbers or email addresses:

```json
{
  "action": "send",
  "channel": "imessage",
  "target": "+1234567890",
  "message": "Task completed successfully! 🚀"
}
```

---

## 📄 License

[MIT License](./LICENSE)

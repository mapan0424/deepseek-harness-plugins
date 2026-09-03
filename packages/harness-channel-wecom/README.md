# `@anarkhgatsby/deepseek-harness-channel-wecom`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-wecom.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-wecom)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

WeCom (Enterprise WeChat / WeChat Work) Intelligent Bot channel plugin for **DeepSeek Harness** (powered by WebSocket long-connection and unified `GatewayCore`).

> ⚠️ **Unofficial Disclaimer**: This project is developed and maintained independently by the open-source community. It is **NOT** an official DeepSeek or Tencent WeCom product.

---

## 🌟 Key Features

* 🔌 **WebSocket Long Connection**: Outbound direct connection to `wss://openws.work.weixin.qq.com`—**no public IP, no webhook callback URL, and no encryption/decryption keys required**. Works out-of-the-box in private VPCs and local environments.
* 🔐 **Simplified Credentials**: Security handshake handled at the WSS layer—requires only `botId` and `secret`.
* 💓 **Heartbeat & Auto-Reconnect**: Built-in 30s ping keep-alive with exponential backoff reconnection (up to 10 retries).
* 📨 **Intelligent Deduplication**: `msgid`-level deduplication backed by `@anarkhgatsby/deepseek-harness-core` prevents duplicate processing upon network retry.
* 💬 **Dual Transmission Modes**:
  * **Passive Stream Reply**: Streams real-time Markdown tokens back to the chat.
  * **Active Push Notification**: Built-in `message_wecom` tool allows autonomous agents to actively message specific team members.
* ⏱️ **Fallback Window**: Automatic fallback to active push if the 6-minute streaming window expires (`errcode 846608`).

---

## 📥 Installation

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-wecom
```

*(Recommended: Also install `@anarkhgatsby/deepseek-harness-channel-config` to configure bot credentials visually in the Web UI)*.

---

## 🚀 WeCom Admin Setup (4-Minute Guide)

1. Open the **WeCom Admin Console** (`work.weixin.qq.com`) ➔ **Apps & Tools ➔ Intelligent Bots (智能机器人) ➔ Create Bot ➔ Manual Creation**.
2. Select **API Mode**.
3. Under Connection Method, choose **"Use Long Connection (使用长连接)"** *(⚠️ Do NOT choose "Set Webhook URL")*.
4. Record the generated **Bot ID** and **Secret**.
5. ⚠️ **Critical Step**: Ensure the **Visible Scope (可见范围)** includes all team members who need to interact with the bot.

---

## ⚙️ Configuration & Usage

### Method 1: Via Visual Settings (Recommended)
Open DeepSeek Harness ➔ **Settings ➔ Channel Configuration** ➔ Enter your `Bot ID` and `Secret` ➔ Click **Save & Connect**.

### Method 2: Via Configuration YAML (`~/.dsh/settings.yaml`)
```yaml
wecom:
  botId: "aibS9-XXXXXXXXXXXXXXXXXXXXXXXX"
  secret: "0Y3UNbXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
  defaultWorkspace: "/Users/you/dsh/default"
  autoReply: true
  streamReplies: true
  allowlist: [] # Empty = allow all visible members; or specify user IDs
```

Or via Environment Variables: `WECOM_BOT_ID` and `WECOM_BOT_SECRET`.

---

## 🛠️ Global Agent Tool (`message_wecom`)

Autonomous agents can actively dispatch WeCom notifications:

```json
{
  "action": "send",
  "channel": "wecom",
  "target": "UserMemberID",
  "message": "Deployment completed successfully! ✅"
}
```

---

## ❓ Troubleshooting

| Issue | Cause & Solution |
| :--- | :--- |
| `853000 invalid bot_id or secret` | Credential error. Ensure you copied credentials from the **Long Connection** page. |
| Connected but no messages received | **Check Visible Scope (可见范围)** in WeCom Admin Console. Ensure the user is within scope. |
| Repeated disconnections | Another instance is connected with the same Bot ID (WeCom enforces 1 active socket per bot). |

---

## 📄 License

[MIT License](./LICENSE)

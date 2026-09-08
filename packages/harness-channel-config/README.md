# `@anarkhgatsby/deepseek-harness-channel-config`

[简体中文](README.zh-CN.md) | [NPM](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config) | [Repository](https://github.com/mapan0424/deepseek-harness-plugins/tree/main/packages/harness-channel-config)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-config.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)

Visual channel configuration center for **DeepSeek Harness**. It adds a settings page that discovers installed community channel runtimes and exposes their credentials, workspace routing, auto-reply, and streaming controls through the Harness web UI.

> ⚠️ **Unofficial project** — independently developed and maintained by the open-source community. It is not an official DeepSeek product.

## What it provides

* **One settings surface** for Feishu/Lark, WeCom, iMessage, and DingTalk integrations.
* **Runtime-aware forms** — only channels with an installed runtime plugin are actionable.
* **Credential masking** for App Secrets, Client Secrets, Bot Secrets, and other sensitive fields.
* **Hot configuration updates** through the channel gateway remotes; saving settings does not require editing YAML by hand.
* **Status and authorization visibility** including connection state, active sessions, and iMessage macOS permission hints.
* **Workspace routing controls** for assigning a sender or conversation to a specific local workspace.

The package is a configuration UI, not a message transport. Installing it alone does not connect any channel.

## Installation

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-config
```

Install the channel runtimes you intend to use as well:

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-feishu
dsh plugin add @anarkhgatsby/deepseek-harness-channel-wecom
dsh plugin add @anarkhgatsby/deepseek-harness-channel-imessage
dsh plugin add @anarkhgatsby/deepseek-harness-channel-dingtalk
```

The exact plugin set is platform-dependent. iMessage is macOS-only; do not install or enable it on Windows.

## Quick start

1. Start DeepSeek Harness and open **Settings → Channel Configuration**.
2. Select an installed channel and enter its platform credentials.
3. Set the default workspace and optional per-sender routes.
4. Choose whether to enable automatic replies, streaming output, and tool activity messages.
5. Save the configuration and confirm the channel status changes to connected.

The page writes to the active Harness settings profile. It does not embed credentials in the browser bundle or transmit them to a third-party service.

## Supported fields

| Channel | Required credentials | Optional controls |
| --- | --- | --- |
| Feishu / Lark | App ID, App Secret | Verification Token, Encrypt Key, workspace, allowlist, cards, streaming |
| WeCom | Bot ID, Secret | workspace, allowlist, streaming; legacy app fields are retained for compatibility |
| iMessage | Local `chat.db` access | database path, workspace, auto-reply, streaming; requires macOS permissions |
| DingTalk | Client ID (AppKey), Client Secret | workspace, allowlist, auto-reply, streaming |

Credentials remain in the local Harness settings profile. Treat the profile directory and exported settings as sensitive data.

## Troubleshooting

* **No channel card appears:** install the corresponding runtime plugin, then refresh the settings page.
* **Saved but not connected:** verify credentials, platform bot capabilities, and the runtime log; configuration saving and platform authentication are separate steps.
* **iMessage shows authorization required:** grant Full Disk Access to DeepSeek Harness and Automation access to Messages in macOS System Settings, then restart the app.
* **DingTalk or WeCom is unavailable on Windows:** these channels require their platform credentials; iMessage is intentionally excluded from the Windows desktop bundle.

## Compatibility

The `0.1.7` line targets the DeepSeek Harness `0.1.2-rc.1` client runtime family. Channel configuration is most useful when the UI package and channel runtimes are installed into the same profile.

## License

[MIT License](./LICENSE)

# `@anarkhgatsby/deepseek-harness-channel-imessage`

[简体中文](README.zh-CN.md) | [NPM](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage) | [Repository](https://github.com/mapan0424/deepseek-harness-plugins/tree/main/packages/harness-channel-imessage)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-imessage.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)

Native local iMessage channel plugin for **DeepSeek Harness**. It uses macOS `Messages.app` and the local `chat.db` database, without the `imsg` CLI, Photon, or any cloud relay.

> ⚠️ **Unofficial project** — independently developed and maintained by the open-source community. It is not an official DeepSeek or Apple product.

## Platform and installation

This plugin is macOS-only. Windows desktop bundles intentionally exclude iMessage because Windows has no Messages.app or AppleScript transport.

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-imessage
dsh plugin add @anarkhgatsby/deepseek-harness-channel-config
```

The configuration package is optional. The shared `@anarkhgatsby/deepseek-harness-core` package is resolved as a dependency.

## 隐私设计

- 消息数据不经过第三方云服务。
- 入站消息从 `~/Library/Messages/chat.db` 只读轮询。
- 出站消息通过 macOS `/usr/bin/osascript` 控制 `Messages.app` 发送。
- 不需要安装额外的 CLI，也不需要配置云端 API Key。
- 需要为 DeepSeek Harness 授予“完全磁盘访问”和“自动化 → 信息”权限。

## 架构

```
Harness Agent
     │
     ▼
Cordis 通道插件（host: index.js）
     │
     ▼
GatewayCore（来自 @anarkhgatsby/deepseek-harness-core）
     │  统一消息总线：路由 / 去重 / 投递 / 流式回复
     ▼
LocalAdapter
     ├── chat.db：读取入站消息
     └── Messages.app：发送出站消息
```

## Configuration

The plugin keeps `local` as a compatibility marker; it is currently the only supported mode. The configuration page exposes:

- `chatDb`: Messages database path, defaulting to `~/Library/Messages/chat.db`
- `defaultWorkspace`: default workspace path
- `autoReply`, `streamReplies`, and `toolCallReplies`
- `allowlist` and `routes` for sender access and workspace routing

The `imessage` settings namespace can also be configured in YAML. Prefer an absolute path when overriding `chatDb`:

```yaml
imessage:
  mode: "local"
  chatDb: "/Users/you/Library/Messages/chat.db"
  defaultWorkspace: "/Users/you/dsh/default"
  autoReply: true
  streamReplies: true
  toolCallReplies: true
  allowlist: []
  routes: {}
```

Defaults can be overridden during local development with `IMSG_CHAT_DB` and `IMSG_DEFAULT_WORKSPACE`. Incoming messages are routed by sender to the selected workspace and then delivered to the Harness Agent.

## Outbound message formatting

Messages.app sends plain text, so the adapter applies a small readability pass before delivering an iMessage reply:

- Markdown emphasis, strikethrough, and inline-code markers are removed;
- headings become plain-text headings;
- unordered lists use `•` bullets;
- Markdown links keep both their label and URL;
- fenced code blocks are rendered under a `代码：` label with indentation preserved.

This conversion is limited to iMessage outbound messages. Web, Feishu, DingTalk, and other rich-text-capable channels keep their existing rendering behavior.

## Approvals and agent questions

For an Agent session created from iMessage, sandbox or tool permission requests are sent to the same Messages conversation:

* Reply `1` to approve once.
* Reply `2` or any other non-approval text to reject.
* For `userQuestions`, reply with the displayed option number; separate multiple selections with commas.

Requests from desktop GUI sessions continue to use the native Harness GUI dialog. Approval and question prompts time out if no answer is received within the runtime window.

## 代码结构

- `index.js` — 注册 `imessage` settings namespace、启动本地网关和 `message_imessage` 工具。
- `client.js` — 导出本地模式的客户端元数据。
- `lib/config.mjs` — 本地模式配置 schema 与归一化逻辑。
- `lib/adapters/local.mjs` — `chat.db` 监听与 `Messages.app` AppleScript 发送。
- `cordis.patch.yml` — Cordis 补丁入口。

## Troubleshooting

| Symptom | Check |
| --- | --- |
| `chat.db` cannot be opened | Grant Full Disk Access to DeepSeek Harness (or Terminal / iTerm2 when running from a shell). |
| Messages are received but replies fail | Grant Automation permission for DeepSeek Harness to control Messages.app. |
| No conversations appear | Confirm the database path, the signed-in Messages account, and that the runtime is running on macOS. |
| Approval appears as a GUI popup | The session-to-sender mapping was not recognized; inspect the Core and iMessage runtime logs. |
| Duplicate replies | Ensure only one iMessage runtime instance is watching the same `chat.db`. |

## Development

```bash
node --check index.js
node --check client.js
node --check lib/config.mjs
node --check lib/adapters/local.mjs
```

## Compatibility

The `0.1.5` line targets the DeepSeek Harness `0.1.2-rc.1` dependency family.

## License

[MIT License](./LICENSE)

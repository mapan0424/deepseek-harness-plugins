# DeepSeek Harness Plugins

[简体中文](README.zh-CN.md) | [Plugin development guide](docs/plugin-development-guide.md)

[![CI](https://github.com/mapan0424/deepseek-harness-plugins/actions/workflows/ci.yml/badge.svg)](https://github.com/mapan0424/deepseek-harness-plugins/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![pnpm workspace](https://img.shields.io/badge/pnpm-workspace-orange.svg)](https://pnpm.io/workspaces)

An independently maintained community monorepo of plugins for **DeepSeek Harness**.

> ⚠️ **Unofficial project** — this repository is developed and maintained by the open-source community. It is not an official DeepSeek product and is not sponsored, endorsed, or operated by DeepSeek.

## Overview

This repository packages the integrations that sit around the Harness runtime:

* a shared **GatewayCore** for channel-neutral routing, sessions, deduplication, and delivery;
* a visual configuration center for installed messaging channels;
* Feishu/Lark, DingTalk, WeCom, and native macOS iMessage transports;
* a local usage-insights dashboard and an extended locale pack.

Each integration is independently installable. Channel packages keep platform-specific authentication and I/O at the edge, while common session behavior remains in Core.

## Package matrix

The versions below are the versions currently represented by this source tree. The npm status column distinguishes published versions from local versions awaiting publication.

| Package | Role | Source version | npm status |
| --- | --- | :---: | --- |
| [deepseek-harness-core](packages/harness-core) | Shared gateway, sessions, routing, deduplication, approvals | 0.1.4 | [npm](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-core) |
| [deepseek-harness-channel-config](packages/harness-channel-config) | Visual configuration UI for installed channels | 0.1.7 | [npm](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-config) |
| [deepseek-harness-channel-feishu](packages/harness-channel-feishu) | Feishu / Lark WebSocket channel | 0.1.2 | [npm](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-feishu) |
| [deepseek-harness-channel-dingtalk](packages/harness-channel-dingtalk) | DingTalk Stream channel | 0.1.0 | [npm](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-dingtalk) |
| [deepseek-harness-channel-wecom](packages/harness-channel-wecom) | WeCom AI Bot WebSocket channel | 0.1.4 | [npm](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-wecom) |
| [deepseek-harness-channel-imessage](packages/harness-channel-imessage) | Native local macOS iMessage channel | 0.1.5 | [npm](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage) |
| [deepseek-harness-insights](packages/harness-insights) | Local-first usage and activity dashboard | 0.1.7 | [npm](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-insights) |
| [deepseek-harness-locale-pack](packages/harness-locale-pack) | Additional interface and minority-language locales | 0.1.4 | [npm](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-locale-pack) |

Every package directory contains an English README and a [简体中文 README](README.zh-CN.md) where applicable. The package-specific documents are the source of truth for platform credentials and configuration fields.

## Architecture

~~~text
DeepSeek Harness host
        │
        ├── channel-config ─── settings UI and runtime status
        │
        ├── GatewayCore ────── sessions, routing, deduplication, delivery
        │        │
        │        ├── Feishu / Lark adapter
        │        ├── DingTalk adapter
        │        ├── WeCom adapter
        │        └── macOS iMessage adapter
        │
        ├── insights ───────── usage projection and analytics UI
        └── locale-pack ────── additional interface locales
~~~

Channel-originated approval and userQuestions requests are routed back to the originating conversation when the channel supports it. Sessions created from the Harness desktop UI continue to use the native GUI flow.

## Installation

Install only the packages you need into the active Harness profile:

~~~bash
dsh plugin add @anarkhgatsby/deepseek-harness-core
dsh plugin add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin add @anarkhgatsby/deepseek-harness-channel-feishu
~~~

For a named profile:

~~~bash
dsh plugin --profile work add @anarkhgatsby/deepseek-harness-channel-config
dsh plugin --profile work add @anarkhgatsby/deepseek-harness-channel-feishu
dsh --profile work
~~~

Most channel packages resolve deepseek-harness-core as a dependency. Installing the configuration center alone does not connect a channel; install the corresponding runtime package and configure its credentials.

### Platform notes

* Feishu/Lark, DingTalk, and WeCom use their respective platform credentials and network transports.
* iMessage is **macOS-only**. It reads the local Messages database and sends through Messages.app; Windows desktop bundles intentionally exclude it.
* Native iMessage use requires Full Disk Access and Automation permission for the Harness host to access Messages.app.
* Keep credentials in the local Harness profile or environment variables. Never commit secrets to this repository.

## Configuration examples

The optional configuration package exposes the same settings through the Harness UI. The following namespaces can also be configured in the active profile:

~~~yaml
feishu:
  appId: "cli_xxxxxxxxx"
  appSecret: "replace-me"
  defaultWorkspace: "/Users/you/dsh/workspace"
  autoReply: true
  streamReplies: true

dingtalk:
  appKey: "dingxxxxxxxx"
  appSecret: "replace-me"
  defaultWorkspace: "/Users/you/dsh/workspace"

imessage:
  mode: "local"
  chatDb: "/Users/you/Library/Messages/chat.db"
  defaultWorkspace: "/Users/you/dsh/workspace"
  autoReply: true
~~~

See the channel README before configuring production credentials:

* [Feishu / Lark](packages/harness-channel-feishu/README.md)
* [DingTalk](packages/harness-channel-dingtalk/README.md)
* [WeCom](packages/harness-channel-wecom/README.md)
* [native iMessage](packages/harness-channel-imessage/README.md)
* [visual configuration](packages/harness-channel-config/README.md)

## Development

~~~bash
git clone https://github.com/mapan0424/deepseek-harness-plugins.git
cd deepseek-harness-plugins
pnpm install
pnpm test
~~~

The workspace uses pnpm and Changesets. Package-local checks can be run directly, for example:

~~~bash
node --check packages/harness-channel-dingtalk/index.js
node --check packages/harness-channel-imessage/lib/adapters/local.mjs
~~~

### Release workflow

1. Make the package change and add a Changeset with pnpm changeset.
2. Review the generated version and changelog with pnpm version:packages.
3. Verify the package tarball with npm pack --dry-run from the package directory.
4. Publish only the packages with an intentional version change using pnpm publish:packages or the package-local npm command.

Publishing may require npm account 2FA. A package is not publicly installable until the publish command completes successfully and the version appears on npm.

## Documentation

* [Plugin development guide](docs/plugin-development-guide.md)
* [Core runtime](packages/harness-core/README.md)
* [Usage Insights](packages/harness-insights/README.md)
* [Locale pack](packages/harness-locale-pack/README.md)

## License

All packages in this repository are released under the [MIT License](LICENSE), unless a package directory states otherwise.

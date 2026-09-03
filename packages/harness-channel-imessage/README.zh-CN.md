# `@anarkhgatsby/deepseek-harness-channel-imessage`

[English](README.md) | [简体中文](README.zh-CN.md)

[![npm version](https://img.shields.io/npm/v/@anarkhgatsby/deepseek-harness-channel-imessage.svg)](https://www.npmjs.com/package/@anarkhgatsby/deepseek-harness-channel-imessage)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

DeepSeek Harness 的 macOS 本地原生 iMessage 通道插件（100% 本地隐私安全、直连 Messages.app 与 SQLite 数据库，零云端中继）。

> ⚠️ **非官方声明**：本项目由开源社区独立开发与维护，**不是 DeepSeek 或 Apple 官方产品**，未经官方赞助或背书。

---

## 🌟 隐私优先设计与核心特性

* 🔒 **100% 本地安全，零云端中继**：所有对话数据完全在本地处理，绝不经过任何第三方云服务或外网转发中继；
* 📖 **原生 SQLite 只读入站读取**：入站消息直接从本地 `~/Library/Messages/chat.db` 只读轮询；
* ✉️ **原生 AppleScript 出站调度**：出站回复通过 macOS 系统自带的 `/usr/bin/osascript` 驱动 `Messages.app` 极速发送；
* 🛡️ **依托 `GatewayCore` 消息总线**：自带会话管理、自动回复与智能防重机制；
* 🧰 **免装任何第三方 CLI**：无需安装 `imsg` CLI 或 Photon，纯原生能力实现。

---

## 📥 快速安装

```bash
dsh plugin add @anarkhgatsby/deepseek-harness-channel-imessage
```

*(强烈建议同时安装可视化配置中心：`dsh plugin add @anarkhgatsby/deepseek-harness-channel-config`)*。

---

## 🔐 必需的 macOS 系统权限配置

由于 macOS 系统对 iMessage 隐私数据有严格的系统沙盒保护，初次使用必须开启以下两项系统权限：

1. **完全磁盘访问权限 (Full Disk Access)**：
   * 打开 **系统设置 ➔ 隐私与安全性 ➔ 完全磁盘访问权限**；
   * 点击 `+` 号添加并开启 **DeepSeek Harness**（如果通过终端命令行运行，请添加 **终端 / iTerm2**）；
   * *（此权限用于读取本地 `~/Library/Messages/chat.db` 消息数据库）*。
2. **自动化权限 (Automation)**：
   * 打开 **系统设置 ➔ 隐私与安全性 ➔ 自动化**；
   * 在 **DeepSeek Harness** 或终端下方，勾选允许控制 **「信息 (Messages)」**；
   * *（此权限用于通过 AppleScript 发送出站回复）*。

---

## ⚙️ 接入与配置

### 方式 1：通过可视化渠道配置面板（推荐）
启动 DeepSeek Harness 后，打开 **设置 ➔ 渠道配置** 页面，在 iMessage 卡片中开启自动回复并配置默认工作区即可。

### 方式 2：配置文件方式 (`~/.dsh/settings.yaml`)
```yaml
imessage:
  chatDb: "~/Library/Messages/chat.db"           # 默认数据库路径
  defaultWorkspace: "/Users/you/dsh/default"     # 默认工作区
  autoReply: true
  streamReplies: false
```

---

## 🛠️ 全局主动推送工具 (`message_imessage`)

插件注册了 `message_imessage` 工具，AI Agent 在执行完后台任务后可主动向指定手机号或 Apple ID 发送 iMessage：

```json
{
  "action": "send",
  "channel": "imessage",
  "target": "+8613800000000",
  "message": "构建与测试已全部完成 🚀"
}
```

---

## 📄 开源协议

遵循 [MIT License](./LICENSE) 开源协议。

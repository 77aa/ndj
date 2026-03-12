# OpenClaw 项目介绍

> 参考项目：[https://github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)

## 简介

**OpenClaw** 是一个**个人 AI 助手**，可在你自己的设备上运行。它的口号是 "The lobster way. 🦞"，支持在你日常使用的各类即时通讯平台上收发消息，无需将数据上传至第三方云端，真正实现本地优先、隐私可控。

- **GitHub**：[openclaw/openclaw](https://github.com/openclaw/openclaw)
- **官网**：[https://openclaw.ai](https://openclaw.ai)
- **文档**：[https://docs.openclaw.ai](https://docs.openclaw.ai)
- **协议**：MIT
- **主要语言**：TypeScript
- **Stars**：307k+（截至 2026 年 3 月）

---

## 核心特性

| 特性 | 说明 |
|------|------|
| 本地优先网关 | 在本地运行 Gateway（控制平面），统一管理会话、频道、工具和事件 |
| 多平台消息收发 | 支持 WhatsApp、Telegram、Slack、Discord、Google Chat、Signal、iMessage、Matrix、微信（Feishu/飞书）、LINE 等 20+ 平台 |
| 语音唤醒与对话 | 支持 macOS/iOS 上的唤醒词，以及 Android 上的连续语音对话（ElevenLabs + 系统 TTS） |
| 实时画布（Canvas） | 代理驱动的可视化工作区，支持 A2UI 协议 |
| 技能（Skills）平台 | 向导式安装内置/托管/工作区技能，可扩展 AI 能力 |
| 多代理路由 | 将不同频道/账号路由到独立代理（隔离工作区与会话） |
| 浏览器控制 | 内置浏览器控制能力，支持快照、操作、上传、配置文件 |
| 定时任务与 Webhook | 支持 Cron 定时任务、Webhook、Gmail Pub/Sub 自动化 |
| 伴侣应用 | macOS 菜单栏应用 + iOS/Android 节点应用 |

---

## 快速上手

**运行环境要求：Node.js ≥ 22**

```bash
# 全局安装
npm install -g openclaw@latest

# 运行向导，自动安装守护进程（launchd/systemd）
openclaw onboard --install-daemon

# 启动网关
openclaw gateway --port 18789 --verbose

# 向助手发送消息
openclaw agent --message "你好，OpenClaw" --thinking high
```

---

## 架构概览

```
WhatsApp / Telegram / Slack / Discord / Signal / iMessage / Matrix / ...
                │
                ▼
┌───────────────────────────────┐
│            Gateway            │  ← 本地控制平面
│       ws://127.0.0.1:18789    │
└──────────────┬────────────────┘
               │
               ├─ AI 代理（RPC 模式）
               ├─ CLI（openclaw …）
               ├─ WebChat UI
               ├─ macOS 菜单栏应用
               └─ iOS / Android 节点
```

---

## 支持的消息平台

WhatsApp · Telegram · Slack · Discord · Google Chat · Signal · iMessage (BlueBubbles) · IRC · Microsoft Teams · Matrix · 飞书 (Feishu) · LINE · Mattermost · Nextcloud Talk · Nostr · Synology Chat · Tlon · Twitch · Zalo · WebChat

---

## 安全说明

OpenClaw 默认启用 **DM 配对策略**（`dmPolicy="pairing"`）：未知发件人需完成配对才能与助手通信，有效防止未经授权访问。可通过以下命令批准配对：

```bash
openclaw pairing approve <channel> <code>
```

运行 `openclaw doctor` 可检测并修复不安全的 DM 策略配置。

---

## 从源码构建

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw

pnpm install
pnpm ui:build
pnpm build

pnpm openclaw onboard --install-daemon

# 开发模式（TS 变更自动重载）
pnpm gateway:watch
```

---

## 相关链接

- [快速入门指南](https://docs.openclaw.ai/start/getting-started)
- [更新说明](https://docs.openclaw.ai/install/updating)
- [安全文档](https://docs.openclaw.ai/gateway/security)
- [常见问题 (FAQ)](https://docs.openclaw.ai/help/faq)
- [Discord 社区](https://discord.gg/clawd)
- [DeepWiki 文档](https://deepwiki.com/openclaw/openclaw)

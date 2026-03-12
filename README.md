# OpenClaw 项目介绍

> 项目地址：https://github.com/openclaw/openclaw

## 简介

**OpenClaw**（🦞）是一款**个人 AI 助手**，可以运行在你自己的设备上。它通过你日常使用的各种即时通讯渠道与你交互，并能真正地在计算机上执行任务。

## 核心特点

- **本地优先（Local-first）**：助手运行在你自己的设备上，数据不经过第三方云服务，注重隐私保护。
- **多渠道支持**：支持 WhatsApp、Telegram、Slack、Discord、Google Chat、Signal、iMessage、BlueBubbles、IRC、Microsoft Teams、Matrix、飞书、LINE、Mattermost、Nextcloud Talk、Nostr、Synology Chat、Tlon、Twitch、Zalo、WebChat 等众多主流通讯平台。
- **语音交互**：在 macOS/iOS 上支持语音唤醒词，在 Android 上支持持续语音模式（需要 ElevenLabs 或系统 TTS）。
- **多模型支持**：兼容 OpenAI、以及众多其他主流 AI 模型提供商，支持模型故障转移与 API Key 轮换。
- **可扩展插件体系**：通过 npm 包方式分发插件，支持本地插件加载；同时提供 MCP（模型上下文协议）集成（通过 mcporter 桥接）。
- **自动化能力**：内置定时任务（Cron）、Webhook、Gmail Pub/Sub 等自动化触发方式。
- **浏览器控制**：可驱动专属 Chrome/Chromium 完成网页浏览、截图、交互等操作。
- **伴侣 App**：提供 macOS 菜单栏 App、iOS/Android 节点 App，支持摄像头、屏幕录制、位置获取、通知等设备能力。
- **实时画布（Live Canvas）**：AI 驱动的可视化工作空间，通过 A2UI 协议实时推送 UI 内容。

## 架构概览

```
WhatsApp / Telegram / Slack / Discord / … （各通讯渠道）
               │
               ▼
┌─────────────────────────────────┐
│           Gateway（网关）        │
│         控制平面 / 路由          │
│      ws://127.0.0.1:18789       │
└──────────────┬──────────────────┘
               │
               ├─ Pi agent（RPC 模式，工具调用 + 流式输出）
               ├─ CLI（openclaw 命令行）
               ├─ WebChat UI
               ├─ macOS App
               └─ iOS / Android 节点
```

网关（Gateway）是整个系统的控制平面，负责管理会话、渠道、工具调用和事件分发。

## 安全机制

- **DM 配对（Pairing）**：默认情况下，陌生发送者会收到一个配对码，助手不会处理其消息，需要管理员审批后才能加入白名单。
- **安全默认值**：强默认配置，同时暴露可控的开关供信任的高权限工作流使用。
- 可通过 `openclaw doctor` 命令检查并发现潜在的安全风险配置。

## 快速开始

```bash
# 安装（需要 Node.js >= 22）
npm install -g openclaw@latest

# 启动引导向导
openclaw onboard --install-daemon

# 启动网关
openclaw gateway --port 18789 --verbose

# 与助手对话（--thinking high 表示使用深度推理模式）
openclaw agent --message "帮我整理今日待办" --thinking high
```

## 技术栈

- **语言**：TypeScript（便于二次开发和扩展）
- **包管理**：pnpm（推荐）/ npm / bun
- **运行时**：Node.js >= 22
- **部署方式**：本地守护进程（launchd/systemd）、Docker、Nix

## 相关链接

- 官网：https://openclaw.ai
- 文档：https://docs.openclaw.ai
- 项目愿景：[VISION.md](https://github.com/openclaw/openclaw/blob/main/VISION.md)
- Discord 社区：https://discord.gg/clawd
- MIT 开源协议

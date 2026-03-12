# OpenClaw 项目介绍

## 项目概述

**OpenClaw**（https://github.com/openclaw/openclaw）是一个**个人 AI 助手**，可以运行在你自己的设备上。它能够在你日常使用的各种通讯平台上与你互动，支持语音对话，并可在 macOS/iOS/Android 上运行。

> OpenClaw is a personal AI assistant you run on your own devices.

---

## 核心特性

### 多平台消息支持
OpenClaw 支持接入几乎所有主流的即时通讯平台，包括：

- **国际平台**：WhatsApp、Telegram、Slack、Discord、Signal、iMessage、Microsoft Teams、Google Chat、Matrix、IRC、LINE、Twitch、Nostr、Zalo
- **国内平台**：飞书（Feishu）
- **其他**：Mattermost、Nextcloud Talk、Synology Chat、Tlon、BlueBubbles、WebChat 等

### 语音能力
- **语音唤醒（Voice Wake）**：支持 macOS/iOS 上的唤醒词功能
- **持续对话模式（Talk Mode）**：支持 Android 上的持续语音交互
- 集成 ElevenLabs TTS 及系统 TTS 作为备选

### 本地优先架构（Local-first Gateway）
- 单一控制平面，统一管理会话、频道、工具和事件
- Gateway 作为控制层，以守护进程（launchd/systemd）方式常驻运行
- 支持多智能体路由（Multi-agent routing），可将不同频道/账户路由到独立的 Agent 工作空间

### 实时画布（Live Canvas）
- Agent 驱动的可视化工作区
- 支持 A2UI（Agent-to-UI）交互

### 工具与技能
- 内置浏览器、画布、定时任务（Cron）、会话管理等工具
- 支持自定义技能（Skills）扩展
- 向导式安装与配置（`openclaw onboard`）

---

## 支持的 AI 模型

OpenClaw 支持多种 AI 模型提供商，包括：
- **OpenAI**（ChatGPT/Codex）
- 以及其他多种模型提供商

支持 OAuth 订阅与 API Key 两种认证方式，并提供模型故障转移（Model Failover）机制。

---

## 快速开始

### 环境要求
- Node.js ≥ 22

### 安装

```bash
npm install -g openclaw@latest
# 或者使用 pnpm
pnpm add -g openclaw@latest

# 启动安装向导（推荐）
openclaw onboard --install-daemon
```

### 从源码构建

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

## 安全说明

OpenClaw 连接到真实的消息平台，默认对入站私信采用**配对验证（DM pairing）**策略：

- 未知发件人会收到一个配对码，Bot 不会处理其消息
- 使用 `openclaw pairing approve <channel> <code>` 批准后，发件人会被加入本地白名单
- 公开入站私信需要显式启用 `dmPolicy='open'` 并配置白名单

运行 `openclaw doctor` 可检查并发现潜在的安全配置问题。

---

## 赞助商

OpenClaw 得到以下公司的赞助支持：

- [OpenAI](https://openai.com/)
- [Vercel](https://vercel.com/)
- [Blacksmith](https://blacksmith.sh/)
- [Convex](https://www.convex.dev/)

---

## 相关资源

| 资源 | 链接 |
|------|------|
| 官方网站 | https://openclaw.ai |
| 文档 | https://docs.openclaw.ai |
| 快速入门 | https://docs.openclaw.ai/start/getting-started |
| FAQ | https://docs.openclaw.ai/help/faq |
| Discord 社区 | https://discord.gg/clawd |
| GitHub 仓库 | https://github.com/openclaw/openclaw |
| Docker 安装 | https://docs.openclaw.ai/install/docker |

---

## 许可证

OpenClaw 采用 **MIT 许可证**开源发布。

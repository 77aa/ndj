# 扭蛋机固件 (Capsule Toy Machine Firmware)

本项目是用于扭蛋机（ガシャポン机）的 STM32 嵌入式固件，支持乐摇摇串口通信协议。

## 项目简介

**ndj** 是扭蛋机（扭蛋/ガシャポン 自动售货机）的控制器固件，基于 STM32F10x 系列微控制器开发。项目包含完整的硬件设计文件（原理图和 PCB）以及固件源代码。

## 项目结构

```
ndj/
├── niudan_V1906.sch                    # 电路原理图 (V1906)
├── niudan_V1907.pcb                    # PCB 布局文件 (V1907)
└── niudan_src_new V2.9.21.7.3 leyaoyao/  # 固件源代码 (V2.9.21.7.3)
    └── src/
        ├── main.c / main.h             # 主程序入口
        ├── game.c / game.h             # 游戏逻辑（投币、出蛋控制）
        ├── protocol.c / protocol.h     # 串口通信协议（主机协议）
        ├── leyaoyao_protocol.c/.h      # 乐摇摇第三方支付协议
        ├── usart.c / usart.h           # 串口驱动
        ├── key.c / key.h               # 按键输入
        ├── led.c / led.h               # LED 灯控制
        ├── music.c / music.h           # 音乐/音效
        ├── light_eye.c / light_eye.h   # 光眼（出蛋检测传感器）
        ├── digital_tube.c/.h           # 数码管显示
        ├── at24c64.c / at24c64.h       # EEPROM 存储驱动
        ├── timer.c / timer.h           # 定时器
        ├── clock.c / clock.h           # 时钟
        ├── delay.c / delay.h           # 延时函数
        ├── watch_dog.c / watch_dog.h   # 看门狗
        └── sys.c / sys.h               # 系统初始化
```

## 主要功能

- **投币控制**：支持多币种配置，设置每局所需硬币数
- **出蛋驱动**：电机驱动控制扭蛋出货，含超时保护与错误检测
- **光眼检测**：通过光电传感器检测扭蛋是否成功出货
- **串口通信**：支持 RS-485 总线，可接入上位机管理系统
- **乐摇摇协议**：集成乐摇摇第三方无现金支付协议（扫码/刷卡）
- **数据存储**：使用 AT24C64 EEPROM 保存运营统计数据（投币次数、出蛋次数等）
- **LED/音乐**：支持氛围灯与音效播放

## 硬件平台

- **MCU**：STM32F10x 系列（ARM Cortex-M3）
- **开发工具**：Keil MDK (μVision)
- **通信接口**：USART（串口）、I²C、RS-485

## 版本说明

最新固件版本：**V2.9.21.7.3**

主要更新（2021.7.3）：
1. 改乐摇摇串口 COM3 开漏输入为上拉输入，改善与乐摇摇新版盒子的兼容性
2. 每次上传弹仓信息为乐摇摇提供的参考信息
3. 修正将几币一局设定为 1 币一局时出现无限出蛋的 Bug

---

## 关于 OpenClaw 项目

> 本 Issue 提及了 [openclaw/openclaw](https://github.com/openclaw/openclaw) 项目，以下是该项目的简介。

**OpenClaw** 是一个运行在你自己设备上的**个人 AI 助手**，口号是 *"EXFOLIATE! EXFOLIATE!"*。

### 核心特点

- **本地优先**：运行在你自己的设备上，数据不经过第三方服务器
- **多平台消息接入**：支持 WhatsApp、Telegram、Slack、Discord、Google Chat、Signal、iMessage、BlueBubbles、IRC、Microsoft Teams、Matrix、飞书（Feishu）、LINE、Mattermost、Nextcloud Talk、Nostr、Synology Chat、Tlon、Twitch、Zalo 等主流即时通讯平台
- **语音交互**：支持 macOS / iOS / Android 上的语音唤醒与持续对话
- **Live Canvas**：支持 AI 驱动的可视化工作区（A2UI）
- **多智能体路由**：将不同频道/账户路由到隔离的 AI 工作区
- **技能系统（Skills）**：支持内置技能与自定义工作区技能扩展

### 快速安装

```bash
# 需要 Node.js >= 22
npm install -g openclaw@latest

# 启动向导（安装 Gateway 守护进程）
openclaw onboard --install-daemon
```

### 支持的 AI 模型提供商

OpenAI（ChatGPT/Codex）、Anthropic、Google、以及其他兼容 OpenAI API 的模型。

### 相关链接

- 官网：https://openclaw.ai
- 文档：https://docs.openclaw.ai
- Discord 社区：https://discord.gg/clawd
- GitHub：https://github.com/openclaw/openclaw
- 开源协议：MIT License

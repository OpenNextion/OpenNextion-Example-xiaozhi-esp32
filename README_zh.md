# OpenNextion 小智 AI 聊天机器人

([English](README.md) | [中文](README_zh.md) | [日本語](README_ja.md))

将支持的 OpenNextion ESP32-S3 触摸屏变成小智 AI 语音助手。为您的屏幕烧录对应固件，连接 Wi-Fi 后，轻触屏幕或按下 BOOT 按键即可开始对话。

<!-- MEDIA TODO — 首屏成品图或视频。建议路径：docs/images/opennextion-xiaozhi-hero.jpg
     展示已通电、装入桌面外壳的 OpenNextion 面板；建议宽度：820 px。 -->

<p align="center">
  <img src="docs/v1/OpenNextion-ONX2432G028.jpg" alt="OpenNextion ONX2432G028 2.8 寸触摸屏" width="390">
  <img src="docs/v1/OpenNextion-ONX3248G035.jpg" alt="OpenNextion ONX3248G035 3.5 寸触摸屏" width="390">
</p>

> 本项目是 [xiaozhi-esp32](https://github.com/78/xiaozhi-esp32) 的 OpenNextion 硬件适配版本，仅面向以下两款面板。

## 支持的硬件

| OpenNextion 型号 | 显示屏 | 方向 | 固件板型名称 | 状态 |
| --- | --- | --- | --- | --- |
| [ONX2432G028][onx2432g028] | 2.8 寸电容触摸屏，240 × 320 | 竖屏 | <code>OpenNextion-ONX2432G028</code> | 支持 |
| [ONX3248G035][onx3248g035] | 3.5 寸电容触摸屏，320 × 480 | 竖屏 | <code>OpenNextion-ONX3248G035</code> | 支持 |

**务必使用与面板型号完全一致的固件。ONX2432G028 与 ONX3248G035 的固件不可互刷。**

本适配支持显示、电容触摸、双麦克风、扬声器和 Wi-Fi；需连接 2.4 GHz Wi-Fi 网络。

## 开始前准备

- 上表中的一块 OpenNextion 面板。
- 一条支持数据传输的 USB 线，而不仅是充电线。
- Windows、macOS 或 Linux 电脑。
- 一个 2.4 GHz Wi-Fi 网络；ESP32-S3 无法连接仅提供 5 GHz 的网络。
- 使用默认小智服务时，需要一个 [xiaozhi.me](https://xiaozhi.me) 账号。

## 快速上手

### 1. 获取正确的固件

从项目的 [GitHub Releases](https://github.com/OpenNextion/OpenNextion-Example-xiaozhi-esp32/releases) 页面下载最新固件。当前 <code>v2.2.6</code> 的首次烧录镜像如下：

| 您的面板 | 下载文件 |
| --- | --- |
| ONX2432G028 | [<code>xiaozhi_V2.2.6_merged_ONX2432G028_en_Jarvis.bin</code>](https://github.com/OpenNextion/OpenNextion-Example-xiaozhi-esp32/releases/download/v2.2.6/xiaozhi_V2.2.6_merged_ONX2432G028_en_Jarvis.bin) |
| ONX3248G035 | [<code>xiaozhi_V2.2.6_merged_ONX3248G035_en_Jarvis.bin</code>](https://github.com/OpenNextion/OpenNextion-Example-xiaozhi-esp32/releases/download/v2.2.6/xiaozhi_V2.2.6_merged_ONX3248G035_en_Jarvis.bin) |

请根据文件名中的 <code>ONX...</code> 型号选择与您的面板一致的文件，不要使用其他小智硬件的固件。

### 2. 烧录面板

<!-- MEDIA TODO — 烧录步骤图。建议路径：docs/images/opennextion-xiaozhi-flashing.jpg
     展示面板已通过 USB 连接，且烧录工具中选中了对应型号；建议宽度：620 px。 -->

1. 使用支持数据传输的 USB 线连接面板与电脑。
2. 按照[新手烧录教程][flashing-guide]，将对应的 <code>.bin</code> 文件写入地址 <code>0x0</code>。
3. 等待烧录完成，面板会自动重启。

若电脑没有出现串口设备，请先更换 USB 线或 USB 端口；部分 USB 线只能充电。若烧录工具无法连接，请使用面板的 BOOT 和 Reset 按键进入下载模式后重试。

### 3. 配置 Wi-Fi

<!-- MEDIA TODO — Wi-Fi 配网图。建议路径：docs/images/opennextion-xiaozhi-wifi-setup.jpg
     展示 Xiaozhi-xxxx 热点和/或 http://192.168.4.1 配置页面；建议宽度：620 px。 -->

首次启动，或无法使用已保存的 Wi-Fi 时，设备会创建名为 <code>Xiaozhi-xxxx</code> 的配置热点。

1. 用手机或电脑连接 <code>Xiaozhi-xxxx</code> Wi-Fi。
2. 如果没有自动打开配置页，请访问 <http://192.168.4.1>。
3. 选择您的 2.4 GHz 家庭 Wi-Fi 并输入密码。
4. 保存设置，等待设备连接网络并继续启动。

该配置热点不设密码，请仅在可信环境中配网，并在完成后退出配置模式。

### 4. 激活并开始对话

<!-- MEDIA TODO — 激活或使用图。建议路径：docs/images/opennextion-xiaozhi-activation.jpg
     展示激活界面，或用户触摸屏幕开始对话；建议宽度：620 px。 -->

默认固件连接至 [xiaozhi.me](https://xiaozhi.me)。按屏幕提示完成激活，然后登录小智控制台管理设备和模型设置。

轻触屏幕一次，或短按 **BOOT** 按键，即可开始对话；再次执行相同操作可结束当前对话。

## 日常使用

| 想做什么 | 操作方法 |
| --- | --- |
| 开始或结束对话 | 轻触屏幕，或短按 **BOOT** 按键。 |
| 修改 AI 服务设置 | 激活后登录 [xiaozhi.me](https://xiaozhi.me) 控制台。 |
| 更换 Wi-Fi | 重启设备，在启动过程中通过 **BOOT** 按键进入配网，再完成热点配置。 |
| 恢复错误或异常的固件 | 通过 USB 为对应面板型号重新烧录完整固件包。 |
| 更新固件 | 仅使用明确标注适用于本面板型号的更新包，并遵循该版本的发布说明。 |

## 小智服务与大模型配置

设备在默认服务激活后，请登录 [xiaozhi.me](https://xiaozhi.me) 控制台管理设备及可用的大模型设置。服务选择、可用模型和账户选项由控制台管理，而非在面板固件中设置。

如需自建服务或使用其他后端，请部署兼容小智协议的服务端，并按其文档进行配置。可从以下项目开始：

- [xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server)（Python）
- [xiaozhi-esp32-server-java](https://github.com/joey-zhou/xiaozhi-esp32-server-java)（Java）
- [xiaozhi-server-go](https://github.com/AnimeAIChat/xiaozhi-server-go)（Go）

## 常见问题

### 电脑找不到面板

请使用支持数据传输的 USB 线，并尝试其他 USB 端口。若仍未出现设备，请为操作系统安装所需的 USB 串口驱动。

### 无法连接烧录

重新插拔 USB 后再试。如有必要，使用面板的 BOOT 和 Reset 按键进入下载模式后重新开始烧录。

### 无法连接 Wi-Fi

确认选择的是 2.4 GHz Wi-Fi，且密码正确。启动时按 **BOOT** 按键重新进入配网，连接 <code>Xiaozhi-xxxx</code> 热点后再次配置。

### 显示异常或触摸无响应

很可能烧录了错误固件。请通过 USB 为正确的面板型号重新烧录完整固件包；两款 OpenNextion 面板的固件不能互换。

## 外壳与图片

<!-- MEDIA TODO — 补充最终安装照片和公开的 3D 模型链接。
     建议路径：
       docs/images/onx2432g028-xiaozhi-enclosure.jpg
       docs/images/onx3248g035-xiaozhi-enclosure.jpg
     每个型号各放一张面板已装入 3D 打印外壳的斜角照片。 -->

桌面外壳照片和可下载的 3D 打印文件将在后续补充。

| 型号 | 3D 打印外壳 |
| --- | --- |
| ONX2432G028 | 链接待补充 |
| ONX3248G035 | 链接待补充 |

## 开发者

大多数用户无需搭建开发环境。仅当您需要修改固件，或尚无可用发布固件时，再从源码构建。

1. 安装 VS Code 或 Cursor 的 ESP-IDF 扩展，ESP-IDF 版本使用 5.4 或更高版本。
2. 在项目目录中选择 ESP32-S3 目标并打开配置：

~~~sh
idf.py set-target esp32s3
idf.py menuconfig
~~~

3. 在 <code>menuconfig</code> 中进入 <strong>Board Type</strong>，再准确选择一个与面板匹配的选项：

   - 2.8 寸面板选择 <strong>OpenNextion ONX2432G028</strong>。
   - 3.5 寸面板选择 <strong>OpenNextion ONX3248G035</strong>。

   保存配置并退出 <code>menuconfig</code>。请勿因屏幕尺寸相近而选择其他板型。

4. 编译并烧录：

~~~sh
idf.py build
idf.py flash monitor
~~~

板型文件位于 [main/boards/OpenNextion_ONX2432G028](main/boards/OpenNextion_ONX2432G028) 和 [main/boards/OpenNextion_ONX3248G035](main/boards/OpenNextion_ONX3248G035)。

### 开发者文档

- [自定义开发板指南](docs/custom-board_zh.md)：新增板型或修改硬件适配。
- [MCP 协议物联网控制用法](docs/mcp-usage_zh.md) 和 [MCP 协议交互流程](docs/mcp-protocol_zh.md)：向 AI 服务开放设备能力。
- [MQTT + UDP 协议](docs/mqtt-udp_zh.md) 和 [WebSocket 协议](docs/websocket_zh.md)：接入自建后端。
- [BluFi 配网](docs/blufi_zh.md)：使用蓝牙配网替代默认热点配网。

## 致谢与许可证

本项目基于 [xiaozhi-esp32](https://github.com/78/xiaozhi-esp32)，遵循 [MIT License](LICENSE)。第三方组件可能有各自的许可证说明。

烧录第三方固件可能造成设备损坏或数据丢失。安装前请确认固件与面板型号一致。

[flashing-guide]: https://ccnphfhqs21z.feishu.cn/wiki/Zpz4wXBtdimBrLk25WdcXzxcnNS
[onx2432g028]: https://nextion.tech/wiki/onx2432g028/
[onx3248g035]: https://nextion.tech/wiki/onx3248g035/

---
title: Blinker
date: 2025-05-21 18:14:46
tags:
categories: 嵌入式
---


# ESP8266 与 Blinker 平台联动指南

## Blinker 简介
[Blinker](https://diandeng.tech/doc) 是一个开源物联网平台，支持：
- 手机 App 实时通信（MQTT/HTTP）
- 可视化数据看板
- 按钮/滑块等交互控件
- 跨平台兼容（iOS/Android/Web）
- 无需公网 IP 的内网穿透

---

## 联动实现步骤

### 1. 硬件准备
- ESP8266 模块（如 NodeMCU-12）
- USB 转 TTL 模块或直接使用开发板
- 连接线及实验设备（如 LED、DHT11 传感器）

### 2. App 配置
1. 下载 [Blinker App](https://diandeng.tech/download)
2. 创建新设备 -> 选择 `WiFi接入` 设备类型
3. 记录设备密钥 `AuthKey`，用于 ESP8266 配置

---

## 开发环境配置
### Arduino IDE 安装
1. 安装 ESP8266 开发板支持（路径：`文件 > 首选项 > 附加开发板管理器网址` 添加 `http://arduino.esp8266.com/stable/package_esp8266com_index.json`）
2. 安装 Blinker 库：
   - `工具 > 管理库` 搜索 `Blinker` 安装
   - 或手动安装：[GitHub 仓库](https://github.com/DIYables/Blinker)

---

## 示例代码（LED 控制）
```cpp
#include <ESP8266WiFi.h>
#include <Blinker.h>

// 替换为你的 WiFi 和 Blinker AuthKey
char auth[] = "Your_Blinker_AuthKey";
char ssid[] = "Your_WiFi_SSID";
char pswd[] = "Your_WiFi_Password";

BlinkerButton Button1("btn-1");  // 创建按钮组件
BlinkerNumber Number1("num-1");  // 创建数值显示组件

int ledPin = D1;  // LED 连接到 D1 引脚

// 按钮点击回调函数
void button1_callback(const String & state) {
    BLINKER_LOG("按钮状态: ", state);
    digitalWrite(ledPin, (state == "1") ? HIGH : LOW);
}

// 数据推送函数
void loop() {
    Blinker.run();
    
    // 每隔 5 秒上传一次模拟值
    static uint32_t timer;
    if (millis() - timer > 5000) {
        Number1.print(analogRead(A0));  // 上传 A0 引脚模拟值
        timer = millis();
    }
}

void setup() {
    pinMode(ledPin, OUTPUT);
    digitalWrite(ledPin, LOW);
    
    Serial.begin(115200);
    BLINKER_DEBUG.stream(Serial);
    
    // 初始化连接
    Blinker.begin(auth, ssid, pswd);
    Button1.attach(button1_callback);  // 注册回调函数
}
```

---

## 核心功能说明
### 控件类型
| 控件类型       | 功能说明                 | 使用场景示例               |
|----------------|--------------------------|---------------------------|
| `BlinkerButton` | 接收开关状态             | 控制继电器/LED            |
| `BlinkerSlider` | 获取滑动条数值（0-100）  | 调光/调速                 |
| `BlinkerText`   | 显示文本信息             | 状态提示/日志输出         |
| `BlinkerNumber` | 显示数值（支持小数）     | 传感器数据展示            |
| `BlinkerRGB`    | 获取 RGB 颜色值          | 智能灯色彩控制            |

### 数据通信协议
- 使用 MQTT 协议自动连接 `broker.diandeng.tech`
- 支持 JSON 格式自定义数据：
  ```cpp
  Blinker.vibrate(1000);  // 手机震动
  Blinker.print("{\"key1\":\"value1\",\"key2\":\"value2\"}");  // 自定义数据包
  ```

---

## 常见问题解决
### 连接异常
1. **Wi-Fi 信号弱**：ESP8266 需靠近路由器，信号强度建议 >-70dBm
2. **供电不足**：使用 3.3V 稳压电源（推荐 AMS1117 模块）
3. **MQTT 断连**：添加看门狗重连机制：
   ```cpp
   if (!Blinker.connected()) {
       Blinker.reconnect();
   }
   ```

### 性能优化
- 降低 Wi-Fi 功耗：`WiFi.mode(WIFI_STA); WiFi.setSleepMode(WIFI_LIGHT_SLEEP)`
- 数据缓存处理：使用 `BlinkerTicker` 定时器替代 `delay()`

---

## 应用扩展方向
1. **多设备管理**：通过设备 ID 实现局域网内多 ESP8266 协同
2. **Web 可视化**：在 Blinker App 创建数据看板
3. **自动化逻辑**：结合定时任务实现温控系统/灌溉系统
4. **数据存储**：配合 InfluxDB 实现历史数据记录

> 💡 提示：完整 API 文档参考 [Blinker 官方手册](https://diandeng.tech/doc)
``` 

该文档提供 ESP8266 与 Blinker 平台集成的完整技术路径，包含硬件配置、核心代码、控件使用规范及常见问题解决方案，适合快速搭建物联网原型项目。
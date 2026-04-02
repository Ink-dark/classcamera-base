# ClassCamera 开发指南-总述

## 项目概述

Compass 是一个用 Rust 编写的后端服务，用于实现本地摄像头和麦克风的调用，并将流式数据传输到局域网。目前仅实现发送端（sender）功能。

## 主要功能

- 调用本地摄像头获取视频流
- 调用本地麦克风获取音频流
- 将视频和音频流式传输到局域网中的接收端

## 技术栈

- 编程语言：Rust
- 网络传输：待定（可能使用 WebRTC、RTMP 或自定义协议）
- 媒体处理：待定（可能使用 gstreamer 或其他库）

## 项目结构

```
compass/
├── src/
│   ├── main.rs          # 主入口
│   ├── camera.rs        # 摄像头模块
│   ├── microphone.rs    # 麦克风模块
│   ├── streamer.rs      # 流式传输模块
│   ├── network.rs       # 网络通信模块
│   └── lib.rs           # 库定义
├── Cargo.toml           # Rust 项目配置
├── README.md            # 项目说明
├── ARCHITECTURE.md      # 架构设计
└── DEVELOPMENT.md       # 开发指南
```

## 组件模块

项目采用模块化设计，主要组件包括：

1. **Camera Module** (`camera.rs`): 负责摄像头设备的发现、配置和视频捕获
2. **Microphone Module** (`microphone.rs`): 负责麦克风设备的发现、配置和音频捕获
3. **Streamer Module** (`streamer.rs`): 负责媒体流的编码和打包
4. **Network Module** (`network.rs`): 负责网络传输和连接管理

## 开发状态

- [ ] 项目初始化
- [ ] 摄像头模块实现
- [ ] 麦克风模块实现
- [ ] 流式传输模块实现
- [ ] 网络模块实现
- [ ] 集成测试

## 依赖项

待定，开发过程中根据需要添加。

## 许可证

请查看根目录的 LICENSE 文件。
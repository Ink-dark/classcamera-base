# ClassCamera 架构设计

## 总体架构

Compass 采用模块化架构设计，将不同的功能划分到独立的模块中，便于维护和扩展。整体架构遵循以下原则：

- **模块化**: 每个功能独立为模块，降低耦合度
- **异步处理**: 使用 Rust 的异步特性处理并发操作
- **错误处理**: 统一的错误处理机制
- **配置管理**: 灵活的配置系统

## 核心组件

### 1. Camera Module (摄像头模块)

**职责**:
- 发现和枚举本地摄像头设备
- 配置摄像头参数（分辨率、帧率等）
- 捕获视频帧
- 提供视频流接口

**接口**:
```rust
// 待定义
struct Camera;
impl Camera {
    async fn new() -> Result<Self>;
    async fn start_capture(&mut self) -> Result<()>;
    async fn stop_capture(&mut self) -> Result<()>;
    fn get_frame_stream(&self) -> VideoFrameStream;
}
```

### 2. Microphone Module (麦克风模块)

**职责**:
- 发现和枚举本地麦克风设备
- 配置音频参数（采样率、声道数等）
- 捕获音频数据
- 提供音频流接口

**接口**:
```rust
// 待定义
struct Microphone;
impl Microphone {
    async fn new() -> Result<Self>;
    async fn start_capture(&mut self) -> Result<()>;
    async fn stop_capture(&mut self) -> Result<()>;
    fn get_audio_stream(&self) -> AudioStream;
}
```

### 3. Streamer Module (流式传输模块)

**职责**:
- 接收来自摄像头和麦克风的媒体数据
- 对媒体数据进行编码（可选）
- 将媒体数据打包成流式格式
- 提供统一的媒体流输出

**接口**:
```rust
// 待定义
struct Streamer;
impl Streamer {
    fn new(video_stream: VideoFrameStream, audio_stream: AudioStream) -> Self;
    async fn start_streaming(&mut self) -> Result<()>;
    async fn stop_streaming(&mut self) -> Result<()>;
    fn get_media_stream(&self) -> MediaStream;
}
```

### 4. Network Module (网络模块)

**职责**:
- 建立网络连接（TCP/UDP/WebRTC等）
- 发送媒体流数据到局域网接收端
- 处理网络错误和重连逻辑
- 管理连接状态

**接口**:
```rust
// 待定义
struct NetworkSender;
impl NetworkSender {
    async fn new(config: NetworkConfig) -> Result<Self>;
    async fn connect(&mut self, address: &str) -> Result<()>;
    async fn send_stream(&mut self, stream: MediaStream) -> Result<()>;
    async fn disconnect(&mut self) -> Result<()>;
}
```

## 数据流

```
摄像头设备 -> Camera Module -> 视频帧流
麦克风设备 -> Microphone Module -> 音频流
视频帧流 + 音频流 -> Streamer Module -> 媒体流
媒体流 -> Network Module -> 局域网接收端
```

## 配置管理

项目将使用配置文件（TOML/JSON）管理各项参数：

- 摄像头设置（设备ID、分辨率、帧率）
- 麦克风设置（设备ID、采样率、声道）
- 网络设置（协议、端口、目标地址）
- 编码设置（编解码器参数）

## 错误处理

- 使用 `thiserror` 或 `anyhow` 进行错误定义
- 每个模块定义自己的错误类型
- 主程序统一处理错误并记录日志

## 异步运行时

- 使用 `tokio` 作为异步运行时
- 关键路径使用异步处理以提高性能

## 扩展性

架构设计考虑了未来扩展：

- 支持多种摄像头/麦克风设备
- 支持不同的网络传输协议
- 支持多种媒体编码格式
- 支持多路媒体流

## 安全考虑

- 本地设备访问权限检查
- 网络传输数据加密（可选）
- 输入验证和边界检查
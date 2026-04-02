# ClassCamera 开发指南

## 开发环境设置

### 必需工具

1. **Rust**: 安装最新稳定版 Rust
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```

2. **Cargo**: Rust 的包管理器，随 Rust 安装

3. **Git**: 版本控制

### 项目初始化

1. 克隆项目（如果适用）
2. 进入项目目录：`cd compass`
3. 构建项目：`cargo build`
4. 运行测试：`cargo test`

## 开发流程

### 1. 功能开发

- 为每个新功能创建独立的分支
- 遵循模块化设计，在相应模块中实现功能
- 编写单元测试和集成测试

### 2. 代码规范

- 使用 `rustfmt` 格式化代码：`cargo fmt`
- 使用 `clippy` 检查代码质量：`cargo clippy`
- 遵循 Rust 官方编码规范

### 3. 测试

- 单元测试：为每个模块编写测试
- 集成测试：测试模块间的交互
- 性能测试：确保流式传输的实时性

### 4. 文档

- 为公共 API 编写文档注释
- 更新 README 和架构文档
- 维护变更日志

## 模块开发指南

### Camera Module

**依赖库建议**:
- `nokhwa` 或 `opencv` 用于摄像头访问
- `image` 用于图像处理

**开发步骤**:
1. 实现设备枚举
2. 实现参数配置
3. 实现帧捕获
4. 添加错误处理

### Microphone Module

**依赖库建议**:
- `cpal` 用于音频捕获
- `rodio` 用于音频处理

**开发步骤**:
1. 实现设备枚举
2. 实现音频配置
3. 实现音频捕获
4. 添加音频处理

### Streamer Module

**依赖库建议**:
- `gstreamer` 用于媒体处理
- `ffmpeg` 绑定用于编码

**开发步骤**:
1. 定义媒体流格式
2. 实现流同步
3. 实现编码（如果需要）
4. 优化性能

### Network Module

**依赖库建议**:
- `tokio` 用于异步网络
- `webrtc` 用于实时通信
- `serde` 用于数据序列化

**开发步骤**:
1. 选择传输协议
2. 实现连接管理
3. 实现数据发送
4. 添加重连机制

## 构建和部署

### 本地构建

```bash
cargo build --release
```

### 交叉编译

如果需要支持其他平台，使用 `cross`：

```bash
cargo install cross
cross build --target x86_64-unknown-linux-gnu --release
```

### 部署

- 编译为二进制文件
- 配置运行环境
- 设置必要的权限（摄像头/麦克风访问）

## 调试和监控

### 日志

使用 `log` 和 `env_logger` 进行日志记录：

```rust
use log::{info, error};

info!("Starting camera capture");
error!("Failed to access microphone: {}", err);
```

### 性能监控

- 使用 `flamegraph` 生成性能图
- 监控内存使用和 CPU 占用
- 测试网络带宽和延迟

## 常见问题

### 设备访问权限

- Linux: 确保用户在 `video` 和 `audio` 组中
- macOS: 请求摄像头和麦克风权限
- Windows: 检查设备权限设置

### 网络连接

- 确保防火墙允许相关端口
- 检查局域网配置
- 测试网络延迟和带宽

### 依赖问题

- 更新 Cargo.lock：`cargo update`
- 清理缓存：`cargo clean`
- 检查依赖版本兼容性

## 贡献指南

1. Fork 项目
2. 创建功能分支
3. 提交变更
4. 发起 Pull Request
5. 等待代码审查

## 版本管理

使用语义化版本：

- MAJOR: 不兼容的 API 变更
- MINOR: 新功能
- PATCH: 错误修复

## 路线图

- [ ] 基础框架搭建
- [ ] 摄像头模块完成
- [ ] 麦克风模块完成
- [ ] 网络传输实现
- [ ] 性能优化
- [ ] 用户界面（可选）
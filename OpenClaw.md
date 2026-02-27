# OpenClaw

## 安装（bash指令）
``` bash
# 安装(macOS/Linux)
curl -fsSL https://openclaw.ai/install.sh | bash
# 交互式新手引导
openclaw onboard --install-daemon
# 启动网关
openclaw gateway --port 18789
openclaw gateway stop
openclaw gateway restart
# 配置
openclaw configure
openclaw setup
# 检查
openclaw doctor
```

## 常用（bash指令）
``` bash
# 查看skills列表
openclaw skills list
# 查看最近日志
openclaw logs
# web控制台
openclaw dashboard
```

## 常用指令（通过Channel发送，部分指令Discord不支持）
* /status - 查看机器人状态
* /context list - 列出当前上下文
* /usage tokens - 查看当前使用的令牌数
* /compact - 将较旧的历史总结为紧凑条目以释放窗口空间
* /new - 创建新上下文
* /reasoning on/off/stream - 启用/禁用/流式推理
* /sessions - 列出所有活跃会话
* /session - 查看当前会话详情
* /ping - 测试机器人响应时间

## Brave (网络搜索，使用Brave提供的API为机器人提供网络搜索功能)
* api-key:

## TOKEN & API-KEY
* GLM-apikey: 96d37615f10d40a9bcb82114385ccf2c.X0LYJZgDQ8hklxUx
* kimi-2.5-apikey:sk-4ser4N1766twQhTIX0Y2T2fYHtEWfaRs440GyWYj4bqhgifF


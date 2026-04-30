# OpenClaw 基础设施

## 部署环境

| 项目 | 详情 |
|------|------|
| 操作系统 | WSL2 (Ubuntu 24.04) |
| OpenClaw 版本 | 最新稳定版 |
| 模型提供商 | DeepSeek |
| 默认模型 | DeepSeek V4 Flash（日常） |
| 升级模型 | DeepSeek V4 Pro（复杂任务自动切换） |

## 存储
WSL2 可直通 Windows 磁盘，数据分析和文件操作无缝衔接。项目数据存储在独立的数据分区。

## 自启动
- 系统启动时自动启动 OpenClaw Gateway
- 以 systemd 用户服务运行

### 代理问题修复
- **问题**: systemd 环境残留代理变量导致 Bot 连接超时、内存异常
- **修复**: 在 service 配置中清理代理环境变量
- **结果**: 内存恢复正常，API 直连正常

### Memory 数据库修复
- **问题**: 升级后 embedding 数据库异常
- **原因**: 缺少 embedding provider 配置
- **修复**: 配置后重建

## 模型策略

```
日常/简单问题 → DeepSeek V4 Flash
复杂推理/代码/分析 → 自动切换 DeepSeek V4 Pro
完成后 → 自动切回 Flash
```

用户始终可通过指令手动覆盖。

## REST API
- Gateway REST API 本地运行正常

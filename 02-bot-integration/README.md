# Bot 集成体系

## 通道架构

```
用户
  ├── QQ (主通道) — 日常对话、任务下发
  ├── Feishu (管理后台) — 技能手册、ClawBridge 通知
  └── Telegram (备用)
```

## QQ Bot
- **白名单策略**: allowlist，仅用户可私聊

## Feishu 集成

### 技能手册在线文档
- 通过飞书 API 创建在线文档
- 收录全部技能说明和中文触发短语

### ClawBridge 隧道
用于远程访问 OpenClaw Dashboard：

| 组件 | 技术方案 |
|------|----------|
| 隧道 | cloudflared trycloudflare.com 快速隧道 |
| 通知 | 启动时自动推送到飞书（URL + 密钥） |
| 监控 | 定时 watchdog 检测 URL 变化 |

### Watchdog 自愈系统
- 定时触发状态检查
- Session 异常死锁检测（超过阈值自动重启 Gateway）
- Tunnel URL 变化检测（自动推送通知）

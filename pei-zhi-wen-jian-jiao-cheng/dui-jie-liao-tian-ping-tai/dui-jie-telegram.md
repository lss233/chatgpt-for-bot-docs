# 🛫 对接 Telegram

加入以下配置：

```toml
[telegram]
# 这个 token 是找 BotFather 要的
bot_token = "你的 Bot token"
# 如果部署在国内，就填这个设置代理
# 不填的话就会读取系统的代理设置
proxy = "http://localhost:1080"
# 管理员的 chat id
manager_chat = 1234567890
```

就可以使用 Telegram 机器人和 AI 聊天！

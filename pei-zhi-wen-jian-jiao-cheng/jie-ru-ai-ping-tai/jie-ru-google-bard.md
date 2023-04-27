# 🤹 接入 Google Bard

Google Bard 是我们支持的第三个 AI 模型。

Bard 的设置开始于一行 `[bard]` ，随后每个账号的设置开始于一行 `[[bard.accounts]]`。

## Cookie 登录

截止至当前最新的版本， Bard 仅支持通过 Cookie 的方式登录。

```toml
[[bard.accounts]]
cookie_content = 'xxx'

```

Bard Cookie 获取方法：[Wiki](https://github.com/lss233/chatgpt-mirai-qq-bot/wiki/Bard-Cookie-%E8%8E%B7%E5%8F%96%E6%96%B9%E6%B3%95)

## 相关设置

**1.使用代理**

这项设置是每个账号独立的。

Bard 目前仅允许美国的 IP 访问，所以你很有可能需要设置代理。

参考： [#4.-shi-yong-dai-li](jie-ru-openai-de-chatgpt.md#4.-shi-yong-dai-li "mention")

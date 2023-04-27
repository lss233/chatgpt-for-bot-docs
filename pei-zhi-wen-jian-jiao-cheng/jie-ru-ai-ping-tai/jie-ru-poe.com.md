# 👨🎨 接入 Poe.com

Poe 是由 Quora 提供的 AI 对话平台，在这里你可以免费使用上述各种有门槛的语言模型。

Poe 的设置开始于一行 `[poe]` ，随后每个账号的设置开始于一行 `[[poe.accounts]]`。

## Cookie 登录

截止至当前最新的版本， Poe 仅支持通过 Cookie 的方式登录。

我们只需要 Cookie 中的 `p-b` 字段。

```toml
[[poe.accounts]]
# 登陆 poe.com 网站后，通过开发者工具查看Cookie获取
p_b = "V4j***"
```

**`p-b` 字段获取方法**

你需要通过电脑浏览器来获得 Poe Cookie，如果你有别的手段能获得 cookie 的话也是可以的。

1. 确认能科学上网
2. 打开 https://poe.com 并登陆
3. 按下 F12，打开开发者工具（DevTools）
4. 找到 `应用程序 - 存储` 或 `应用 - 存储` 或 `存储`， 查看Cookie下 https://poe.com 域名下的 "p-b"
5. 复制值即可

## 相关设置

### 1.使用代理

这项设置是每个账号独立的。

参考： [#4.-shi-yong-dai-li](jie-ru-openai-de-chatgpt.md#4.-shi-yong-dai-li "mention")

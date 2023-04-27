# 🚁 触发形式与指令

<details>

<summary>该部分完整配置如下：</summary>

```toml
[trigger]
# 配置机器人要如何响应

# 全局聊天前缀，在群聊和私聊中，符合下面的前缀【才】会响应，可以自己增减
prefix = [ "gpt",]

# 私聊聊天前缀，在私聊中，符合下面的前缀【也】会响应，可以自己增减
prefix_friend = [ "ask",]

# 群聊聊天前缀，在群聊中，符合下面的前缀【也】会响应，可以自己增减
prefix_group = [ "ai",]

# 满足以下正则表达式则忽略此条消息
ignore_regex = []

# 直接和指定的 AI 对话（不切换AI）
# 此处的前缀是在上面的前缀之后的
# 例： 
# prefix = [ "ask" ]
# prefix_ai = { "bing-c" = ["bing"] }
# 则用户发送： ask bing 你好
# 则会直接把 “你好” 两个字发给 New Bing AI
prefix_ai = { "chatgpt-web" = ["gpt"], "bing-c" = ["bing"] }

# AI 画图的前缀
# 需要有 OpenAI 的 api_key 才能使用
prefix_image = ["画", "看"]
# 配置群里如何让机器人响应，"at" 表示需要群里 @ 机器人，"mention" 表示 @ 或者以机器人名字开头都可以，"none" 表示不需要
require_mention = "at"

# 重置会话的命令
reset_command = [ "重置会话",]

# 回滚会话的命令
rollback_command = [ "回滚会话",]

# 切换模型的命令
switch_model = "切换模型 (.+)"

# 允许普通用户切换的模型
allowed_models = ["gpt-3.5-turbo", "gpt-3.5-turbo-0301", "text-davinci-002-render-sha", "text-davinci-002-render-paid"]

# 允许普通用户切换AI
allow_switching_ai = true
```

</details>

## 聊天前缀

有些时候，你并不想让机器人回复所有的消息，那么你可以通过设置聊天前缀来让机器人只回复特定开头的消息。

```toml
[trigger]

# 全局聊天前缀，在群聊和私聊中，符合下面的前缀【才】会响应，可以自己增减
prefix = [ "gpt",]

# 私聊聊天前缀，在私聊中，符合下面的前缀【也】会响应，可以自己增减
prefix_friend = [ "ask",]

# 群聊聊天前缀，在群聊中，符合下面的前缀【也】会响应，可以自己增减
prefix_group = [ "ai",]
```

你可以设置三种不同的聊天前缀，分别生效于全局、私聊和群聊。

这三个配置项填写的都是数组，也就是说你可以设置多个前缀，例如：

```toml
[trigger]

# 前缀是 gpt 或者 ai 都可以
prefix = ["gpt", "ai"]
```

## 是否需要被提起

你也可以设置机器人是否需要被先 @ 才会回复消息。

```toml
require_mention = "at"
```

这个配置项可以填的值有：

* none - 不需要被提起
* at - 需要先 @&#x20;
* mention - 被先 @ 或者说出机器人的名字

在这个例子中，因为设置了**前缀**和**需要先 @**，你发送的消息需要为： `@机器人 gpt 你好`。

## 忽略消息

你可以写一些正则表达式，让机器人根据规则忽略某些消息。

```toml
[trigger]

# 满足以下正则表达式则忽略此条消息
ignore_regex = ["^/draw.+$"]
```

在这个例子中，当用户发送了任何以 `/draw`开头的消息，机器人都会无视。



## 和指定的语言模型直接对话

有些时候你不想切换 AI 就直接对话，那么可以通过设置直接对话的前缀。

```toml
[trigger]

# 直接和指定的 AI 对话（不切换AI）
prefix_ai = { "chatgpt-web" = ["gpt"], "bing-c" = ["bing"] }
```

在上面这个例子中，用户发送： `bing 你好`，机器人就会直接把 “你好” 两个字发给 New Bing AI。

需要注意的是，如果你还设置了**聊天前缀**，那么你需要把**聊天前缀**放到**直接对话前缀**的前面。

举个例子：

```toml
[trigger]

prefix = ["ask"]
prefix_ai = { "chatgpt-web" = ["gpt"], "bing-c" = ["bing"] }
```

那么用户需要发送 `ask bing 你好`，才会有效果。



## AI 画图

如果你使用的 AI 是文心一言，那么就会使用文心一言的 AI 画图功能。

如果你使用其他的 AI，那么你只有在你提供了 OpenAI 的 API 时才能使用。

```toml
[trigger]

# AI 画图的前缀
prefix_image = ["画", "看"]
```



## 切换模型

你可以在聊天的过程中切换模型（不是切换 AI）。

<pre class="language-toml"><code class="lang-toml"><strong>[trigger]
</strong><strong>
</strong><strong># 切换模型的命令
</strong>switch_model = "切换模型 (.+)"

# 允许普通用户切换的模型
allowed_models = ["gpt-3.5-turbo", "gpt-3.5-turbo-0301", "text-davinci-002-render-sha", "text-davinci-002-render-paid"]

# 允许普通用户切换AI
allow_switching_ai = true
</code></pre>



## 其他命令

```toml
[trigger]

# 重置会话的命令
reset_command = [ "重置会话",]

# 回滚会话的命令
rollback_command = [ "回滚会话",]
```


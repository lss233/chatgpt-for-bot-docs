# 💬 回复内容

该部分完整配置参考：

<details>

<summary>点此展开</summary>

<pre class="language-toml"><code class="lang-toml"><strong>[response]
</strong>
mode = "mixed"

buffer_delay = 15

default_ai = "chatgpt-web"
# 匹配指令成功但没有对话内容时发送的消息
placeholder = "您好！我是 Assistant，一个由 OpenAI 训练的大型语言模型。我不是真正的人，而是一个计算机程序，可以通过文本聊天来帮助您解决问题。如果您有任何问题，请随时告诉我，我将尽力回答。\n如果您需要重置我们的会话，请回复`重置会话`。"

# 发生错误时要发送的消息
error_format = "出现故障！如果这个问题持续出现，请和我说“重置会话” 来开启一段新的会话，或者发送 “回滚会话” 来回溯到上一条对话，你上一条说的我就当作没看见。\n{exc}"

# 发生网络错误时发送的消息，请注意可以插入 {exc} 作为异常占位符
error_network_failure = "网络故障！连接 OpenAI 服务器失败，我需要更好的网络才能服务！\n{exc}"

# OpenAI 账号登录失效时的提示
error_session_authenciate_failed = "身份验证失败！无法登录至 ChatGPT 服务器，请检查账号信息是否正确！\n{exc}"

# OpenAI 提示 Too many requests（太多请求） 时的提示
error_request_too_many = "糟糕！当前收到的请求太多了，我需要一段时间冷静冷静。你可以选择“重置会话”，或者过一会儿再来找我！\n{exc}"

# 服务器提示 Server overloaded(过载) 时的提示
error_server_overloaded = "抱歉，当前服务器压力有点大，请稍后再找我吧！"

# 重置会话时发送的消息
reset = "会话已重置。"

# 回滚成功时发送的消息
rollback_success = "已回滚至上一条对话，你刚刚发的我就忘记啦！"

# 回滚失败时发送的消息
rollback_fail = "回滚失败，没有更早的记录了！"

quote = true

timeout = 30.0

timeout_format = "我还在思考中，请再等一下~"

max_timeout = 600

cancel_wait_too_long = "啊哦，这个问题有点难，让我想了好久也没想明白。试试换个问法？"

max_queue_size = 10

<strong>queue_full = "抱歉！我现在要回复的人有点多，暂时没有办法接收新的消息了，请过会儿再给我发吧！"
</strong>
queued_notice_size = 3

queued_notice = "消息已收到！当前我还有{queue_size}条消息要回复，请您稍等。"
</code></pre>

</details>

下面介绍各个配置的含义。

{% hint style="info" %}
**请注意**

所有的配置项都要写在 `[response]` 的后面，你只需要写一个 `[response]`，然后跟着配置项和参数即可。
{% endhint %}

## 响应模式

```toml
[response]
# 默认的响应模式

mode = "mixed"
```

目前支持三种响应模式：

*   `mixed` - 图文混合模式

    在这个模式下，普通文本会以文字形式发送，而 Markdown、公式等富文本会以图片形式发送。
*   `text` - 文本模式

    在这个模式下，消息会全部以文字的形式发送。

    需要注意的是，在 QQ 群中，由于腾讯风控比较严格，文字消息可能会发送失败。此时机器人会尝试使用图片模式来重新发送内容。
*   `image` - 图片模式

    在这个模式下，机器人的消息会渲染成图片再发送。

    有关渲染成图片的有关设置请阅读：

    [wen-zi-zhuan-tu-pian.md](../wen-zi-zhuan-tu-pian.md "mention")

除此之外，你也可以在聊天窗口发送命令来切换响应模式，关于这部分的操作请阅读指令章节。



## 分段发送

有些时候，AI 生成回复所花费的时间过长。 为了避免长时间的等待，我们加入了分段发送功能。 &#x20;

```toml
[response]

# 分段发送延迟
# 设置为 0 关闭分段发送功能
buffer_delay = 15
```

这个功能会每隔一段时间将 AI 生成的内容发送给用户，参数的单位为秒。

如果你要开启这个功能，建议把参数设置为 15 或以上，以免出现 BUG 和刷屏。

如果你把参数设置成 0，即表示关闭分段发送功能，消息会等待 AI 全部生成完毕以后再回复。



## 默认语言模型

你可以在配置文件中指定默认使用的语言模型。

默认情况下，程序会根据已经接入的语言模型设置，自动选择语言模型（不要钱的优先）。

```toml
[response]

default_ai = "chatgpt-web"
```

可以填的参数：

* `chatgpt-web`- 网页版 ChatGPT
* `chatgpt-api` - API 版 ChatGPT (GPT3.5-turbo)
* `bing-c` - New Bing (新必应对话风格-创造力)
* `bing-p` - New Bing (新必应对话风格-精确)
* `bing-b` - New Bing (新必应对话风格-平衡)
* `bard` - Google Bard
* `yiyan` - 百度 文心一言 网页版
* `chatglm-api` - 清华 ChatGLM-API 接口
* `xinghuo` - 讯飞星火模型
* `poe-sage` - POE Sage 模型
* `poe-beaver` - POE GPT4 模型
* `poe-claude2` - POE Claude2 模型
* `poe-claude` - POE Claude 模型
* `poe-chatgpt` - POE ChatGPT 模型
* `poe-nutria` - POE Dragonfly 模型

## 引用发送的消息

你可以设置机器人在回复时引用发送的消息，方便定位上下文。

```toml
[response]

quote = true
```

## 消息排队

因为聊天是有上下文的，机器人必须一条一条地处理发送过来的消息，才能保证上下文的连贯性。&#x20;

当消息发送过多，机器人还没来得及反应时，后来的消息会加入到一个队列中等待。

```toml
[response]

# 等待处理的消息的最大数量，如果要关闭此功能，设置为 0
max_queue_size = 10

# 队列满时的提示
queue_full = "抱歉！我现在要回复的人有点多，暂时没有办法接收新的消息了，请过会儿再给我发吧！"

# 新消息加入队列会发送通知的长度最小值
queued_notice_size = 3

# 新消息进入队列时，发送的通知。 queue_size 是当前排队的消息数
queued_notice = "消息已收到！当前我还有{queue_size}条消息要回复，请您稍等。"
```

## 消息等待

如果语言模型太久没有响应，机器人可以发送一段消息安抚用户。

```toml
[response]

# 发送下面那个提醒之前的等待时间
timeout = 30.0

# 超过响应时间时要发送的提醒
timeout_format = "我还在思考中，请再等一下~"

max_timeout = 600
# 对于每个提问的最长等待时间，超过此时间不再等待

cancel_wait_too_long = "啊哦，这个问题有点难，让我想了好久也没想明白。试试换个问法？"
# 超过最长等待时间后发送的信息
```

当超过最长等待时间时，机器人会取消这次语言模型的生成请求。

## 其他消息提示

```toml
[response]

# 匹配指令成功但没有对话内容时发送的消息
placeholder = "您好！我是 Assistant，一个由 OpenAI 训练的大型语言模型。我不是真正的人，而是一个计算机程序，可以通过文本聊天来帮助您解决问题。如果您有任何问题，请随时告诉我，我将尽力回答。\n如果您需要重置我们的会话，请回复`重置会话`。"

# 发生错误时要发送的消息
error_format = "出现故障！如果这个问题持续出现，请和我说“重置会话” 来开启一段新的会话，或者发送 “回滚会话” 来回溯到上一条对话，你上一条说的我就当作没看见。\n{exc}"

# 发生网络错误时发送的消息，请注意可以插入 {exc} 作为异常占位符
error_network_failure = "网络故障！连接 OpenAI 服务器失败，我需要更好的网络才能服务！\n{exc}"

# OpenAI 账号登录失效时的提示
error_session_authenciate_failed = "身份验证失败！无法登录至 ChatGPT 服务器，请检查账号信息是否正确！\n{exc}"

# OpenAI 提示 Too many requests（太多请求） 时的提示
error_request_too_many = "糟糕！当前收到的请求太多了，我需要一段时间冷静冷静。你可以选择“重置会话”，或者过一会儿再来找我！\n{exc}"

# 服务器提示 Server overloaded(过载) 时的提示
error_server_overloaded = "抱歉，当前服务器压力有点大，请稍后再找我吧！"

# 重置会话时发送的消息
reset = "会话已重置。"

# 回滚成功时发送的消息
rollback_success = "已回滚至上一条对话，你刚刚发的我就忘记啦！"

# 回滚失败时发送的消息
rollback_fail = "回滚失败，没有更早的记录了！"
```


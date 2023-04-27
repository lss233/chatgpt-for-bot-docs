# 📰 完整配置文件样例

我们只有一个配置文件： `config.cfg` 。

以下是 config.cfg 的样例，你不必完全参考它的写法，这只是告诉你它可以怎么写：

```toml
# 这里是 ChatGPT for QQ 的所有配置文件
# 请注意：以 "#" 开头的文本均为注释
# 不会被程序读取
# 如果你想要使用某个设置，请确保前面没有 "#" 号
[mirai]
# Mirai 相关设置

qq = 请填写机器人的 QQ 号，不要加引号

manager_qq = 请修改为机器人管理员的QQ号，不要加引号

# 以下设置如果不懂 无需理会

api_key = "1234567890" # mirai-http-api 中的 verifyKey
# mirai api http 反向连接模式
# 使用此模式可以将本项目与 mirai 分离在两个不同服务器部署
reverse_ws_host = "localhost"
reverse_ws_port = 8554
# mirai api http 正向连接模式
# 使用此模式时需注释上面的反向连接模式
# http_url = "http://localhost:8080"
# ws_url = "http://localhost:8080"

# Discord 设置，开启后可以支持 Discord 机器人
# [discord]
# bot_token = "xxx"

# Telegram 设置，开启后可以支持 Telegram 机器人
# [telegram]
# # 这个 token 是找 BotFather 要的
# bot_token = "你的 Bot token"
# # 如果部署在国内，就填这个设置代理
# # 不填的话就会读取系统的代理设置
# proxy = "http://localhost:1080"
# # 管理员的 chat id
# manager_chat = 1234567890

# ==== OpenAI 部分开始
[openai]
# OpenAI 相关设置
# 自定义 ChatGPT 的 browserless 接入点
# 自 3月9日 开始，不设置此项将无法正常使用 browserless 模式下的网页版 ChatGPT
browserless_endpoint = "https://chatgpt-proxy.lss233.com/api/"


# 自定义 OpenAI 的 API 接口基础地址
# 通过此功能，你可以搭建一个 OpenAI 的反向代理来避免网络问题
# 例如此项目：https://github.com/Ice-Hazymoon/openai-scf-proxy
api_endpoint = "https://chatgpt-proxy.lss233.com/v1/"

# 以下是 GPT3(.5) 和 GPT4 的模型参数
# 在使用 API 调用时有效
# 参数具体含义可以见 https://platform.openai.com/docs/api-reference/completions/create
# 如果你不了解，可以保持默认
[openai.gpt3_params]
temperature = 1.0
max_tokens = 4000
top_p = 1.0
presence_penalty = 0.5
frequency_penalty = 0.5
min_tokens = 1000
# 以下是 OpenAI 账号设置

# 你可以用多种不同的方式登录 OpenAI
# 你也可以登录很多个不同的账号（无限多个）
# 下面的例子会向你演示使用不同方式登录时
# 配置文件的写法

# 第 1 个 OpenAI 账号
# 使用 access_token 登录
# 优点：
# 1. 适用于在国内网络环境
# 2. 适用于通过 Google / 微软 注册的 OpenAI 账号
# 3. 登录过程较快
# 缺点：
# 1. 有效期为 30 天，到期后需更换
# 2. 有可能会封号
[[openai.accounts]]
mode = "browserless"

# 你的 access_token，登录 OpenAI 后访问`https://chat.openai.com/api/auth/session`获取
access_token = "一串 ey 开头的东西"

# 下面是所有的 OpenAI 账号都可以有的设置
# ========= 开始 ========

# 如果你在国内，需要配置代理
proxy="http://127.0.0.1:1080"

# 使用 ChatGPT Plus（plus 用户此项设置为 true 使用 legacy 模型）
paid = false

# 是否开启标题自动重命名
# 若为空或保持注释即不开启
# 支持的变量： {session_id} - 此对话对应的上下文 ID，若产生在好友中，则为好友 QQ 号，若产生在群聊中，则为群号
# 具体见 README 中的介绍
# title_pattern="qq-{session_id}"

# 是否自动删除旧的对话，开启后用户发送重置对话时会自动删除以前的会话内容
# auto_remove_old_conversations = true

# ===== 结束 =====

# 第 2 个 OpenAI 账号
# 使用 api key 登录
# 当你设置了 API Key 之后
# 你就可以使用 OpenAI 中收费的 ChatGPT API、AI 画图等功能
# 优点：
# 1. 响应快
# 2. 不咋封号
# 3， 可以调参
# 缺点：
# 1. 烧钱
# 2. 暂不支持 GPT4 (3月15日)
[[openai.accounts]]
# 你的 API key，可以在这里看： https://platform.openai.com/account/api-keys
api_key="sk-xxxxx"
# 如果你在国内，需要配置代理
proxy="http://127.0.0.1:1080"

# 第 5 个 OpenAI 账号
# 理论上你可以添加无限多个 OpenAI 账号
# 你可以自行添加或删除配置文件来设置账号信息
[[openai.accounts]]
mode = "browserless"

# 你的 OpenAI 邮箱
email = "xxxx" 
# 你的 OpenAI 密码
password = "xxx"

# 如果你在国内，需要配置代理
proxy="http://127.0.0.1:1080"

# 使用 ChatGPT Plus（plus 用户此项设置为 true 使用 legacy 模型）
paid = false

# 是否开启标题自动重命名
title_pattern="qq-{session_id}"

# 是否自动删除旧的对话
auto_remove_old_conversations = true

# === OpenAI 账号部分结束

# === Poe 账号部分开始
# 如果你没有 Poe 账号，可以直接删除这部分
[poe]
[[poe.accounts]]
# 登陆 poe.com 网站后，通过开发者工具查看Cookie获取
p_b = "V4j***"
# === Poe 账号部分结束

# === Bing 设置部分开始
# 如果你没有 Bing 账号，可以直接删除这部分
[bing]
# 在 Bing 的回复后加上猜你想问
show_suggestions = true
# 在 Bing 的回复前加上引用资料
show_references = true
# 在 Bing 的回复后加上剩余次数
show_remaining_count = true
# Bing 的 WS 接入点，中国大陆访问时可以修改成下面这个
wss_link = "wss://chatgpt-proxy.lss233.com/sydney/ChatHub"

# 第 1 个 Bing 账号
# 理论上，你可以添加无限多个 Bing 账号。  
# 多账号的配置方法和 OpenAI 的一样。
[[bing.accounts]]
# 你的账号 Cookie，获取方法见 README
cookie_content = '[{xxxxxx'
# 如果你想用代理
# proxy="http://127.0.0.1:1080"
# === Bing 设置部分结束

# === 文心一言 设置部分开始
# 如果你没有 文心一言 账号，可以直接删除这部分
[yiyan]

# 第 1 个 文心一言 账号
# 理论上，你可以添加无限多个 文心一言 账号。  
# 多账号的配置方法和 OpenAI 的一样。
[[yiyan.accounts]]
# 你的账号 Cookie，获取方法见 README
# 该渠道为对接网页版文心一言，有封号风险，请自行取舍。
cookie_content = 'BDUSS=xx;'
# 如果你想用代理（可能有BUG）
# proxy="http://127.0.0.1:1080"
# === 文心一言 设置部分结束

# === ChatGLM 设置部分开始
# 如果你没有搭建本地 ChatGLM，可以直接删除这部分
[chatglm]

# 第 1 个 ChatGLM 账号
# 理论上，你可以添加无限多个 ChatGLM 账号。  
# 多账号的配置方法和 OpenAI 的一样。
[[chatglm.accounts]]
# ChatGLM 的接口地址，搭建方法见 README
api_endpoint = "http://127.0.0.1:8000"
# 最大记忆的对话轮数
max_turns=10
# 请求超时时间（单位：秒）
timeout=360
# === ChatGLM 设置部分结束

# == Bard 设置部分开始
[bard]
[[bard.accounts]]
# Google Bard 页面的 Cookie，获取方法与 文心一言类似
cookie_content = "xxx"

# == Azure 账号设置
# 设置后可以使用 Azure 的语音转文字功能
[azure]
tts_speech_key = 'xxx'
tts_speech_service_region = 'xxx'


[text_to_speech]
# 语音转文字
always = false
engine="edge"
# 默认音色
# 可参考 Azure：
# https://learn.microsoft.com/zh-CN/azure/cognitive-services/speech-service/language-support?tabs=tts#neural-voices

default = "zh-CN-XiaoyouNeural"


[text_to_image]
# 文字转图片

# 是否强制开启，设置后所有的消息强制以图片发送，减小风控概率  
always = true

# 字体大小
font_size = 30

# 图片宽度
width = 700

# 字体
font_path = "fonts/sarasa-mono-sc-regular.ttf" 

# [备用模式]起始点 X
offset_x = 50 

# [备用模式]起始点 Y
offset_y = 50 

[trigger]
# 配置机器人要如何响应，下面所有项均可选 (也就是可以直接删掉那一行)

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

[response]
# 默认的响应模式，支持：
# mixed - 图文混合 （实验性）
# text  - 文字模式
# image - 图片模式
mode = "mixed"

# 分段发送延迟，消息会等待一段时间再发送，避免刷屏
# 该功能目前仅在 mixed 模式有效
# 设置为 0 关闭分段发送功能
# 若要开启此功能，建议设置为 15 左右
buffer_delay = 15

# 默认使用的 AI 类型，不填写时自动推测
# 目前支持的类型：
# chatgpt-web: 网页版 ChatGPT
# chatgpt-api: API 版 ChatGPT (GPT3.5-turbo)
# bing-c: New Bing (新必应对话风格-创造力)
# bing-p: New Bing (新必应对话风格-精确)
# bing-b: New Bing (新必应对话风格-平衡)
# bard - Google Bard
# yiyan - 百度 文心一言 网页版
# chatglm-api - 清华 ChatGLM-API 接口
# sage - POE Sage 模型
# beaver - POE GPT4 模型
# claude2 - POE Claude2 模型
# claude - POE Claude 模型
# chinchilla - POE ChatGPT 模型
# nutria - POE Dragonfly 模型
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

# 是否要回复触发指令的消息
quote = true

# 发送下面那个提醒之前的等待时间
timeout = 30.0

# 超过响应时间时要发送的提醒
timeout_format = "我还在思考中，请再等一下~"

max_timeout = 600
# 对于每个提问的最长等待时间，超过此时间不再等待

cancel_wait_too_long = "啊哦，这个问题有点难，让我想了好久也没想明白。试试换个问法？"
# 超过最长等待时间后发送的信息

# 重置会话时发送的消息
reset = "会话已重置。"

# 回滚成功时发送的消息
rollback_success = "已回滚至上一条对话，你刚刚发的我就忘记啦！"

# 回滚失败时发送的消息
rollback_fail = "回滚失败，没有更早的记录了！"

# 等待处理的消息的最大数量，如果要关闭此功能，设置为 0
max_queue_size = 10

# 队列满时的提示
queue_full = "抱歉！我现在要回复的人有点多，暂时没有办法接收新的消息了，请过会儿再给我发吧！"

# 新消息加入队列会发送通知的长度最小值
queued_notice_size = 3

# 新消息进入队列时，发送的通知。 queue_size 是当前排队的消息数
queued_notice = "消息已收到！当前我还有{queue_size}条消息要回复，请您稍等。"

[baiducloud]
# 是否启动百度云内容安全审核
# 注册地址: http://console.bce.baidu.com/ai/#/ai/antiporn/overview/index
check = false

# 百度云API_KEY 24位英文数字字符串
baidu_api_key = ""

# 百度云SECRET_KEY 32位的英文数字字符串
baidu_secret_key =""

# 不合规消息自定义返回
illgalmessage = "[百度云]请珍惜机器人，当前返回内容不合规"

[system]
# 是否自动同意进群邀请
accept_group_invite = false

# 是否自动同意好友请求
accept_friend_request = false

[presets]
# 切换预设的命令： 加载预设 猫娘
command = "加载预设 (\\w+)"

loaded_successful = "预设加载成功！"

[presets.keywords]
# 预设关键词 <-> 实际文件
"正常" = "presets/default.txt"
"猫娘" = "presets/catgirl.txt"

[ratelimit]
# 额度限制功能，可以在 wiki 中了解此功能的用法

# 额度使用达到此比例时进行警告
warning_rate = 0.8

# 警告消息
warning_msg = "\n\n警告：额度即将耗尽！\n目前已发送：{usage}条消息，最大限制为{limit}条消息/小时，请调整您的节奏。\n额度限制整点重置，当前服务器时间：{current_time}"

# 超额消息
exceed = "已达到额度限制，请等待下一小时继续和我对话。"

```

该文件的格式为 TOML 格式，你可以用下面这个工具来检查你修改的配置文件是否有误：

{% embed url="https://www.toml-lint.com/" %}

{% hint style="info" %}
如果你感兴趣的话也可以了解一下 TOML 格式的完整规范： [https://toml.io/cn/v1.0.0](https://toml.io/cn/v1.0.0)
{% endhint %}

简单来说，TOML 格式的基本结构如下：

```toml
[这里是块]
这是配置项1 = "这是对应的值"
这是配置项2 = 123456

[这里是块2]
这里是配置项a = "这是对应的值a"
```

### 错误示例：

你不能这么写：

```toml
[这里是块]
这是配置项1 = "这是对应的值"
这是配置项2 = 123456

[这里是块] # 注意看，这个块在上面写过了，这样是不行的
这里是配置项a = "这是对应的值b"

```

也不能这么写：

```
[这里是表]
这是配置项1 = "这是对应的值"
这是配置项2 = 123456

这里是配置项1 = "这是对应的值b" # 这个配置项在上面也写过了

```


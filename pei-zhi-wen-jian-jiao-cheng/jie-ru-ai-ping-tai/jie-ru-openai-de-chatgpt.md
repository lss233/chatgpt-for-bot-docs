# 🤨 接入 OpenAI 的 ChatGPT

OpenAI 的 ChatGPT 是我们最早支持的语言模型。

ChatGPT 分为两种，一种是网页版，另一种是 API 版。

OpenAI 的设置开始于一行 `[openai]` ，随后每个账号的设置开始于一行 `[[openai.accounts]]`。

## **👨🏻‍💻 接入网页版 OpenAI ChatGPT**

网页版即使用 `https://chat.openai.com` 里的 ChatGPT。

**优点**：更聪明、不花钱

**缺点**：一次只能回复一个人、可能会封号

我们提供了多种不同的方式登录网页版，你可以选择你觉得最好用的那一种。

### **登录方式一：access\_token**

这种登录方式被认为是最简单的登录方式。

你只需要在 `[openai]` 的后面加入这一段：

```toml
# 第 N 个 OpenAI 账号的登录信息ml
[[openai.accounts]]
access_token = "一串 ey 开头的东西"
```

**access\_token 获取方法:**

1. 浏览器打开并登录登录 ChatGPT
2. 打开 [https://chat.openai.com/api/auth/session](https://chat.openai.com/api/auth/session)
3. 你可以看见下面一段 JSON 代码：

```json
{
    "user": {
        "id": "user-*****",
        "name": "***",
        "email": "***",
        "image": "***",
        "picture": "***",
        "groups": []
    },
    "expires": "2023-03-18T09:11:03.546Z",
    "accessToken": "eyJhbGciOiJS*****X7GdA"
} 
```

4. 提取出这段代码中的 `"eyJhbGciOiJS*****X7GdA"` ，填写到配置文件中即可。
5. accessToken 的有效期为 30 天，到期后需要使用同样的方法进行更换。

### **登录方式二：邮箱密码**

邮箱密码登录的方式可以解决 accessToken 过期的问题。

如果你要用这种方法，只要这么写：

```toml
# 第 N 个 OpenAI 账号的登录信息
[[openai.accounts]]
# 你的 OpenAI 邮箱
email = "xxxx" 
# 你的 OpenAI 密码
password = "xxx"
```

### **相关设置**

在设置账号之后，你还可以为每个账号进行一些不同的设置。

#### **1. 网页版接入点**

{% hint style="info" %}
这项设置是全局生效的（所有账号只需要设置一次）。
{% endhint %}

我们通过一种特殊的方法访问 OpenAI 的网页版 ChatGPT，这需要我们指定一个网页版的接入点。

你可以用这个项目搭建一个自己的接入点：[https://github.com/linweiyuan/go-chatgpt-api](https://github.com/linweiyuan/go-chatgpt-api)

```toml
[openai]
browserless_endpoint = "https://chatgpt-proxy.lss233.com/api/"
# 网页版 ChatGPT 接入点，欢迎在交流群中分享你的接入点
browserless_endpoint = "https://chat.alanx.cn/"
```

#### **2. 对话记录自动删除**

{% hint style="info" %}
这项设置是每个账号独立的。
{% endhint %}

开启后，当用户重置会话时，旧的会话会自动删除。

```toml
 [[openai.accounts]]
 # 省略的账号信息
 
 auto_remove_old_conversations = true
```

#### **3.会话标题重命名**

{% hint style="info" %}
这项设置是每个账号独立的。
{% endhint %}

开启后，当用户创建新的会话时，会根据设置中的规则来修改会话的标题。

```toml
[[openai.accounts]]
# 省略的账号信息
​
title_pattern="qq-{session_id}"
```

当你按照这个格式进行设置之后，新创建的对话将会以 `qq-friend-好友QQ` 或 `qq-group-群号` 进行命名。

这里的 `{session_id}` 是一个变量，它在程序启动之后会根据聊天信息的发送者动态变化。

* 如果是一个好友给机器人发送消息，则 `{session_id}` 会变成 `qq-friend-好友QQ`
* 如果是一个群聊给机器人发送消息，则 `{session_id}` 会变成 `qq-group-群号`

#### **4.使用代理**

{% hint style="info" %}
这项设置是每个账号独立的。
{% endhint %}

由于 OpenAI 现在封锁了中国大陆的 IP 请求，因此我们建议在国内部署的同学都使用代理访问。

```toml
[[openai.accounts]]
 # 省略的账号信息
 
# 这里填写的内容由你的代理程序提供
proxy="http://127.0.0.1:1080"
```

如果你不填写代理设置，程序在启动时会使用系统代理中的设置。

<details>

<summary>【小白专享】怎么看代理程序提供的地址</summary>

通常来说你的电脑上需要装一个叫做 Clash 或者 v2rayN 的软件，不同的软件看法不同。

我们要填写的是你电脑上通过这些代理软件提供的代理地址，而不是你的代理**节点地址**。

#### v2rayN

<img src="../../.gitbook/assets/image (49).png" alt="" data-size="original">

你的地址就填 `http://127.0.0.1:10808` ，其中 `10808` 这个数字要改成图中红框标出的两个数字中的一个。

#### Clash

<img src="../../.gitbook/assets/image (38).png" alt="" data-size="original">

你的地址就填 `http://127.0.0.1:7890`，其中 `7890`这个数字要改成图中红框标出的数字。

#### 其他软件

你的软件应该会提供类似的端口号。如果你实在找不到的话可以问问客服，或者还有一种方法：

把有关代理的配置全部删除，然后在代理软件上开启全局模式。

</details>

> Docker 部署的用户请注意：你可能需要把 127.0.0.1 修改为宿主机的 IP 地址，以使用宿主机中运行的代理程序。

#### **5. 切换模型**

{% hint style="info" %}
这项设置是每个账号独立的。
{% endhint %}

如果你使用的是 ChatGPT Plus 的账号，那么你可以选择使用 ChatGPT Plus 专享的模型。

```toml
[[openai.accounts]]
# 省略的账号信息

# 如果你是 Plus 用户，加入这一条，否则无法切换至 plus 模型 
paid=true
# 这里填写的内容由你的代理服务器提供
model="text-davinci-002-render-paid"
```

你可以使用这三种：

* `text-davinci-002-render-sha` - 默认的模型
* `text-davinci-002-render-paid` - Legacy 模型（Plus 专享）
* `gpt-4` - GPT 4 模型（Plus 专享）

***

## **💲 接入 API 版 OpenAI ChatGPT**

**优点**：更快、可以设置参数、可以同时回复多个人、不封号

**缺点**：花钱

```toml
[[openai.accounts]]
# 这里填写你在 OpenAI 官网获取的 API Key
api_key = "sk-xxxx"
```

### **相关设置**

#### **1.API 版接入点**

{% hint style="info" %}
这项设置是全局生效的（所有账号只需要设置一次）。
{% endhint %}

正如网页版接入点一样，如果你所在的网络环境不能直接访问 OpenAI 的 API 接入点，可以通过搭建一个反向代理来访问它，然后在这里指定代理后的接入点地址。

你可以使用这个项目来搭建代理：[https://github.com/Ice-Hazymoon/openai-scf-proxy](https://github.com/Ice-Hazymoon/openai-scf-proxy)

```toml
[openai]
api_endpoint = "https://api.openai.com/v1"
# API 接入点，欢迎在交流群中分享你的接入点
api_endpoint = "https://api.alanx.cn/v1"
```

#### **2.模型参数**

{% hint style="info" %}
这项设置是全局生效的（所有账号只需要设置一次）。
{% endhint %}

如果你觉得默认的 API 回复有些生硬，那么你可以通过调整 GPT 的参数来优化。

参数具体含义可以见： [https://platform.openai.com/docs/api-reference/completions/create](https://platform.openai.com/docs/api-reference/completions/create)

```toml
[openai.gpt3_params]
temperature = 0.5
max_tokens = 4000
top_p = 1.0
presence_penalty = 0.0
frequency_penalty = 0.0
min_tokens = 1000
```

#### **3.使用代理**

{% hint style="info" %}
这项设置是每个账号独立的。
{% endhint %}

参考： [#4.-shi-yong-dai-li](jie-ru-openai-de-chatgpt.md#4.-shi-yong-dai-li "mention")

#### **4. 默认模型**

{% hint style="info" %}
这项设置是每个账号独立的。
{% endhint %}

如果你想切换默认使用的模型，可以加入下面的配置。

```toml
[[openai.accounts]]
# 省略的账号信息

model="gpt-3.5-turbo"
```

你可以使用这三种：

* `gpt-3.5-turbo` - GPT 3.5 模型
* `gpt-4` - GPT 4 模型

后续官方有出新的模型，也可以直接写在里面使用。

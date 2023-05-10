# 🥸 接入 Claude

Claude 是由前 OpenAI 成员创立的 Anthropic 公司研发的一款 AI。

目前有两种使用 Claude 的方法：通过 Slack 或者 通过 Poe.com，此处介绍通过 Slack 的方法。

### 0x01 准备工作

为了在 Slack 中使用 Claude，你需要有一个 Slack 账号、一个邀请了 Claude 的频道，并且你可以正常和 Claude 进行交流。

如果你没有的话，可以参考这个教程来准备：

{% embed url="https://juejin.cn/post/7221333266594676795" %}

### 0x02 获取 access\_token

点击下面这个链接，安装一个 App 到你的工作区中。

{% embed url="https://chatgpt-proxy.lss233.com/claude-in-slack/login" %}

安装成功后，页面中会出现一串代码，记下它，这是你稍后会用到的 `access_token` 。

### 0x03 获取 channel\_id

按照以下步骤获取 `channel_id`：

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

你需要将 Claude 和 Claude-Interactor 同时拉入频道，才能正常收发消息。

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

### 0x04 获取 Claude 的识别码

一些用可能会遇到发消息时无法 @claude 变蓝的情况，所以我们还需要完成这一步。

你需要按照下图的方式获取识别码：

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

通常来说 Claude 的识别码都是以 `U0` 开头的。

### 0x05 编写配置文件

在 `config.cfg` 中加入以下配置项，添加相关信息：

```toml
[slack]
[[slack.accounts]]
channel_id = "C0XXXXXX:U0xxx" # 这里写你获得的 channel_id:Claude 的识别码 
access_token = "XXXX" # 这里写前面获得的 access_token


```

## 相关设置

**1.使用代理**

这项设置是每个账号独立的。

参考： [#4.-shi-yong-dai-li](jie-ru-openai-de-chatgpt.md#4.-shi-yong-dai-li "mention")

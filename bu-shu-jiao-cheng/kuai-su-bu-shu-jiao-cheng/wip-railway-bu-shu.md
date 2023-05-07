# PaaS 平台部署（Railway）

{% hint style="info" %}
本文的教程只负责 ChatGPT for Bot 的部署，如果你想接入 QQ 平台，需要另外找地方部署 Mirai 或 go-cqhttp。
{% endhint %}

{% hint style="info" %}
我们建议你在自己电脑上根据 Windows 快速部署教程 先部署一次，熟悉流程。
{% endhint %}

PaaS 平台是一种可以直接运行你代码的平台。通过这种方法部署，你不需要实际拥有一个服务器。

本文以 Railway 为例，Railway 是一个 PaaS 平台，你可以在这上面运行 ChatGPT for Bot。  针对免费用户，它提供每个月 500小时（约20天） 的运行时间。&#x20;

## 0x00 开始

点击下面按钮开始部署

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/template/QSxuAE?referralCode=hnDyRG)

如果你还未注册，会看到下面这样一个按钮，点击它并登录 GitHub。



<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

如果你已经登录了，那么点击 Deploy Now，开始部署。

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

接下来，在这里填写配置文件：

{% hint style="info" %}
你可能会注意到，这里的编辑框不能输入多行的文字

所以我们会在后面的步骤中重新填写配置文件。
{% endhint %}

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>



然后点击下方的 Deploy 开始部署。

### 0x01 配置

首先我们要做的就是重新填写配置文件。&#x20;

点击 Variables -> CHATGPT\_FOR\_BOT\_FULL\_CONFIG -> Edit，然后重新粘贴配置文件，点击打勾保存。

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

除了 `CHATGPT_FOR_BOT_FULL_CONFIG` 之外，下面还有一个 `PORT` 变量。

如果你想要接入 Mirai 或者 go-cqhttp，那么需要保证配置中的 `reverse_ws_port` 与 `PORT` 变量的值一致，否则会无法使用。

### 0x02 接入 GO-CQHTTP

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

当你的程序启动以后，会出现一个链接。通过这个链接就可以访问到你的程序。

在 GO-CQHTTP 中，你可以把这个链接填到反向 WebSocket 的 Universal 地址中。

### 0x03 更新

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

如果项目有更新，你可以点击这里的按钮同步最新的代码。&#x20;


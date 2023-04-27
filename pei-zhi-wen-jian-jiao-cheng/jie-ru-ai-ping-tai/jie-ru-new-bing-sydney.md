# 😅 接入 New Bing (Sydney)

New Bing 是我们支持的第二个 AI 模型。

Bing 的设置开始于一行 `[bing]` ，随后每个账号的设置开始于一行 `[[bing.accounts]]`。

## Cookie 获取方法

截止至当前最新的版本， Bing 仅支持 Cookie 的方式登录。

你需要通过电脑浏览器来获得 Bing Cookie，Firefox 请安装[此插件](https://addons.mozilla.org/en-US/firefox/addon/cookie-editor/)，Chrome / Edge 安装[此插件](https://chrome.google.com/webstore/detail/cookie-editor/hlkenndednhfkekhgcdicdfddnkalmdm)。

1. 切换到国外节点
2. 打开 https://bing.com
3. 点开插件
4.  点击下方的 Export 按钮，然后选 Export as JSON

    ![](<../../.gitbook/assets/image (37).png>)
5. 打开下面这个网站，把 JSON 粘贴进去变成一行，然后复制出来：

{% embed url="https://jsonformatter.org/json-minify" %}

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

&#x20;6\. 把最终的结果填入配置文件：

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
需要注意的是，这里用了单引号来包裹 JSON。
{% endhint %}

```toml
[[bing.accounts]]
cookie_content = '你的结果'
```

## 相关设置

### 1.使用代理

这项设置是每个账号独立的。

根据社区反馈，中国大陆的 IP 可能无法直接使用 Bing，具体表现为登录失败，提示：**Authentication failed. You have not been accepted into the beta**。

所以我们建议使用国外的 IP。

参考： [#4.-shi-yong-dai-li](jie-ru-openai-de-chatgpt.md#4.-shi-yong-dai-li "mention")

### 2.Bing 的接入点

{% hint style="info" %}
这项设置是全局生效的（所有账号只需要设置一次）。
{% endhint %}

除了使用代理之外，你还可以通过设置 Bing 接入点的方式来使用 Bing。

你可以使用这个项目来搭建接入点：https://github.com/acheong08/EdgeGPT-Proxy

下面是默认的配置：

```toml
[bing]

# Bing 的 WS 接入点，通常不需要修改
wss_link = "wss://sydney.bing.com/sydney/ChatHub"
# 会话创建的接入点
bing_endpoint = "https://edgeservices.bing.com/edgesvc/turing/conversation/create"
```

如果你访问 Bing 出现问题，可以用下面的接入点配置：

{% hint style="info" %}
警告：

使用第三方接入点时，你的 Bing Cookie 将会被发送至接入点服务器。&#x20;

这会让你的微软账号信息有泄露的风险，请知晓。
{% endhint %}

```toml
[bing]

wss_link = "wss://chatgpt-proxy.lss233.com/sydney/ChatHub"
# 会话创建的接入点
bing_endpoint = "https://chatgpt-proxy.lss233.com/edgesvc/turing/conversation/create"
```

### 3.关闭 Bing 的引用链接、猜你想问和剩余次数

{% hint style="info" %}
这项设置是全局生效的（所有账号只需要设置一次）。
{% endhint %}

如果你觉得这两个东西有点烦，可以关闭他们。

```toml
[bing]

# 在 Bing 的回复后加上猜你想问
show_suggestions = false
# 在 Bing 的回复前加上引用资料
show_references = false
# 在 Bing 的回复后加上剩余次数
show_remaining_count = false
```

### 4. 开启 Bing 画图功能

{% hint style="info" %}
这项设置是全局生效的（所有账号只需要设置一次）。
{% endhint %}

如果你想使用 Bing 画图功能，那么你可以这样开启它：

```toml
[bing]

# 开启 Bing 画图功能
use_drawing = true
```

提示：如果你配置了 Stable Diffusion，那么你需要删除那部分配置，才能触发 Bing 画图。


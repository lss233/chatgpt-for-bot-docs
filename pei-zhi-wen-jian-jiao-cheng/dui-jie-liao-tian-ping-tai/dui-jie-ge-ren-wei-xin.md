# 😁 对接个人微信

目前的个人微信支持由 [lcjqyml/wechatbot](https://github.com/lcjqyml/wechatbot) 项目提供，基于本项目的 HTTP API 功能实现，

## 0x01 开启 HTTP API 服务

在 `config.cfg` 中加入以下配置后，将额外提供 HTTP API 支持。

{% hint style="info" %}
我们建议将本项目部署在国外服务器上，减少网络错误发生的概率。
{% endhint %}

```toml
[http]
host = "0.0.0.0"
# 填写提供服务的端口
port = 8234
# 是否开启调试
debug = false
```

### 注意事项

Docker 用户别忘了将此处配置中的 `port` 的端口号映射出来，以便被访问到。 &#x20;

举个**例子**（只是例子，不代表完全一样，别直接抄）：

<pre class="language-yaml"><code class="lang-yaml">version: '3.4'
services:
<strong>  chatgpt:
</strong>    image: lss233/chatgpt-mirai-qq-bot:browser-version
    restart: always
    environment:
      LANG: 'C.UTF-8'
    ports:
      - 8234:8234 # &#x3C;----- 主要就是加这一项
    volumes:
      - ./config.cfg:/app/config.cfg
      - ./data:/app/data
      - ./presets:/app/presets
</code></pre>

## 0x02 部署 [lcjqyml](https://github.com/lcjqyml)/[**wechatbot**](https://github.com/lcjqyml/wechatbot)

{% hint style="info" %}
我们建议将这个项目部署在国内的服务器上，降低微信被封号的概率。
{% endhint %}

{% hint style="info" %}
这是一个由第三方提供的程序，教程可能会随着项目的发展而过时。

建议参考原项目文档进行部署：[https://github.com/lcjqyml/wechatbot](https://github.com/lcjqyml/wechatbot)
{% endhint %}

此处以 Ubuntu 20.04 系统为例，在安装 Docker 后，执行以下命令：

```bash
docker run -e CHATBOT_PROXY="http://127.0.0.1:8234" lcjqyml/wechatbot:latest
```

将 `127.0.0.1` 换成你部署的 ChatGPT for Bot 项目服务器的 IP，然后按下回车启动，然后扫码登录即可。

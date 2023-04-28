# 😁 对接个人微信

目前的个人微信支持由 [lcjqyml/wechatbot](https://github.com/lcjqyml/wechatbot) 项目提供，基于本项目的 HTTP API 功能实现，

## 0x01 开启 HTTP API 服务

在 `config.cfg` 中加入以下配置后，将额外提供 HTTP API 支持。

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
      - 5001:5001 # &#x3C;----- 主要就是加这一项
    volumes:
      - ./config.cfg:/app/config.cfg
      - ./data:/app/data
      - ./presets:/app/presets
</code></pre>

## 0x02 部署 [lcjqyml](https://github.com/lcjqyml)/[**wechatbot**](https://github.com/lcjqyml/wechatbot)

参考：[https://github.com/lcjqyml/wechatbot](https://github.com/lcjqyml/wechatbot)

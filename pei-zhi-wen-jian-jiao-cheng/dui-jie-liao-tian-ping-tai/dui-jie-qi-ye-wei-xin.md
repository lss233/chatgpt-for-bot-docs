# 🧑🍳 对接企业微信

在 `config.cfg` 中加入以下配置，开启对企业微信的支持：

```toml
[wecom]
# 企业微信相关设置
# 企业微信管理后台网址： https://work.weixin.qq.com/wework_admin/frame
# 企业微信回调地址，需要能够被公网访问
host = "0.0.0.0"
port = 5001
debug = false
# 企业微信应用相关设置
# 企业 ID： 我的企业 -> 企业信息 -> 企业 ID
corp_id = "ww***"
# 应用 AgentId： 应用管理 -> 自建 -> 创建应用 -> AgentId
agent_id = 1000001
# 应用 Secret： 应用管理 -> 自建 -> 创建应用 -> Secret
secret = "abc***"
# API 回调地址请填写 http://公网ip:5001/wechat
# API 令牌： 应用管理 -> 自建 -> 刚刚创建的应用 -> 功能 -> 接收消息 -> 启用API接收 -> 随机生成的 Token
token = "abc***"
# API 加解密密钥： 应用管理 -> 自建 -> 刚刚创建的应用 -> 功能 -> 接收消息 -> 启用API接收 -> 随机生成的 EncodingAESKey
encoding_aes_key = "abc***"
```

### 注意事项

企业微信要求提供一个 API 回调地址到本项目中，所以你可能需要把这个项目部署在有公网 IP 的电脑上（或者使用 frp 等软件进行端口映射）。



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

修改完这个文件后，还要执行：`docker-compose up -d` 来更新容器编排，确保端口映射成功。

当你完成上面的所有操作后，可以在自己的浏览器中打开：`http://你的服务器IP:5001` 看看有没有内容。如果浏览器提示打开失败，说明你的端口映射没有成功。


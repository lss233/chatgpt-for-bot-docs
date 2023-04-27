# 🦠 对接 Mirai

Mirai 协议是我们最初支持的协议。

我们支持 **反向 Websocket 连接**和**正向 Websocket + HTTP 连接**两种方式通过 Mirai 接入 QQ。

## 反向 Websocket 连接时的设置

如果你要使用 Mirai 来连接 QQ，那么需要你在配置文件中这么写：

```toml
[mirai]
# Mirai 相关设置
​
qq = 请填写机器人的 QQ 号
​
manager_qq = 请修改为机器人管理员的QQ号（你自己的 QQ 号）
​
# 以下是和 Mirai 连接所需要的相关设置

# 如果你是小白，或者使用我们提供的快速部署方案，可以不用修改这里的设置
# mirai-http-api 中的 verifyKey
api_key = "1234567890"
# mirai api http 反向连接模式
reverse_ws_host = "0.0.0.0"
reverse_ws_port = 8554
```

在这段配置中，我们使用了 **反向 Websocket** 连接到 Mirai。&#x20;

在这个模式下，本程序启动后会等待 Mirai 主动连接到本程序。

这样你就可以把本程序放在云服务器上，而 Mirai 可以放在自己的电脑上，从而避免触发 QQ 的异地登录保护或者掉线问题。

### mirai-api-http 中的设置

你需要保证这里的配置和 mirai-api-http 中的设置是一致的，我们的程序才能接入 Mirai。

mirai-api-http 的配置文件存放于 `mirai/config/net.mamoe.mirai-api-http`，你可以用记事本打开它。

以我们上面的配置为例， mirai-api-http 的配置文件应该改成这样：

```yaml
adapters:
 - reverse-ws

verifyKey: 1234567890
singleMode: false
cacheSize: 4096
adapterSettings:
  reverse-ws:
    ## 远端 websocket server 地址配置
    destinations:
    - host: localhost
      port: 8554
      path: /
      protocol: ws
      
```

需要注意的是：

* `verifyKey` 的 `1234567890` 要和上面的 `api_key` 保持一致
* `port` 的 `8554` 要和上面的 `reverse_ws_port` 保持一致
*   `host` 的 `localhost` 填写本程序的 IP 地址。这取决于你的部署方式，

    如果是 Docker（或者 Linux 一键部署），那你要改成 `chatgpt` 。

    如果是 Windows，那就保持现在这样，不需要再改了。

## 正向 Websocket + HTTP 方式连接

你也可以使用正向 Websocket + HTTP 的方式来连接到 Mirai。

在这个模式下， 本程序启动成功后会主动连接到 Mirai。&#x20;

如果你要这么做，那就注释掉 `reverse_ws`开头的两行配置，然后加入另外两行配置，就像这样：

```toml
# mirai api http 反向连接模式
# reverse_ws_host = "0.0.0.0"
# reverse_ws_port = 8554
# mirai api http 正向连接模式
# 使用此模式时需注释上面的反向连接模式配置
http_url = "http://localhost:8080"
ws_url = "http://localhost:8080"
```

此处的 `localhost` 是 Mirai 程序的 IP 地址。在 Docker 中，你可以填容器名，在 Windows 同一台机器中，那就填 `localhost`。

通常来说，使用正向连接模式没有什么优点，因此我们觉得你没有必要对这里的配置进行修改。

### mirai-api-http 中的设置

```yaml
adapters:
  - http
  - ws
verifyKey: 1234567890
singleMode: false
cacheSize: 4096
persistenceFactory: 'built-in'
adapterSettings:
  ## HTTP 服务的主机, 端口和跨域设置
  http:
    host: "0.0.0.0"
    port: 8080
    cors: ["*"]

  ## Websocket 服务的主机, 端口和事件同步ID设置
  ws:
    host: "0.0.0.0"
    port: 8080
    reservedSyncId: -1
```

需要注意的是：

* `verifyKey` 的 `1234567890` 要和上面的 `api_key` 保持一致
* `port` 的 `8080`要和上面的 `url` 冒号后面的数字保持一致


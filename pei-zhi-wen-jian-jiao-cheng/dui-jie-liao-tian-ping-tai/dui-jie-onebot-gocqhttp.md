# 🙇 对接 OneBot (go-cqhttp)

OneBot 协议可以用于对接 go-cqhttp 等机器人框架。

如果你要使用 OneBot 协议，那么你就将 `config.cfg` 中的 `[mirai]` 块删除，然后加入以下配置：

```properties
[onebot]
qq=请修改为你机器人的QQ号
manager_qq = 请修改为机器人管理员的QQ号

reverse_ws_host = "0.0.0.0"
reverse_ws_port = 8566
```

就可以使用 go-cqhttp 或者其他支持 OneBot 协议的程序和 ChatGPT 聊天！

## go-cqhttp 的设置教程

如果你在搭建过程中遇到问题，可以看：

[gocqhttp-qi-dong-guo-cheng-zhong-de-chang-jian-wen-ti.md](../../chang-jian-wen-ti-jie-da/gocqhttp-qi-dong-guo-cheng-zhong-de-chang-jian-wen-ti.md "mention")

OneBot 是一个典型的支持 OneBot 协议的平台。

如果你在使用 go-cqhttp，那就可以不需要理会 Mirai 了。

{% hint style="info" %}
如果你通过 GO-CQHTTP 的 Linux 部署脚本来安装的这个项目，那么你可以跳过这一段教程。
{% endhint %}

### 1. 下载 go-cqhttp

你可以在这里下载最新的 go-cqhttp：[https://github.com/Mrs4s/go-cqhttp/releases](https://github.com/Mrs4s/go-cqhttp/releases)

### 2. 初始化 go-cqhttp

解压并启动 go-cqhttp，选 `3` 后回车，退出程序。

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

### 3. 设置 go-cqhttp

编辑 go-cqhttp 的 `config.yaml`，设置机器人的 QQ 号和反向 Universal 地址 （这个反向 Universal 地址和前面的 `reverse_ws_host` 、`reverse_ws_port` ）有关。

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

这里的 universal 地址的写法如下：

* 如果你的 go-cqhttp 和 chatgpt 在同一台机器上，那么就写： `ws://localhost:8566/ws` ，这里的 8566 和 `reverse_ws_port`的值是一样的。
* 如果你的 go-cqhttp 和 chatgpt 在不同的机器上，那么就在上面的基础上，把 `localhost` 改成你 chatgpt 服务器的 IP 地址。

### 4. 映射 \`reverse\_ws\_port\` 端口

这一步是使用 Docker 部署的同学才需要做的， Windows 用户可以直接跳过。 &#x20;

打开 docker-compose.yaml，在图中的位置加入下面这么一行：

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

然后执行 `docker-compose up -d` 更新即可。

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### 5. 启动 go-cqhttp，生成配置文件

首次启动时我们不要登录 QQ，我们只是需要它生成的 `device.json`文件。

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

### 6. 打开 device.json，修改协议

找到 `protocol`，把后面的数字改成 2，然后保存并退出即可。&#x20;

这会让 go-cqhttp 使用 Android Watch 协议进行登录。

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

### 7. 启动 go-cqhttp，扫码并登录

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

### 注意事项

这个go-cqhttp 的扫码登录，是需要你自己的手机 QQ 和 go-cqhttp 在同一个网络环境下的才能成功的。

这个问题有两种解决方法：

#### 方法一：代理

在你的服务器上搭个代理，让你的手机通过代理再进行扫码。

#### 方法二：同步 session.token 文件

在你自己的电脑上用同样的 device.json 来登陆一次 go-cqhttp，扫码登录成功后，把这个 session.token 放到服务器上

#### 方法三：在自己电脑运行

你自己的电脑上跑 go-cqhttp，然后在服务器跑 chatgpt

然后通过 go-cqhttp 的反向 websocket 功能，让你电脑上的 go-cqhttp 连接上服务器的 chatgpt 程序。

唯一要修改的就是：在第2步里面将 `127.0.0.1` 就换成你运行 chatgpt 服务器的公网 IP 地址。

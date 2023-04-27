# 🎨 ChatGPT 启动过程中的常见问题

下面是你在启动 ChatGPT 中可能会遇到的常见问题和解决方法方案：

#### 1. 使用邮箱密码登录 OpenAI 时，出现：登录失败! 连接 OpenAI 服务器失败,请更换代理节点重试

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

原因及解决方法：

{% embed url="https://github.com/lss233/chatgpt-mirai-qq-bot/issues/462" %}

#### 2. 启动时出现：配置文件有误，请重新修改！

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

这是因为你的 `config.cfg` 写的有问题。你可以用下面这个工具帮你检查：

{% embed url="https://www.toml-lint.com/" %}

#### 3. 未能使用所配置的账号激活 sessionKey，请检查 mirai\_session 配置

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

出现这个问题的原因可能是因为你启动 Mirai 的时候没有登录 QQ。

解决方法就是在 Mirai 那边登录机器人 QQ，然后重新开一下我们这个程序。

#### 3. 使用过程中出现：ClientConnectorError(ConnectionKey(host='localhost.....

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

这是因为我们的程序没有连接上 Mirai。请检查一下 Mirai 是不是启动了，并且登录了QQ。 &#x20;

如果 Mirai 确实没问题，请按照 [#zheng-xiang-websocket-+-http-fang-shi-lian-jie](../pei-zhi-wen-jian-jiao-cheng/dui-jie-liao-tian-ping-tai/dui-jie-mirai.md#zheng-xiang-websocket-+-http-fang-shi-lian-jie "mention") 检查你的配置。


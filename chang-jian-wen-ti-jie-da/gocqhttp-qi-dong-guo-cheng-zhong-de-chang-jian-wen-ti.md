# 🧳 go-cqhttp 启动过程中的常见问题

#### 1. 连接到反向 WebSocket Universal 服务器 ws://localhost:8566/ws 时出现错误： dial tcp...

<figure><img src="../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>

这是因为 go-cqhttp 没法成功连接上我们的程序。请检查一下我们的程序是不是启动了。

如果程序确实有在运行，那就按照 [#gocqhttp-de-she-zhi-jiao-cheng](../pei-zhi-wen-jian-jiao-cheng/dui-jie-liao-tian-ping-tai/dui-jie-onebot-gocqhttp.md#gocqhttp-de-she-zhi-jiao-cheng "mention") 检查一下你的配置。

#### 2.新版go-cqhttp

启动时显示未签名服务器，账号风控等。可以参考

{% embed url="https://github.com/fuqiuluo/unidbg-fetch-qsign" %}

{% file src="../.gitbook/assets/qsign-api喂饭教程（改编自moki）.docx" %}

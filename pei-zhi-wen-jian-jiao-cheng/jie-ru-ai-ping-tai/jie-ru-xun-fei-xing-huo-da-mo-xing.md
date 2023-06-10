# ⭐ 接入 讯飞星火大模型

讯飞的星火大模型申请当场通过。

星火模型的设置开始于一行 `[xinghuo]` ，随后每个账号的设置开始于一行 `[[xinghuo.accounts]]`。每个账号填写 `ssoSessionId` 即可使用。

```toml
[[xinghuo.accounts]]
ssoSessionId = "xxxxx-xxxx-xxxx-xxxxx"
```

## ssoSessionId 获取方法

1. 打开星火模型官网，然后登录：[https://xinghuo.xfyun.cn/](https://xinghuo.xfyun.cn/)
2. 登录完成后，点击[这里](https://xinghuo.xfyun.cn/)回到首页。
3. 按下 F12，打开开发人员工具（DevTools），点 应用（Application），在左边找到 Cookie
4. 找到 `ssoSessionId` 复制它的值即可。

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

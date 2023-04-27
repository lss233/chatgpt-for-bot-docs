# 📎 接入 AI 平台

我们的一个程序实例可以接入多个 AI 平台。

我们所有的 AI 平台都支持多账号登录，你可以配置多种不同的 AI 平台，然后通过指令来进行切换。

以下面 OpenAI 的配置为例，添加多账号的写法如下：

```toml
# OpenAI 相关设置
[openai] # 这一行必写

# 第 1 个 OpenAI 账号的登录信息
[[openai.accounts]] # 这一行必须跟在 [openai] 的后面
# 里面是一些设置

# 第 2 个 OpenAI 账号的登录信息
[[openai.accounts]]
# 里面是一些设置

# 第 3 个 OpenAI 账号的登录信息
[[openai.accounts]]
# 里面是一些设置
```

### 接入 OpenAI

{% content-ref url="jie-ru-openai-de-chatgpt.md" %}
[jie-ru-openai-de-chatgpt.md](jie-ru-openai-de-chatgpt.md)
{% endcontent-ref %}

### 接入 New Bing （Sydney）

{% content-ref url="jie-ru-new-bing-sydney.md" %}
[jie-ru-new-bing-sydney.md](jie-ru-new-bing-sydney.md)
{% endcontent-ref %}

### 接入 Google Bard

{% content-ref url="jie-ru-google-bard.md" %}
[jie-ru-google-bard.md](jie-ru-google-bard.md)
{% endcontent-ref %}

### 接入 ChatGLM

{% content-ref url="jie-ru-chatglm.md" %}
[jie-ru-chatglm.md](jie-ru-chatglm.md)
{% endcontent-ref %}

### 接入 文心一言

{% content-ref url="jie-ru-wen-xin-yi-yan.md" %}
[jie-ru-wen-xin-yi-yan.md](jie-ru-wen-xin-yi-yan.md)
{% endcontent-ref %}

### 接入 Poe.com

{% content-ref url="jie-ru-poe.com.md" %}
[jie-ru-poe.com.md](jie-ru-poe.com.md)
{% endcontent-ref %}

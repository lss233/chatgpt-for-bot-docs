# 百度云回复审核

如果你担心机器人发送的消息存在敏感内容导致封号，可以配置百度云审核。

<pre class="language-toml"><code class="lang-toml">[baiducloud]
<strong>
</strong><strong># 是否启动百度云内容安全审核
</strong>check = false

# 百度云API_KEY 24位英文数字字符串
baidu_api_key = ""

# 百度云SECRET_KEY 32位的英文数字字符串
baidu_secret_key =""

# 不合规消息自定义返回
prompt_message = "[百度云]请珍惜机器人，当前返回内容不合规"
</code></pre>

你可以在这里注册百度云审核服务：

{% embed url="http://console.bce.baidu.com/ai/#/ai/antiporn/overview/index" %}

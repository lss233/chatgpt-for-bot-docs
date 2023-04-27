# Edge TTS 语音接入教程

接入 Edge TTS 需要在配置文件中添加下面几行配置：

```toml
[text_to_speech]

# 引擎名填写这一个
# 设置后可以使用 Edge 的语音转文字功能
engine = "edge"

# 音色名
default = "zh-CN-XiaoxiaoNeural"
```

## 依赖

如果你想在 QQ 上使用这个引擎，需要安装 ffmpeg。

Windows 参考：

{% embed url="https://www.jianshu.com/p/5015a477de3c" %}

Linux ：建议你直接问 ChatGPT：`XXX 系统怎么装 ffmpeg？`

Docker: 自带，无需安装。

## 音色

你可以在这里查看支持的音色：

{% embed url="https://www.cnblogs.com/v3ucn/p/17186731.html" %}

在这里可以试听：

{% embed url="https://speech.microsoft.com/portal/voicegallery" %}

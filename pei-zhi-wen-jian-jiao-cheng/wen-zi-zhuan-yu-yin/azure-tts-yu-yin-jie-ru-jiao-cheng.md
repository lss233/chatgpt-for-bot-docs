# Azure TTS 语音接入教程

接入 Azure TTS 需要在配置文件中添加下面几行配置：

```toml
[text_to_speech]

# 引擎名填写这一个
# 设置后可以使用 Azure 的语音转文字功能
engine = "azure"

# 音色名
default = "zh-CN-XiaoyouNeural"

[azure]
tts_speech_key = '你的密钥'
tts_speech_service_region = '你的位置/区域'
```

配置文件中提到的两个值的获取方法请参考：

{% embed url="https://blog.csdn.net/he99774/article/details/126653141" %}

你可以在这里查看支持的音色：

{% embed url="https://learn.microsoft.com/zh-CN/azure/cognitive-services/speech-service/language-support?tabs=tts#neural-voices" %}

在这里试听：

{% embed url="https://speech.microsoft.com/portal/voicegallery" %}

# VITS 语音接入教程

我们使用 MoeGoe-Simple-API 作为 VITS 语音的后端。

接入 MoeGoe-Simple-API 的 VITS TTS 需要在配置文件中添加下面几行配置：

```toml
[text_to_speech]

# 引擎名填写这一个
engine = "vits"

# 角色 ID
default = "0"

[vits]
# 后端接口地址
api_url = "xxxx"

# 语音速度
speed = 1.4

# 目标语言
lang = "zh"

# 语音生成超时时间
timeout = 30
```

### 配置项介绍

#### 后端接口地址

此处填写你搭建好的 MoeGoe-Simple-API 的接口地址，`http://IP:端口号/voice` 。

你可以使用我的接口地址：`http://lss.mchank.cn:23456/voice` 来体验效果，但我不保证这个接口的稳定性（可能随时会关闭）。

#### 角色ID

和你的模型有关，具体请见 MoeGoe-Simple-API  的文档。

#### 语音速度

这个值越大，语速越慢。经测试发现 `1.4` 是一个比较均衡的值。

#### 目标语言

即想要转换成语音的语言，支持：

* zh - 中文
* ja - 日文
* mix - 混合

#### 生成超时时间

等待多久放弃生成本次语音，单位为秒。

### MoeGoe-Simple-API 搭建教程

{% hint style="info" %}
**注意**

此项目为第三方提供的项目，教程已经因为原项目的发展而**过时**，建议参考原项目的文档进行搭建。

项目地址： [https://github.com/Artrajz/MoeGoe-Simple-API](https://github.com/Artrajz/MoeGoe-Simple-API)
{% endhint %}

搭建此 VITS 后端需要至少 5GB 的磁盘空间和一个较好的 CPU（或 GPU）。

如果你是在 Windows 上进行部署，可以直接项目的 README 进行部署。

#### 模型下载

你可以在这里下载一些训练好的 VITS 模型：

{% embed url="https://github.com/CjangCjengh/TTSModels" %}

#### Docker 部署

你可以在 docker-compose.yaml 中加入以下内容：

```yaml
  moegoe:
    image: lss233/moegoe-simple-api:latest
    restart: always
    ports:
      - 23456:23456
    environment:
      LANG: 'C.UTF-8'
    volumes:
      - ./Model:/app/Model
      - ./moegoe-config.json:/app/config.json
```

然后新建一个叫做 Model 的文件夹，在里面放你下载好的模型文件。

~~然后写一个叫做 `moegoe-config.json` 的配置文件：~~

```json
[
        ["./Model/1374_epochs.pth", "./Model/config.json"]
]
```

~~这里的 `./Model/1374_epochs.pth` 和 `./Model/config.json` 就是你放进去的模型文件。~~

完成之后，输入 `docker-compose up -d` 更新容器编排。 &#x20;

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

然后你的接口地址就是： `http://moegoe:23456/voice`

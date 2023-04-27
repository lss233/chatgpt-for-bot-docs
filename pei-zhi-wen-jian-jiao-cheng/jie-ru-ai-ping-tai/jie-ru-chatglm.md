# 🧑🎓 接入 ChatGLM

ChatGLM 是由清华开源的离线语言模型，你可以用自己的服务器来运行语言模型。

ChatGLM 的设置开始于一行 `[chatglm]` ，随后每个账号的设置开始于一行 `[[chatglm.accounts]]`。

**API 访问**

我们使用 ChatGLM 项目中 `api.py` 所提供的 Web API 来访问 ChatGLM。

```toml
[[chatglm.accounts]]
# ChatGLM 的接口地址，搭建方法见下
api_endpoint = "http://127.0.0.1:8000"
# 最大记忆的对话轮数
max_turns=10
# 请求超时时间（单位：秒）
timeout=360
```

**API 搭建方法**

```bash
# 下载项目
git clone https://github.com/THUDM/ChatGLM-6B.git
cd ChatGLM-6B
# 安装依赖
pip install -r requirements.txt
pip install fastapi uvicorn
# 启动
python api.py
```

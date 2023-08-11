# ImmersiveL

ImmersiveL 是一个连接全球各种语言的框架和模型中心，它是开放且自由的。

现在，ImmersiveL 应用程序是基于 Deepspeed 的中英双向翻译框架。主要结构位于 `app` 目录中，由 Python 3.8+ 环境、Flask、Deepspeed 和 PyTorch 组成。

**目前的第一个模型是基于 bloomz 模型进行训练的，其许可证可以在[此处](https://bigscience.huggingface.co/blog/the-bigscience-rail-license)找到。Apache 许可证适用于此模型的派生部分和此仓库中的其他源代码文件。**

🌐 **[中文阅读](README_CN.md)**

## 开始使用

1. **克隆仓库并设置环境**

   首先，将 ImmersiveL 仓库克隆到您的本地计算机：

   ```bash
   git clone https://github.com/immersive-translate/ImmersiveL.git
   ```

   克隆后，导航到 `app` 目录，并安装 `requirements.txt` 中列出的所有必要的包：

   ```bash
   cd ImmersiveL/app
   pip install -r requirements.txt
   ```

2. **运行应用程序**

   使用以下命令使用 Deepspeed 启动应用程序：

   ```bash
   deepspeed --num_gpus 1 app.py
   ```

   当您看到类似 `* Running on [IP 地址]` 的消息，就表示应用程序已成功启动。

## 使用 ImmersiveL

应用程序启动并运行后，您可以轻松使用提供的翻译端点。

### 示例 1：从中文翻译成英文

```bash
curl -X POST -H "Content-Type: application/json" -d '{"text": "欧洲经济增长仍面临较大挑战", "task": "zh2en"}' http://localhost:7000/translate
```

### 示例 2：从英文翻译成中文

```bash
curl -X POST -H "Content-Type: application/json" -d '{"text": "Want to live longer? Play with your grandkids. It’s good for them, too.", "task": "en2zh"}' http://localhost:7000/translate
```

## API 示例

### 请求

```json
{
  "text": "欧洲经济增长仍面临较大挑战",
  "task": "zh2en"  // 使用 "zh2en" 进行中文到英文的翻译，使用 "en2zh" 进行英文到中文的翻译。
}
```

### 响应

对于给定的请求：

```json
{
  "data": {
    "translation": "欧洲的经济增长继续面临重大挑战",
    "info": {}
  }
}
```

### 参数描述

#### 请求参数

- `text`: 您希望翻译的文本。
- `task`: 定义翻译方向。使用 "zh2en" 进行中文到英文的翻译，使用 "en2zh" 进行英文到中文的翻译。

#### 响应参数

- `data`:
  - `translation`: 翻译后的输出文本。
  - `info`: 关于请求的其他详细信息，包括使用的模型、原始文本等。

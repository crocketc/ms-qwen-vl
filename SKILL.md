---
name: ms-qwen-vl
description: 调用魔搭社区（ModelScope）Qwen3-VL 多模态 API 进行视觉解析。使用 OpenAI SDK 兼容方式调用，支持图片内容描述、OCR 文字提取、视觉问答、对象检测等功能。用户提到"魔搭"、"ModelScope"、"Qwen-VL"、"多模态视觉"、"解析图片"等关键词时应触发。
---

# MS-Qwen-VL Skill

基于 ModelScope Qwen3-VL 系列模型的多模态视觉识别技能，使用 OpenAI SDK 兼容方式调用。

## 功能特点

- **OpenAI SDK 兼容**：使用标准 OpenAI SDK 调用 API
- **多种任务支持**：图像描述、OCR、视觉问答、目标检测、图表解析
- **双模型模式**：默认快速模型（30B）+ 精细高精度模型（235B）
- **灵活输入**：支持本地图片和 URL

## 安装与配置

```bash
# 安装依赖
pip install -r requirements.txt

# 配置 API Key
cp .env.example .env
```

编辑 `.env` 文件，填入从 https://modelscope.cn/my/myaccesstoken 获取的 API Key：

```
MODELSCOPE_API_KEY=your_api_key_here
```

## 快速使用

```bash
# 图像描述（默认）
python scripts/ms_qwen_vl.py image.jpg

# OCR 文字识别
python scripts/ms_qwen_vl.py image.jpg --task ocr

# 视觉问答
python scripts/ms_qwen_vl.py image.jpg --task ask --question "图片里有什么？"

# 使用精细模式（235B 模型）
python scripts/ms_qwen_vl.py image.jpg --task describe --precise
```

Python 代码调用：

```python
from scripts.ms_qwen_vl import analyze_image

result = analyze_image("image.jpg", task="ocr")
print(result)
```

## 任务类型

| 任务 | 参数 | 说明 |
|------|------|------|
| 图像描述 | `describe` | 详细描述图片内容（默认） |
| OCR 识别 | `ocr` | 识别图片中的文字 |
| 视觉问答 | `ask` | 回答关于图片的问题 |
| 目标检测 | `detect` | 检测图片中的物体 |
| 图表解析 | `chart` | 解析图表数据 |

## 环境变量

| 变量名 | 说明 |
|--------|------|
| `MODELSCOPE_API_KEY` | API 密钥（必需） |
| `MODELSCOPE_MODEL` | 默认模型（可选） |
| `MODELSCOPE_MODEL_PRECISE` | 精细模式模型（可选） |

## Resources

### scripts/

**ms_qwen_vl.py** - 核心解析脚本，提供 `analyze_image()` 统一接口

### references/

**api-guide.md** - OpenAI SDK 兼容调用方式详细说明
**models.md** - Qwen3-VL 系列模型及推荐使用场景

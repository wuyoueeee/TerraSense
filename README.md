
# 🛰️ TerraSense AI (Local Edition) - 基于多模态大模型的遥感影像分析与语义理解


代码获取：[https://mbd.pub/o/bread/YZWZl5xuag==](https://mbd.pub/o/bread/YZWZl5xuag==)

项目展示：
[![视频封面](https://i-blog.csdnimg.cn/direct/3cc050a89cb546f38beccef9c64c27d2.png)](https://www.bilibili.com/video/BV1bzSKB9EVL/)

**TerraSense AI (Local Edition)** 是一个基于多模态大模型的遥感影像分析与语义理解。
它完全移除了云端依赖，通过 **Ollama** 调用本地部署的多模态大模型（如 **LLaVA**, **Moondream**），实现数据不离网的科研级分析。

系统具备 **语义生成、目标识别、空间感知、地物分类、时序分析** 五大核心能力，并支持生成分析报告。

---
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/3cc050a89cb546f38beccef9c64c27d2.png#pic_center)

## 📚 目录 (Table of Contents)

- [核心功能](#-核心功能-features)
- [系统架构](#-系统架构-architecture)
- [快速部署](#-快速部署-quick-start)
- [本地模型指南](#-本地模型指南-local-models)
- [常见问题](#-常见问题-faq)

---

## 🌟 核心功能 (Features)

1.  **🛡️ 纯本地运行**: 所有推理在本地 GPU/CPU 上完成，零数据泄露风险。
2.  **📝 全维语义解译**: 自动生成专业的遥感图像描述。
3.  **🎯 目标识别与定位**: 识别关键目标（车辆、建筑等）并在前端进行可视化高亮（支持多目标边界框）。
4.  **🗺️ 地物分类**: 统计地表覆盖类型占比。
5.  **📄 报告生成**: 一键生成离线 PDF 态势分析报告。

---

## 🏗️ 系统架构 (Architecture)

本系统采用前后端分离的本地化架构：

*   **Frontend**: React + Vite (运行于浏览器)
*   **Inference Engine**: Ollama (运行于本地后台)
*   **Communication**: HTTP (REST API)

### 提示词工程 (Prompt Engineering)
针对本地小参数模型（如 LLaVA 7b）遵循指令能力较弱的问题，系统内置了 **One-Shot Prompting** 策略，通过提供具体的 JSON 样本，强制模型输出结构化数据，大幅提升了分析的成功率。

---

## 🚀 快速部署 (Quick Start)

### 1. 准备 Ollama 环境
1.  下载并安装 [Ollama](https://ollama.com)。
2.  拉取视觉模型：
    ```bash
    ollama pull llava
    ```
3.  **关键：启动允许跨域的服务**
    *   **Windows (PowerShell)**:
        ```powershell
        $env:OLLAMA_ORIGINS="*"; ollama serve
        ```
    *   **Mac/Linux**:
        ```bash
        OLLAMA_ORIGINS="*" ollama serve
        ```
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/79b96270ec9246ebaaeb7bae781bd5ea.png#pic_center)

### 2. 启动前端应用
```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev
```
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/0d2129604b4246c08745f3e5c3f490b1.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c944f57b34ce4db1aa66714db0f20c28.png#pic_center)

### 3. 使用系统
1.  打开浏览器访问 `http://localhost:5173`。
2.  在右上角设置中，确认 API 地址为 `http://localhost:11434`，模型选择 `llava`。
3.  上传遥感影像即可开始分析。

---

## 🏠 本地模型指南 (Local Models)

本系统推荐使用以下模型：

| 模型名称            | 描述                     | 显存需求 | 推荐场景           |
| :------------------ | :----------------------- | :------- | :----------------- |
| **llava** (7b)      | 均衡型，指令遵循能力较好 | 8GB+     | 通用解译、目标识别 |
| **moondream**       | 轻量级，速度极快         | 4GB+     | 简单描述、快速概览 |
| **llama3.2-vision** | 最新一代，性能更强       | 12GB+    | 复杂场景推理       |

---



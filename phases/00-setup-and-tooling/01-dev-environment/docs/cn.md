# 开发环境

> 你的工具塑造你的思维方式。一次配置好，终身受益。

**类型：** 构建
**语言：** Python、Node.js、Rust
**前置条件：** 无
**预计时间：** 约 45 分钟

## 学习目标

- 从零搭建 Python 3.11+、Node.js 20+ 和 Rust 工具链
- 配置虚拟环境和包管理器，实现可复现的构建
- 通过 CUDA/MPS 验证 GPU 可用性，并运行一次测试张量运算
- 理解四层技术栈：系统层、包管理层、运行时层、AI 库层

## 问题所在

你即将通过 200+ 节课学习 AI 工程，涉及 Python、TypeScript、Rust 和 Julia。如果你的环境是坏的，每一节课都会变成与工具链的搏斗，而不是学习本身。

大多数人会跳过环境配置这一步。然后花上数小时调试 import 错误、版本冲突以及缺失的 CUDA 驱动。我们要一次性、正确地搞定这件事。

## 核心概念

AI 工程环境由四层组成：

```mermaid
graph TD
    A["4. AI/ML 库层\nPyTorch、JAX、transformers 等"] --> B["3. 语言运行时层\nPython 3.11+、Node 20+、Rust、Julia"]
    B --> C["2. 包管理器层\nuv、pnpm、cargo、juliaup"]
    C --> D["1. 系统基础层\n操作系统、shell、git、编辑器、GPU 驱动"]
```

我们自下而上安装。每一层都依赖它下面的那一层。

## 动手构建

### 第 1 步：系统基础

检查你的系统并安装基础工具。

```bash
# macOS
xcode-select --install
brew install git curl wget

# Ubuntu/Debian
sudo apt update && sudo apt install -y build-essential git curl wget

# Windows（使用 WSL2）
wsl --install -d Ubuntu-24.04
```

### 第 2 步：使用 uv 管理 Python

我们使用 `uv` —— 它比 pip 快 10-100 倍，并且能自动处理虚拟环境。

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh

uv python install 3.12

uv venv
source .venv/bin/activate  # Windows 上使用 .venv\Scripts\activate

uv pip install numpy matplotlib jupyter
```

验证：

```python
import sys
print(f"Python {sys.version}")

import numpy as np
print(f"NumPy {np.__version__}")
a = np.array([1, 2, 3])
print(f"向量: {a}，自身点积: {np.dot(a, a)}")
```

### 第 3 步：使用 pnpm 管理 Node.js

用于 TypeScript 相关课程（Agent、MCP Server、Web 应用）。

```bash
curl -fsSL https://fnm.vercel.app/install | bash
fnm install 22
fnm use 22

npm install -g pnpm

node -e "console.log('Node', process.version)"
```

### 第 4 步：Rust

用于性能关键的课程（推理、系统编程）。

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

rustc --version
cargo --version
```

### 第 5 步：Julia（可选）

用于 Julia 擅长的数学密集型课程。

```bash
curl -fsSL https://install.julialang.org | sh

julia -e 'println("Julia ", VERSION)'
```

### 第 6 步：GPU 配置（如果你有 GPU）

```bash
# NVIDIA
nvidia-smi

# 安装支持 CUDA 的 PyTorch
uv pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
```

```python
import torch
print(f"CUDA 可用: {torch.cuda.is_available()}")
if torch.cuda.is_available():
    print(f"GPU: {torch.cuda.get_device_name(0)}")
```

没有 GPU？没关系。大多数课程都可以在 CPU 上运行。对于训练密集型课程，可以使用 Google Colab 或云 GPU。

### 第 7 步：验证一切

运行验证脚本：

```bash
python phases/00-setup-and-tooling/01-dev-environment/code/verify.py
```

## 使用指南

你的环境现在已经准备好应对本课程的所有内容。以下是各语言的使用场景：

| 语言 | 使用阶段 | 包管理器 |
|----------|---------|-----------------|
| Python | 第 1-12 阶段（机器学习、深度学习、NLP、计算机视觉、音频、大语言模型） | uv |
| TypeScript | 第 13-17 阶段（工具、Agent、Swarms、基础设施） | pnpm |
| Rust | 第 12、15-17 阶段（性能关键系统） | cargo |
| Julia | 第 1 阶段（数学基础） | Pkg |

## 交付物

本课程产出一个验证脚本，任何人都可以运行它来检查自己的环境配置。

参见 `outputs/prompt-env-check.md`，其中包含一个提示词模板，可帮助 AI 助手诊断环境问题。

## 练习

1. 运行验证脚本并修复所有失败项
2. 为本课程创建一个 Python 虚拟环境并安装 PyTorch
3. 用四种语言各写一个 "hello world" 并分别运行

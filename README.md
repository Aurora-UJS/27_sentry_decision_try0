# cpp_dev_template_repository

![C++](https://img.shields.io/badge/Standard-C%2B%2B20-blue.svg)
![Clang](https://img.shields.io/badge/Compiler-Clang%2020-orange.svg)
![Build](https://img.shields.io/badge/Build-CMake%20%2B%20Ninja-brightgreen.svg)
![Environment](https://img.shields.io/badge/Env-DevContainer-007ACC.svg)

这是一个开箱即用、工业级的 C++ 机器人软件开发模板。它内置了高度一致的开发环境、自动化的代码规范检查以及现代 C++ 的包管理工具。

**目标**：让你只需关注核心算法和控制逻辑，彻底告别“环境配置地狱”和“代码格式打架”。

## ✨ 核心特性 (Features)

* **零污染开发环境**：基于 `.devcontainer`，使用 Ubuntu 22.04 容器隔离开发，宿主机无需安装任何 C++ 依赖。
* **现代 C++ 标准**：全局强制使用 **C++20**，开启最严格的编译警告。
* **极速编译链**：默认搭载 **Clang 20** 编译器，配合 **LLD** 链接器与 **Ninja** 构建系统。
* **绝对一致的代码规范**：内置 `.clang-format` (Google 风格微调)，并通过 `pre-commit` **强行锁死 v20.1.0 版本**，保证全员代码风格 100% 一致。
* **无感基建挂载**：只需运行 CMake，底层的 Git 提交拦截钩子就会在后台自动安装生效。
* **依赖管理**：预置 **Conan 2.0**，默认集成 `fmt` 和 `spdlog`（现代 C++ 必备的高性能日志输出库）。

---

## 🏃‍♂️ 快速起步 (Quick Start)

### 1. 创建你的项目
请点击仓库右上角的 **"Use this template"** 按钮，生成你自己的模块仓库（例如 `auto_aim_solver`）。

### 2. 克隆到本地
```bash
git clone git@github.com:YourOrg/your_new_repo.git
cd your_new_repo
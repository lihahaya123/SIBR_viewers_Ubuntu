

---

# SIBR_viewers Ubuntu 安装与构建指南

> **SIBR_viewers** 是一个面向图像基渲染（Image-Based Rendering, IBR）研究的开源系统，包含多种渲染算法与数据处理工具。  
> 本指南适用于 Ubuntu 20.04/22.04 及类似 Linux 发行版。

---

## 1. 许可协议

本项目仅限非商业科研用途，详细条款请参见 [LICENSE.md](./LICENSE.md)。

---

## 2. 依赖环境

### 2.1 系统依赖

请先更新系统并安装以下依赖：

```bash
sudo apt update
sudo apt install -y build-essential cmake git pkg-config \
    libgl1-mesa-dev libglew-dev libassimp-dev libopencv-dev \
    libboost-all-dev libffmpeg-dev libopenmp-dev libembree-dev \
    libegl1-mesa-dev libglfw3-dev doxygen python3 python3-pip \
    python3-opencv python3-numpy python3-scipy python3-pillow \
    imagemagick
```

> **说明：**
> - 推荐使用 Ubuntu 20.04 及以上版本。
> - 若需 GPU 加速渲染，建议安装 NVIDIA 驱动及 CUDA Toolkit（可选）。
> - `libembree-dev`、`libegl1-mesa-dev`、`libglfw3-dev` 仅部分模块需要，建议一并安装。

### 2.2 Python 依赖

部分数据处理脚本依赖 Python 包：

```bash
pip3 install pymeshlab pillow opencv-python numpy scipy
```

---

## 3. 获取源码

```bash
git clone https://gitlab.inria.fr/sibr/sibr_core.git
cd sibr_core
```
或直接使用你当前的源码目录。

---

## 4. 编译构建

### 4.1 创建构建目录

```bash
mkdir build
cd build
```

### 4.2 配置 CMake

```bash
cmake .. -DCMAKE_BUILD_TYPE=Release
```

如需自定义安装路径，可添加 `-DCMAKE_INSTALL_PREFIX=/your/path`。

### 4.3 编译与安装

```bash
make -j$(nproc)
make install
```

编译产物默认安装到 `install/` 目录。

---

## 5. 运行与测试

### 5.1 运行示例

1. 下载官方数据集（如 sibr-museum-front）：

    ```bash
    wget https://repo-sam.inria.fr/fungraph/sibr-datasets/museum_front27_ulr.zip
    unzip museum_front27_ulr.zip -d DATASETS_PATH
    ```

2. 进入安装目录并运行：

    ```bash
    cd install/bin
    ./sibr_ulrv2_app --path ../DATASETS_PATH/sibr-museum-front
    ```

### 5.2 交互说明

- 默认支持 WASD/trackball 等多种交互模式，具体请参考[官方文档](https://sibr.gitlabpages.inria.fr/docs/nightly/howto_sibr_useful_objects.html)。

---

## 6. 文档生成（可选）

如需生成开发文档：

```bash
sudo apt install doxygen
cd docs
cmake .
make DOCUMENTATION
# 文档生成于 install/docs/index.html
```

---

## 7. 常见问题

- **依赖缺失/找不到库**：请确认所有依赖已正确安装，部分库如 OpenCV、Boost 需较新版本。
- **OpenGL/GLFW 报错**：请确保已安装显卡驱动及相关 OpenGL 库。
- **Python 脚本报错**：请检查 Python 依赖是否齐全，建议使用 Python 3.8 及以上版本。

---

## 8. 参考与支持

- [SIBR 官方文档](https://sibr.gitlabpages.inria.fr)
- [数据集下载](https://repo-sam.inria.fr/fungraph/sibr-datasets/)
- 问题反馈请邮件联系：sibr@inria.fr


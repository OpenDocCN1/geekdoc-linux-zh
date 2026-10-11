
![](img/5cfcf2f4448dccdd1c5c2a2851544557_32_0.png)

## 开始

从你的发行版开始菜单打开“驱动设置”。选择“使用来自 Nvidia-Driver-525（专有）的 Nvidia Driver 元包”以开始你的发行版使用硬件厂商加速驱动的旅程。请记住，使用这种厂商提供的软件包驱动会污染内核，并且在某些高可靠性或高信任计算环境中是不允许的。

更新 GPU 驱动通常能带来显著的性能提升。遗憾的是，包管理器往往需要一段时间才能反映厂商提供的更新，因此建议手动干预。前往 `https://developer.nvidia.com/cuda-downloads` 并按照提供的说明安装所选驱动。

这种下载和部署过程通常不会更新当前活动的 Linux 安装工作环境，因此现在请重启。此外，Nvidia 驱动有点迟缓。首先，即使正确安装并完美工作的驱动，也常常因为缺少符号链接而无法被 AI 应用程序找到。幸运的是，解决这个问题的方法很简单：`~/stable-library& sudo ln -s /usr/local/cuda-12.1/bin/ /usr/bin`

完成后，应执行评估以获取更多详细信息。`NVCC` – Nvidia Cuda 编译器 – 非常适合这类任务；在我们的机器上，输出如下所示：

```
$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2023 NVIDIA Corporation
Built on Tue_Feb_ 7_19:32:13_PST_2023
Cuda compilation tools, release 12.1, V12.1.66
Built cuda_12.1.2/Compiling 32415258_0
```

一个常见的错误是“RuntimeError: CUDA error: all CUDA-capable devices are busy or unavailable”（运行时错误：CUDA 错误：所有 CUDA 兼容设备忙碌或不可用）。这通常表明图形加速器被另一个进程阻塞。使用 `Nvidia-smi` 查找标记为“E”的任何进程并将其终止。有时，仅仅在两三秒后再次运行脚本就能解决问题。

### 电源管理

如果你使用笔记本电脑运行 GPU 环境，请确保电源已连接，因为现代笔记本电脑 GPU 对主机有极高的功率需求，且在电池供电时通常会降频。建议将机器设置为性能模式，使内核驱动提供最大量的计算性能。

> 当电源连接到机器时，峰值功率会增加到 80 瓦。

尽管安装 CUDA 环境通常足以确保 AI 功能，但在实践中，各种问题层出不穷。幸运的是，在许多情况下，对确切的错误消息进行 Google 搜索就足以使事物恢复正常运行。请记住，驱动环境已知会与挂起系统发生不良交互；旨在运行 AI 任务的工作站，理想情况下，应始终通过输入命令 `shutdown -h now` 或从窗口管理器中选择相应选项来完全关闭。此外，应避免运行其他也使用硬件加速图形的任务——理想情况下，仅使用桌面和你打开的 AI 任务以实现最大性能和最小内存拥堵。

> **快速提示**
>
> AMD GPU 用户可能会绝望，但并非一切都失去了。
>
> 你仍然可以尝试许多 AI 工具的 CPU 模式。OpenCL 通常不是选项，它本可以利用 AMD 和 Intel GPU，但目前是 Nvidia 优先的 AI 世界。

### 工作环境

运行人工智能需要一个精心调整的系统设置。如果要避免厂商锁定，我们也希望确保工作环境尽可能标准化。

鉴于 AI 任务需要大量的处理能力，它们在卸载到 GPU 上运行时表现最好。遗憾的是，Linux 上的图形加速传统上是系统管理员已知最无常的任务之一。电气工程师和类似的 GPU 密集型工作者通常避免设置 GPU 驱动，因为它们会负面影响整体系统稳定性。因此，如果你的数据很有价值，建议在部署图形驱动之前执行完整备份。

以下步骤将使用 Ubuntu 22.04 LTS 执行。确保所有操作系统更新已安装，并且内核及工具链的其他部分处于尽可能最新的状态。

尽量让你的工作环境尽可能舒适。在普通文本编辑器中编辑 Python 是可能的，但体验不佳，因此我们推荐使用 Visual Studio Code，因为它提供了一个愉快且节省资源的环境。

最后，确保有足够的随机存储可用。AI 模型可能出乎意料地大，即使在训练状态下也是如此；我们进入此任务时拥有超过 200GB 的 NVM 支持的免费内存。

## 自然语言翻译

现代智能机器可以执行实时翻译。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_33_0.png)

在本节中，我们将以原生形式运行翻译环境。LibreTranslate 还提供了位于 `https://registry.hub.docker.com/r/libretranslate/libretranslate` 的 Docker 容器。不过，并不一定建议使用它——请记住，将 CUDA 加速暴露给 Docker（如 `https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html` 中所述）是一个复杂且易出错的流程。由于 Python 社区认为该产品的稳定性已足够高，因此可以通过 *Pip* 来处理底层库的部署。

出于便利性的考虑，我们首先通过输入以下命令创建一个 *virtual environment*（当前环境显示在括号中）：

```
(base)~$ conda create -n aitranslator
(base)~$ conda activate aitranslator
(aitranslator)~$
```

随后，通过 *Pip 3* 完成实际的下载：

```
(aitranslator)~$ pip3 install argostranslate
```

鉴于我们的虚拟环境是全新的，将下载约 2GB 的库，因此请确保你拥有高速互联网连接。当 *Pip 3* 包管理器发出版本信息 '*Successfully installed argostranslate-1.8.0*' 时，即表示安装成功——你的版本可能略有不同，因为在你阅读本文时，*Pip* 仓库的内容可能已经更新。

请记住，在虚拟环境中安装 *Argos* 并不总是最佳方法——如果你想使用 *Argossum* 等命令行实用工具，从工作站进行全局安装可能更合理。然而，对于我们的评估而言，使用虚拟环境可以使清理安装过程更加容易。

其副作用之一是，库和语言包必须彼此独立地部署。如果你进行纯编程式的安装，库包的部署必须通过 Python 代码完成。因此，创建一个新的工作文件，并在你选择的开发环境中打开它。接下来，从导入所需的包并声明目标语言代码开始：

```
import argostranslate.package
import argostranslate.translate
from_code = "en"
to_code = "de"
```

然后，通过以下代码片段完成实际的下载过程：

```
argostranslate.package.update_package_index()
available_packages = argostranslate.package.get_available_packages()
package_to_install = next(
    filter(
        lambda x: x.from_code == from_code and x.to_code == to_code, available_packages
    )
)

argostranslate.package.install_from_path(package_to_install.download())
print("Package installed!")
```

首先，调用 `update_package_index()` 以促使 *Argos Translate* 更新其内部包缓存。之后，`get_available_packages()` 返回当前安装已知的所有包和语言组合列表。实际的安装过程需要一个指示语言包将被下载到的路径。使用 lambda 过滤器从值中提取这个路径是最简单的方法；最终结果传递给方法 `install_from_path`，该方法确保包下载。

鉴于 *Argos Translate* 会在你的机器上创建本地缓存，包下载程序只需运行一次。因此，下一步涉及创建另一个工作文件，该文件将作为实际翻译逻辑的主机。它也从导入包和声明目标语言代码开始。实际的转换操作如下所示：

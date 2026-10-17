
焊盘设置参数由 `IOMUXC` 控制。`IOMUXC` 仅由由几个基础 `IOMUX` 单元组合组合逻辑组成。每个基础 `IOMUX` 单元只处理一个焊盘信号的复用。下图插示了系统中的 `IOMUX`/`IOMUXC` 连接性：

![](img/6ae71abd6b0ad6512145782465527d4b_126_0.png)

主 `IOMUXC` 特性为：

1. 32 位软件复用控制寄存器（`IOMUXC_SW_MUX_CTL_PAD_<PAD NAME>` 或 `IOMUXC_SW_MUX_CTL_GRP_<GROUP NAME>`），用于为每个焊盘或预定义的焊盘组配置八种备用（ALT）模式路径之一，并启用强制焊盘（s）的输入路径（ION 位）。
2. 32 位软件焊盘控制寄存器（`IOMUXC_SW_PAD_CTL_PAD_<PAD NAME>` 或 `IOMUXC_SW_PAD_CTL_GRP_<GROUP NAME>`），用于配置每个焊盘或预定义焊盘组的特定焊盘设置。
3. 32 位通用寄存器 - 根据 SoC 要求提供 14 个 (`GPR0` 到 `GPR13`) 用于任何用途。
4. 32 位输入寄存器 - 根据 SoC 要求用于任何用途。


## 安装配置指南

### 反馈渠道

请向 Don Sccreat（`secret@uiuc.edu`）报告任何相关问题。

### 静态库安装 (`INSTALLSTATICLIB`)

```text
# INSTALLSTATICLIB = installstaticlib
```

如果您希望编译并安装静态库，请取消该行的注释。我建议这样做，但如果不这样做也不是世界末日。稍后若要编译静态库，只需进入源代码目录并输入 `make static` 即可。

### 共享库安装 (`INSTALLSHAREDLIB`)

```text
INSTALLSHAREDLIB = installsharedlib
```

如果您不想安装共享库，请注释掉该行。如果您不安装共享库或静态库，请先使用 `make static` 以强制仅构建静态库；然后演示程序将使用此本地静态库。不过在更改此项之前请三思。共享库是 `SVGAlib` 的基础。如果这对您来说毫无意义，请休息一下，跳转到“SVGAlib 基础”部分。

### LAOUT 兼容库安装 (`INSTALLLAOUTLIB`)

```text
"""INSTALLLAOUTLIB = installlaoutcompat
#-------------------------------------------------------#"""
```

如果您的 `TARGET_FORMAT` 是 ELF，并且有预编译的共享库 `a.out` 映像，请将映像安装在第一个目录（名称类似于 `aout/`）中，该目录位于 `/etc/ld.so.conf` 中。如果您希望这样操作，请保持上述行不变。

### 保留共享库 (`KEEPSHAREDLIBS`)

```text
KEEPSHAREDLIBS = keep
```

如果您希望保留旧的共享映像，请注释掉该行。除了您自行重命名外，旧的标头文件、库桩文件和静态库不能保留在公共位置。

### 安装实用工具 (`INSTALLUTILS`)

```text
INSTALLUTILS = installutils
```

如果您不想编译和安装实用工具，请注释掉该行。

### 安装手册页 (`INSTALLMAN`)

```text
INSTALLMAN = installman
```

如果您不想默认安装手册页（man pages），请注释掉该行。

### 手册页格式 (`MANFORMAT`)

```text
MANFORMAT = compressed
# MANFORMAT = uncompressed
```

删除上述两行中一行的井号（#），以指示您是否希望压缩安装手册页（使用 `gzip`）。如果您注释掉这两行，`Makefile` 将尝试确定您的系统是否支持压缩的手册页，并在可能时安装它们。

### 更新 whatis 数据库 (`MAKEWHATIS`)

```text
# MAKEWHATIS = makewhatis
# Beware, this will really need a few minutes!
#-------------------------------------------------------------#
```

这是更新手册页 `whatis` 数据库的命令。这是一个耗时较长的命令。如果您没有足够的耐心，只需注释掉该行。

### 图形驱动程序配置

```text
#-------------------------------------------------------------#
INCLUDE_ET4000_DRIVER = y
INCLUDE_CIRRUS_DRIVER = y
INCLUDE_TVGA_DRIVER = y
INCLUDE_OAK_DRIVER = y
INCLUDE_EGA_DRIVER = y
INCLUDE_MACH32_DRIVER = y
INCLUDE_S3_DRIVER = y
INCLUDE_ET3000_DRIVER = y
INCLUDE_GVGA6400_DRIVER = y
INCLUDE_ARK_DRIVER = y
INCLUDE_ATI_DRIVER = y
INCLUDE_ALI_DRIVER = y
INCLUDE_MACH64_DRIVER = y
INCLUDE_CHIPS_DRIVER = y
INCLUDE_APM_DRIVER = y
INCLUDE_NV3_DRIVER = y
INCLUDE_ET6000_DRIVER = y
INCLUDE_VESA_DRIVER = y
INCLUDE_MX_DRIVER = y
INCLUDE_PARADISE_DRIVER = y
```

注释掉您不想包含在库中的任何驱动程序。我一直将这些设置为 `y`，但如果您没有某些显卡，可以通过对这些显卡说 `no` 来缩减二进制文件的大小。请记住，使用 `SVGAlib` 的一个优势是，每次更改硬件时无需重新编译。如果只包含一个驱动程序，您将失去这一优势。

### 驱动程序自动检测测试

```text
INCLUDE_ET4000_DRIVER_TEST = y
INCLUDE_CIRRUS_DRIVER_TEST = y
INCLUDE_TVGA_DRIVER_TEST = y
INCLUDE_OAK_DRIVER_TEST = y
INCLUDE_EGA_DRIVER_TEST = y
INCLUDE_MACH32_DRIVER_TEST = y
INCLUDE_GVGA6400_DRIVER_TEST = y
INCLUDE_S3_DRIVER_TEST = y
INCLUDE_ET3000_DRIVER_TEST = y
#INCLUDE_ARK_DRIVER_TEST = y
INCLUDE_ATI_DRIVER_TEST = y
INCLUDE_ALI_DRIVER_TEST = y
#INCLUDE_MACH64_DRIVER_TEST = y
INCLUDE_CHIPS_DRIVER_TEST = y
INCLUDE_APM_DRIVER_TEST = y
INCLUDE_NV3_DRIVER_TEST = y
INCLUDE_ET6000_DRIVER_TEST = y
INCLUDE_MX_DRIVER_TEST = y
INCLUDE_PARADISE_DRIVER_TEST = y
#Might be too dangerous:
#INCLUDE_VESA_DRIVER_TEST = y
```

注释掉您不想自动检测的适配器。

### DAC 支持配置

```text
INCLUDE_NORMAL_DAC = y
INCLUDE_S3_DAC_DAC = y
INCLUDE_S3_GENDAC_DAC = y
INCLUDE_S3_TRIO64_DAC = y
INCLUDE_SIERRA_DAC = y
INCLUDE_SC15025_DAC = y
INCLUDE_ATT20C490_DAC = y
INCLUDE_ATT20C498_DAC = y
INCLUDE_ICW_DAC = y
INCLUDE_IBM86B52x_DAC = y
INCLUDE_SC1148X_DAC = y
```

注释掉您不想包含在库中的任何 `DAC` 支持。`DAC` 代表数模转换器，并在第 2 章中进行了说明。

### DAC 自动检测测试

```text
INCLUDE_S3_SDAC_DAC_TEST = y
INCLUDE_S3_GENDAC_DAC_TEST = y
INCLUDE_SC15025_DAC_TEST = y
INCLUDE_ATT20C490_DAC_TEST = y
INCLUDE IBMRGB52x_DAC_TEST = y
INCLUDE_SC1148X_DAC_TEST = y
```

注释掉您不想自动检测的 `DAC`。（目前并非所有 `DAC` 都可以自动检测）。

### 配置文件路径

```text
SVGAIB_CONFIG_FILE = $(datadir)/1ibvga.config
```

这是 `svgalib` 配置文件的位置。

### 动态解析配置 (`DYNAMIC`)

```text
# Defining DYNAMIC enables runtime parsing of the file
# defined by ET4000_REGS (usually /etc/1ibvga.et4000) for the
# et4000 or et6000 driver. See et4000/README for details.
# Commenting this out again saves binary space.
#
# If you just want to use the et4000.regs or et6000 in the
# source directory, comment out the definition of DYNAMIC.
# DYNAMIC allows development of new resolutions without
# recompiling.
DYNAMIC = y
ET4000_REGS = $(datadir)/1ibvga.et4000
ET6000_REGS = $(datadir)/1ibvga.et6000
```

```text
# The EGA driver may load additional modes (SuperEGA cards)
# like the et4000 driver does. Just define the configuration
# file below. [This should be taken with a grain of salt. EGA
# is untested.]
#EGA_REGS = $(datadir)/1ibvga.ega
```

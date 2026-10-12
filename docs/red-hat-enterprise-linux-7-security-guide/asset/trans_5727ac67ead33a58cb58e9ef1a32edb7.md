
SCAP 安全指南 (SSG) 项目的软件包 scap-security-guide 包含了针对 Linux 系统的最新安全策略集。要在您的系统上安装 SCAP 安全指南软件包，请以 root 身份输入以下命令：

```bash
# yum install scap-security-guide
```

scap-security-guide 的一部分也是关于 Red Hat Enterprise Linux 7 设置的指导。若要检查 scap-security-guide 提供的安全内容，请使用 **oscap info** 模块：

```bash
$ oscap info /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

此命令的输出是 SSG 文档的大纲，其中包含可用的配置配置集。若要审计您的系统设置，请选择合适的配置集并运行相应的评估命令。例如，以下命令用于根据 Red Hat 认证云提供商的草案 SCAP 配置集评估给定系统：

```bash
$ oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_rht-ccp --results ssg-rhel7-xccdf-result.xml --report ssg-rhel7-report.html /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

## 7.10. 其他资源

有关各种感兴趣的安全合规领域的更多信息，请参阅以下资源。

### 已安装的文档

- oscap(8) – **oscap** 命令行实用程序的手册页提供了可用选项的完整列表及其用法说明。
- scap-workbench(8) – **SCAP Workbench** 应用程序的手册页提供了关于该应用的基本信息，以及一些指向潜在 SCAP 内容来源的链接。
- scap-security-guide(8) – **scap-security-guide** 的手册页提供了关于各种可用 SCAP 安全配置集的进一步文档。还介绍了如何利用 **OpenSCAP** 实用程序使用提供的基准的示例。

### 在线文档

- [OpenSCAP 项目主页](#) – OpenSCAP 项目的主页提供了关于 **oscap** 实用程序以及与 SCAP 相关的其他组件和项目的详细信息。
- [SCAP Workbench 项目主页](#) – SCAP Workbench 项目的主页提供了关于 **scap-workbench** 应用程序的详细信息。
- [SCAP 安全指南 (SSG) 项目主页](#) – SSG 项目的主页，提供针对 Red Hat Enterprise Linux 的最新安全内容。
- [国家标准与技术研究院 (NIST) SCAP 页面](#) – 此页面代表了大量的 SCAP 相关材料的集合，包括 SCAP 出版物、规范以及 SCAP 验证计划。
- [国家漏洞数据库 (NVD)](#) – 此页面代表了最大的基于 SCAP 内容和其他 SCAP 标准的漏洞管理数据仓库。
- Red Hat OVAL 内容仓库 – 这是一个包含针对 Red Hat Enterprise Linux 系统的 OVAL 定义的仓库。
- MITRE CVE – 这是一个由 MITRE 公司提供的已知公开安全漏洞数据库。
- MITRE OVAL – 此页面代表了由 MITRE 公司提供的 OVAL 相关项目。除其他 OVAL 相关信息外，这些页面包含 OVAL 语言的最新版本以及包含数千个 OVAL 定义的 OVAL 内容仓库。
- Red Hat Satellite 文档 – 这组指南描述了（除其他主题外）如何使用 OpenSCAP 来维护多个系统的安全性。

# 第 8 章. 联邦标准与法规

为了维持安全级别，您的组织可能努力遵守联邦和工业安全规范、标准和法规。本章描述了这些标准和法规中的一些。

## 8.1. 联邦信息处理标准 (FIPS)

联邦信息处理标准 (FIPS) 出版物 140-2 是一项计算机安全标准，由美国政府和工作组开发，用于验证加密模块的质量。在此处查看官方 FIPS 出版物：[http://csrc.nist.gov/publications/PubsFIPS.html](http://csrc.nist.gov/publications/PubsFIPS.html)。

FIPS 140-2 标准确保加密工具正确实现其算法。有关这些级别和 FIPS 标准其他规范的进一步详情，请在 [http://dx.doi.org/10.6028/NIST.FIPS.140-2](http://dx.doi.org/10.6028/NIST.FIPS.140-2) 查看完整的 FIPS 140-2 标准。

若要查看所有 FIPS 140-2 证书的完整列表，请访问 [http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/140val-all.htm](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/140val-all.htm)。要了解合规要求，请参阅 [Red Hat 政府：标准页面](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/.../)。

### 8.1.1. 启用 FIPS 模式

要使 Red Hat Enterprise Linux 符合联邦信息处理标准 (FIPS) 出版物 140-2，您需要做出几处更改，以确保使用经过认可的加密模块。您可以在系统安装期间或安装后启用 FIPS 模式。

#### 在系统安装期间

若要满足*严格的 FIPS 140-2 合规性*，请在系统安装期间将 `fips=1` 内核选项添加到内核命令行。使用此选项后，所有密钥的生成都通过 FIPS 认可的算法进行，并设置了持续监控测试。安装后，系统将自动配置为启动到 FIPS 模式。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_238_0.png)

> **重要**
> 在安装过程中，通过移动鼠标或按下许多按键来确保系统有足够的熵。建议的按键数为 256 个或更多。少于 256 个按键可能生成非唯一密钥。

#### 在系统安装之后

若要安装后通过将系统的内核空间和用户空间转换为 FIPS 模式，请按照以下步骤操作：

1.  安装 dracut-fips 软件包：

    ```bash
    ~]# yum install dracut-fips
    ```

    对于支持 AES 新指令 (AES-NI) 的 CPU，也安装 dracut-fips-aesni 软件包：

    ```bash
    ~]# yum install dracut-fips-aesni
    ```

2.  重新生成 initramfs 文件：

    ```bash
    ~/# dracut -v -f
    ```

    为了启用模块内完整性验证并在内核启动期间拥有所有必需模块，必须重新生成 initramfs 文件。

    > **警告**
    > 此操作将覆盖现有的 initramfs 文件。

3.  修改引导加载器配置。

    若要启动到 FIPS 模式，请将 `fips=1` 选项添加到引导加载器的内核命令行中。如果您的 /boot 或 /boot/EFI/ 分区位于单独的分区上，请也向内核命令行添加 `boot=<partition>`（其中 <partition> 代表 /boot 或 /boot/EFI）参数。

    若要识别引导分区，请输入以下命令：

    ```bash
    ~/ $ df /boot
    Filesystem     1K-blocks    Used Available Use% Mounted on
    /dev/sda1       495844    53780   416464  12% /boot
    ```

    为了确保即使设备命名在启动之间发生变化，`boot=` 配置选项也能正常工作，请运行以下命令识别分区的通用唯一标识符 (UUID)：

    ```bash
    ~/ $ blkid /dev/sda1
    /dev/sda1: UUID="05c000f1-f899-467b-a4d9-d5ca4424c797" TYPE="ext4"
    ```

    将 UUID 附加到内核命令行：

    ```text
    boot=UUID=05c000f1-f899-467b-a4d9-d5ca4424c797
    ```

    根据您的引导加载器，进行以下更改：

    -   **GRUB 2**

        将 `fips=1` 和 `boot=<partition of /boot or /boot/EFI>` 选项添加到 `/etc/default/grub` 文件中的 `GRUB_CMDLINE_LINUX` 键。若要应用对 `/etc/default/grub` 的更改，请重新构建 `grub.cfg` 文件，如下所示：

        -   在基于 BIOS 的机器上，以 root 身份输入以下命令：

            ```bash
            ~/# grub2-mkconfig -o /etc/grub2.cfg
            ```

        -   在基于 UEFI 的机器上，以 root 身份输入以下命令：

            ```bash
            ~]# grub2-mkconfig -o /etc/grub2-efi.cfg
            ```

    -   **zipl**（仅在 IBM z Systems 架构上）

        将 `fips=1` 和 `boot=<partition of /boot>` 选项添加到 `/etc/zipl.conf` 文件中的内核命令行，并通过作为 `root` 运行以下命令来应用更改：

        ```bash
        ~]# zipl
        ```

4.  确保预链接已禁用。

    为了模块内完整性验证的正常运行，必须禁用库和二进制文件的预链接。预链接由 `prelink` 软件包完成，该软件包默认未安装。除非安装了 `prelink`，否则不需要此步骤。要禁用预链接，请在 `/etc/sysconfig/prelink` 配置文件中设置 `PRELINKING=no` 选项。要禁用所有系统文件上的现有预链接，请使用 `prelink -u -a` 命令。

5.  重启您的系统。

### 在容器中启用 FIPS 模式

如果主机也设置为 FIPS140-2 模式，并且满足以下要求之一，则可以切换容器到 FIPS140-2 模式：

-   在容器中安装了 `dracut-fips` 软件包。
-   从主机在容器上挂载了 `/etc/system-fips` 文件。

## 8.2. 国家工业安全计划操作手册 (NISPOM)

NISPOM（也称为 DoD 5220.22-M）作为国家工业安全计划 (NISP) 的一个组成部分，就机密信息为所有政府承包商建立了一系列程序和要求的程序。当前的 NISPOM 日期为 2006 年 2 月 28 日，并合并了 2013 年 3 月 28 日的主要更改。NISPOM 文档可从以下 URL 下载：`http://www.nispom.org/NISPOM-download.html`。

## 8.3. 支付卡行业数据安全标准 (PCI DSS)

来自 `https://www.pcisecuritystandards.org/about/index.shtml`：*PCI 安全标准委员会是一个于 2006 年启动的开放全球论坛，负责 PCI 安全标准的开发、管理、教育和意识，包括数据安全标准 (DSS)。*

您可以从 `https://www.pcisecuritystandards.org/security_standards/pci_dss.shtml` 下载 PCI DSS 标准。

## 8.4. 安全技术实施指南

安全技术实施指南 (STIG) 是一种用于计算机软件和硬件标准化安全安装和维护的方法。

有关 STIG 的更多信息，请参阅以下 URL：`http://iase.disa.mil/stigs/Pages/index.aspx`。


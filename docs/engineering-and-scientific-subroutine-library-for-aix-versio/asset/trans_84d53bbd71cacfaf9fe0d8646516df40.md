

## 应使用 XL Fortran XLSMPOPTS 或 OMP_NUM_THREADS 环境变量来指定要创建的线程数。

-   在 POWER4 和 POWER4+ 处理器上：
    -   结构化 ESSL 子程序，使得在适用的情况下，编译后的代码充分利用双浮点执行单元。由于每个周期可以执行两条乘加指令，若忽略开销，则每个周期可执行四次浮点运算。
    -   结构化 ESSL 子程序，使得在适用的情况下，编译后的代码充分发挥硬件数据预取的优势。
-   在 POWER3 和 POWER3-II 处理器上：
    -   结构化 ESSL 子程序，使得在适用的情况下，编译后的代码充分利用双浮点执行单元。由于每个周期可以执行两条乘加指令，若忽略开销，则每个周期可执行四次浮点运算。
    -   结构化 ESSL 子程序，使得在适用的情况下，编译后的代码充分发挥硬件数据预取的优势。

### 数学技术

ESSL 的所有领域均采用最先进的数学技术来实现高性能。例如，矩阵-向量线性代数子程序操作于更高级别的数据结构，即矩阵-向量而非向量-标量。因此，它们直接优化您程序的性能，并间接通过使用该子程序的 ESSL 子程序进行优化。

## 子程序的 Fortran 语言接口

ESSL 子程序遵循标准的 Fortran 调用约定，并且必须在 Fortran 运行时环境中运行。当从 Fortran 以外的语言（如 C 或 C++）中的程序调用 ESSL 子程序时，必须使用 Fortran 约定。这适用于接口的所有方面，例如链接约定和数据约定。例如，数组顺序必须与 Fortran 数组顺序技术保持一致。各语言的数据和链接约定在第 107 页的“第 4 章，编写您的程序”中给出。

## 可与 ESSL 一起使用的软件和硬件产品

本节描述可与 ESSL 一起使用的硬件和软件产品，以及用于安装 ESSL 和显示联机文档的产品。它分为以下几个部分：

- “ESSL for AIX—硬件和软件”
- “ESSL for Linux—硬件和软件”见第 8 页

## ESSL for AIX—硬件和软件

本节描述可与 ESSL for AIX 一起使用的硬件和软件产品。

### ESSL for AIX—硬件

ESSL for AIX 运行在受 AIX 操作系统支持的 IBM @server pSeries 和 RS/6000 处理器上。

64 位应用程序需要 64 位硬件。

### ESSL for AIX—操作系统

ESSL for AIX 在以下操作系统环境中得到支持：

- AIX 5L™ Version 5.2 配合 5200-01 推荐维护包（产品编号 5765-E62）

### ESSL for AIX—软件产品

ESSL for AIX 需要表 2 中列出的软件产品用于编译和运行。

为协助 C 和 C++ 用户，提供了一个 ESSL 头文件。此文件的使用在第 124 页的“*C 程序*”和第 140 页的“*C++ 程序*”中进行了描述。

![](img/5b0f44f3be6048723819b26aed7f6f03_31_0.png)

| 用于编译 | 用于链接、加载或运行 |
| :--- | :--- |
| XL Fortran for AIX, Version 8.1 或更高版本（程序编号 5765-F70） *–或–* | XL Fortran Run-Time Environment for AIX, Version 8.1 或更高版本（程序编号 5765-F71） –**和**– |
| IBM Visual Age C++ Professional for AIX, Version 6.0（程序编号 5765-F56） *–或–* | C 库¹ |
| C for AIX, Version 6.0（程序编号 5765-F57） | |

¹ AIX 产品包含 Application Development Toolkit 中的 C 库和数学库。

### ESSL for AIX—安装和定制产品

ESSL for AIX 许可程序以 CD 形式分发。*ESSL Installation Guide* 提供了安装 ESSL 所需的详细信息。

ESSL for AIX 产品根据 AIX 指南进行打包，如 *AIX General Programming Concepts: Writing and Debugging Programs* 手册中所述。该可以使用 smit 命令进行安装，如 *AIX System Management Guide: Operating System and Devices* 手册中所述。

## ESSL for Linux—硬件和软件

本节描述可与 ESSL for Linux 一起使用的硬件和软件产品。

### ESSL for Linux—硬件

ESSL for Linux 运行在受 Linux 操作系统支持的 IBM @server pSeries 和 RS/6000 处理器上。

64 位应用程序需要 64 位硬件。

### ESSL for Linux—操作系统

ESSL for Linux 在以下操作系统环境中得到支持：

- SuSE Linux Enterprise Server 8 for pSeries (SLES8)

### ESSL for Linux—软件产品

ESSL for Linux 需要表 3 第 9 页中列出的软件产品用于编译和运行。

为协助 C 和 C++ 用户，提供了一个 ESSL 头文件。此文件的使用在第 124 页的“*C 程序*”和第 140 页的“*C++ 程序*”中进行了描述。

### 表 3. *与 ESSL for Linux 一起使用所需的软件产品*

| 用于编译 | 用于链接、加载或运行 |
|---|---|
| XL Fortran for Linux on pSeries, Version 8.1 或更高版本（程序编号 5765-F70） *或* IBM Visual Age C++ Professional for Linux on pSeries, Version 6.0（程序编号 5765-F56） | XL Fortran Run-Time Environment for Linux, Version 8.1 或更高版本（程序编号 5765-F71） –和– GCC 32 位和/或 64 位库，Version 3.2 或更高版本，可以在以下包中找到： **32 位库** glibc **64 位库** cross-ppc64-glibc **注释:** 1. 以下包是构建应用程序所需的： **32 位应用程序** binutils **64 位应用程序** cross-ppc64-binutils 2. 以下包是构建 C 和 C++ 应用程序所需的： **32 位应用程序** gcc **64 位应用程序** cross-ppc64-gcc |

### ESSL for Linux—安装和定制产品

ESSL for Linux 许可程序以 CD 形式分发。*ESSL for Linux Installation Guide* 提供了安装 ESSL for Linux 所需的详细信息。

ESSL for Linux 产品打包为 RPM 包。可以使用 **rpm** 命令安装该产品，如以下 URL 中所述：`http://www.rpm.org/`

## 用于显示 ESSL 文档的软件产品

显示 ESSL 联机信息所需的软件产品列于表 4 中。

### 表 4. *显示各种格式 ESSL 联机信息所需的软件*

| 联机信息格式 | 所需软件 |
|---|---|
| HTML | HTML 文档浏览器（如 Microsoft® Internet Explorer） |
| PDF | Adobe Acrobat Reader，可从 Adobe 网站免费下载：`http://www.adobe.com` |
| Manpages | 无需额外软件。要显示特定的 manpage，请按照以下方式使用 man 命令：man subroutine-name |
| | **注意:** 这些 manpages 将安装在以下目录中： **On AIX** /usr/share/man/cat3 **On Linux** /usr/share/man/man3 LAPACK 提供的 manpages 安装在 /usr/share/man/man3 目录中。默认情况下，会显示 ESSL manpages 而不是同名 BLAS 或 LAPACK manpages。若要访问 BLAS 或 LAPACK manpages，必须设置 MANPATH 环境变量。请参阅 man 命令的文档。 |

## ESSL 互联网资源

ESSL 文档以及其他相关信息可以从表 5 中列出的 URL 在互联网上显示或下载。

### 表 5. ESSL 相关信息的在线资源

| 网站 | 提供的信息类型 | 可用文件格式 |
|---|---|---|
| | | PDF | HTML |
| IBM @server Cluster Resource Center: http://publib.boulder.ibm.com/clresctr | 最新发布的 pSeries 和集群服务器软件产品的文档 | 是 | 是 |
| IBM @server pSeries Resource Library: http://www-1.ibm.com/servers/eserver/pseries/1ibrary/sp_books/index.html | 多个发布的 pSeries 和 RS/6000 SP 硬件和软件产品的文档 | 是 | 是 |
| IBM Publications Center: http://w3.ohone.ibm.com/public/applications/publications/csbin/pbi.cgi | IBM 产品的文档 | 是 | 否 |

## 加入 ESSL 邮件列表

可以通过加入 ESSL 邮件列表获取 ESSL 的最新信息。此外，邮件列表上的用户将收到有关新 ESSL 功能的信息，并可能收到客户满意度调查和需求调查，以便向 ESSL 开发部门提供关于产品和用户需求的反馈。

您可以通过向以下任一对象发送请求，询问加入 ESSL 邮件列表，从而被加入邮件列表：

International Business Machines Corporation


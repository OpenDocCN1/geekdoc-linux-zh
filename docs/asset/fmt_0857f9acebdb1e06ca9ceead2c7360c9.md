
> **图 6.82**-使用 ssdeep 查询目标标本和相应的进程内存转储

¹150 有关 pcat 的更多信息，请访问 http://www.porcupine.org/forensics/tct.html。

¹51 有关 ssdeep 的详细讨论，请参阅第 5 章。

## 第 6 章恶意软件标本分析

### 其他可考虑的工具

进程内存获取
有许多工具可用于获取运行进程的内存：

- `memfetch`: 由 Michal Zalewski 编写，`memfetch` 将内存映射转储到单独的文件以供分析 (http://freecode.com/projects/memfetch)。
- `gcore`: 获取运行进程内存内容的传统方法是使用 `gcore` 转储进程的核心镜像（core image），它是 Linux 和 UNIX 发行版的原生实用程序。
- `Shortstop`: 一个转储进程内存和关联元数据的工具 (https://google.com/shortstop/)。
- `Process Dumper (pd_v1.lx)`: 由 Tobias Klein 开发，Process dumper 是免费的闭源软件，与 Memory Parser (http://www.trapkit.de/forensic/pd/index.html) 以及 http://www.trapkit.de/research/mnp/index.html) 工具配合使用。
- `memgrep`: 一个替换或转储运行进程及核心文件内容的工具 (http://freecode.com/projects/memgrep)。进一步的讨论和对比可以在本第 6 章末尾的工具箱以及配套网站 www.malwarefieldguide.com/LinuxChapter6.html 中找到。

在执行文件（在本例中为 Gummo 后门标本）之前，这些文件的相似性得分为 96 (100)。相反，在查询与目标恶意软件标本相关的内存文件时，文件的相似性得分为 100，表明这些标本曾被执行过。

### 可视化

如第 5 章所述，二进制文件内容的可视化为数字调查人员提供了关于文件中数据分布的快速参考。除了识别混淆外，比较多个可疑文件的数据模式也可以作为基于数据分布可视化来识别潜在相似文件的方法。

- 可以通过 BinVis，¹⁵² 使用多种可视化方案查看目标恶意软件执行文件。尽管 BinVis 设计用于解析 Windows 可移植执行文件 (PE) 文件和 ELF 文件，但目前

> ¹⁵² 有关 BinVis 的更多信息，请访问 http://code.google.com/p/binvis/。目前 BinVis 无法在 Linux 中原生安装和运行；必须在 Linux 分析系统上安装 WINE¹¹³

- 要选择执行文件进行分析，请使用 BinView 工具栏并选择“File” = “Open”。
- 一旦将执行文件加载到 BinView，通过“View”选项选择数据可视化方案来查看文件。
- 除了十六进制查看器外，BinView 还有七种不同的数据可视化方案：
  - `Byte Plot（字节图）`: 将每个位映射到像素。
  - `RGB Plot（RGB 图）`: 与 Byte Plot 类似，使用红、绿、蓝。
  - `Bit Plot（位图）`: 将每个位映射到像素。
  - `Attractor Plot（吸引子图）`: 基于混沌理论。
  - `Dot Plot（点图）`: 显示字节序列。
  - `Presence Plot（存在图）`: 数据的一种版本。
  - `Cloud Plot（云图）`: 数据的生成。

BinView 的强大功能是页面之间的交互。BinView 的另一个新颖方面是页面转换。

- 在图 6.8 所示的示例中，检查了三个恶意标本。

### 行为分析

除了比较运行时数据外，行为分析也可以作为一种方法。在编写时，不存在用于 ELF 文件行为分类的框架。

¹¹³ 有关 WINE 的更多信息，请访问 http://www.wine.org/。
¹⁵⁴ 有关 Boxerkit 的更多信息，请访问 http://www.symantic.com/security_response/2007-07。
¹⁵⁵ 有关 SSHDoor 的更多信息，请访问 http://www.symantic.com/security_response/2013。

## 恶意软件标本分析

- 分析可以使用 `Malheur`，¹⁵⁶ 框架进行分类。`Malheur` 可以通过标准编译程序编译适用于 Linux、Macintosh OS 和 OpenBSD 平台的命令行工具¹⁵⁷
- `Malheur` 处理记录并编译为恶意软件指令集 (MIST) 格式的数据集——这并非为了人类可读，而是专门用于机器学习和数据挖掘的恶意软件行为泛化。
- 数据集可以作为目录或压缩包 (`.tar.gz`, `.zip`, `.pax`, `.cpio`) 编译到 `Malheur` 中分析。数字调查人员可以通过转换 ThreatTrack SecurityAnalyzer/CWSSbox 的报告创建自定义数据集¹⁶⁰

¹⁵⁶ 有关 `Malheur` 的更多信息，请访问 http://www.mlsec.org/malheur/; http://honeyblog.org/junkyard/paper-malheur-2009.pdf（基于机器学习的恶意软件行为分析，Rieck K, Trinius P M, & Holt T. Journal of Computer Security, 19(3), 2011）。
¹⁵⁷ http://www.mlsec.org/malheur/install.html。

# Linux 系统恶意软件取证领域指南

- 曼海姆大学（University of Mannheim）可靠分布式系统实验室在其 Mwanalysis 网站上维护了一个数据集仓库。161
- 原型提取：识别并提取子集原型，这些原型是某些同质行为组的典型特征，并代表了大型报告语料的整体情况。162
- 行为聚类：识别包含相似行为的报告组（聚类），从而发现独特的恶意软件类型。163
- 行为分类：对预先处理过的报告聚类通过分类进行进一步分析，或将未知行为分配给已知的恶意软件组。通过这种方法，`Malheur` 可以识别并对独特的恶意软件变体进行分类。164
- 增量分析：`Malheur` 可以校准为以“块”的形式处理（聚类和分类）报告，从而减少资源需求。这种分析方法对于 `Malheur` 的长期实施特别有益，因为可以针对蜜罐传感器获取的常规恶意软件进行 `Malheur` 自动分析。165
- 可以将数据集输入 `Malheur` 并使用以下步骤进行处理：

1. 调用 `malheur`
2. 使用 `-o`（输出）开关并指定分析输出文件的名称（例如，在图 6.84 中，输出文件为 `out.txt`）；执行该操作。
3. 选择操作即应用于目标数据集的分析类型。操作包括：

| 操作 | 结果 |
| :--- | :--- |
| distance | 计算数据集的距离矩阵 |
| prototype | 确定一组代表目标数据集的原型 |
| cluster | 对数据集进行聚类 |
| classify | 对数据集进行分类 |
| increment | 对数据集报告进行增量分析 |
| protodist | 计算原型的距离矩阵 |

161 http://pi1.informatik.uni-mannheim.de/malheur/
162 Automatic Analysis of Malware Behavior using Machine Learning, p. 8; Rieck, K. (2011). Malheur Version 0.5,0, User Manual, p. 2.
163 Rieck, K. (2011). Malheur Version 0.5,0, User Manual, p. 2.
164 Rieck, K. (2011). Malheur Version 0.5,0, User Manual, p. 2.
165 Rieck, K. (2011). Malheur Version 0.5,0, User Manual, p. 2.

# 第 6 章 恶意软件样本分析

4. 增量地应用分析操作。例如，在进行分类之前必须对数据集进行聚类。同样，在聚类时，Malware 会自动提取原型以进行聚类分析，如图 6.84 所示

```
malware@malwareLab:~/Malware-Repository/5 malheur -v -out txt cluster

20090804_mist-tar.gz

############################################

Extracting Features from '20090804_mist-tar.gz' 100.0% 00m 05s

############################################

388,732 feature vectors with distance 31,430 extracted.

Clustering vectors with maximum distance 5. 100.0% 00m 39s

############################################

104,707 prototypes with 8,326 extracted.

Clustering distances (548628 pair, 3,960). 100.0% 00m 05s

############################################

548,628 distances computed.

Clustering linkage with minimum distance 0.95. 100.0% 00m 00s

############################################

Saving 35 feature vectors to /home/malwarelab/malheur/prototypes.zfa.

Saving 100 feature vectors to /home/malwarelab/malheur/rejected.zfa.

Exporting clusters to 'out.txt'.
```

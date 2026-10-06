
# 第 7 章节 软件包管理

## 依赖关系解析

| 软件包 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
| 安装 subversion | 1386 | 1.4.2-4.el5 | base | 2.3 M |
| 更新 neon | i1386 | 0.25.50-10.el5 | base | 101 k |
| 安装依赖项: peri-URI | noarch | 1.35-3 | base | 116 k |

事务摘要

安装 2 个软件包
更新 1 个软件包
移除 0 个软件包

总下载大小: 2.5 M
是否确认 [y/N]: 

[y/N]: []

图 7-2. 使用 yum 安装 subversion 软件包

通过回答提示符，你指示 `yum` 开始安装 `subversion` 软件包并下载其依赖包（例如 `peri-URI.noarch`）。安装完成后，`subversion` 软件包将位于你的系统中。

### 使用 YUM 移除软件包

使用 YUM 移除软件包也会移除其依赖包（如果有的话）。要使用 `yum` 命令移除软件包，请使用 `remove` 选项。例如，如果你不再需要 `gcc` 软件包，可以通过输入以下命令将其从系统中移除：

```bash
yum remove gcc
```

你将看到一个摘要屏幕，询问你是否确定要移除该软件包，如图 7-3 所示。

```
--> Running transaction check
--> Package gcc_i1386 0:4.1.2-44.el5 set to be erased
--> Processing Dependency: gcc -- 4.1.2-44.el5 for package: gcc-c++
--> Running transaction check
--> Package gcc-c++_i1386 0:4.1.2-44.el5 set to be erased
--> Finished Dependency Resolution
```

依赖关系解析

| 软件包 | 架构 | 版本 | 存储库 | 大小 |
| --- | --- | --- | --- | --- |
| 移除 gcc | i1386 | 4.1.2-44.el5 | installed | 9.6 M |
| 依赖项 gcc-c++ | i1386 | 4.1.2-44.el5 | installed | 6.5 M |

```
事务摘要
安装 0 个软件包
更新 0 个软件包
移除 2 个软件包
```

是否确认 [y/N]:

图 7-3. 使用 yum 移除软件包

在此回答 y 将从你的系统中移除 `gcc` 软件包。注意，`g++` 也会被移除，因为它依赖 `gcc` 软件包。

### 使用 YUM 更新软件包

如果你知道某个软件包有更新，并想通过 YUM 将这些更新应用到系统中，可以通过 `update` 命令来实现。例如，如果你想将 `gcc` 软件包更新到更高版本，将使用此命令：

```bash
yum update gcc
```

与 `install` 和 `remove` 命令类似，`update` 命令也会提示你与目标软件包一起需要更新的以下软件包，如图 7-4 所示。

```
--> Package libgomp.i386 0:4.3.2-7.el5 set to be updated
--> Package cpp.i386:4.1.2-44.el5 set to be updated
--> Package libgcc.i386 0:4.1.2-44.el5 set to be updated
--> Finished Dependency Resolution
```

依赖关系解析

| 软件包 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
| 更新: | | | | |
| cpp | i1386 | 4.1.2-44.el5 | base | 2.7 M |
| gcc | i1386 | 4.1.2-44.el5 | base | 5.2 M |
| libgcc | i1386 | 4.1.2-44.el5 | base | 94 k |
| libgomp | i1386 | 0:4.3.2-7.el5 | base | 67 k |

事务摘要

- 安装 0 个软件包
- 更新 4 个软件包
- 移除 0 个软件包

总下载大小: 8.1 M
是否确认 [y/N]:

![](img/57e3c53e2eeaac1ba18c095c31e37c47_175_0.png)

回答 y 将使 YUM 下载更新后的软件包并将其应用到你的系统中。如果没有更新的软件包，YUM 将终止并通知你想要更新的目标软件包仍是最新版本。

### 使用 YUM 搜索软件包

你可以使用 `search` 命令通过 YUM 查找其存储库列表中可以安装的可用软件包。例如，如果你想知道安装 `bison` 软件包时哪些包会被添加到系统中，将输入：

```bash
yum search bison
```

YUM 中的 `search` 命令并不限制于完整的单词。如果你不确定要找的是什么，也可以使用包名的一部分来搜索软件包。例如，如果你知道有一个以 b 和 i 开头的解析器生成工具，并且你想在 YUM 中查找它，可以运行此命令：

```bash
yum search bi
```

你将看到所有 YUM 可以安装的以 bi 开头的软件包列表。

### 为 YUM 添加源

你可以使用 `search` 命令通过 YUM 查找其存储库列表中可以安装的可用软件包。例如，如果你想知道安装 `bison` 软件包时哪些包会被添加到系统中，将输入：

```bash
yum search bison
```

YUM 中的 `search` 命令并不限制于完整的单词。如果你不确定要找的是什么，也可以使用包名的一部分来搜索软件包。例如，如果你知道有一个以 b 和 i 开头的器生成工具，并且你想在 YUM 中查找它，可以运行此命令：

```bash
yum search bi
```

你将看到所有 YUM 可以安装的以 bi 开头的软件包列表。

# 第 7 章节 管理

### 使用 YUM 安装软件包

要使用 `yum` 安装软件包，你将使用 `install` 命令。例如，如果你想为你的开发团队安装 Subversion 源码控制系统，将运行以下：
```bash
yum install subversion
```

这将开始安装 `Subversion` 软件包，`yum` 还会查找需要安装的依赖包，如图 7-2 所示。

```
--> Package peri-URI.noarch 0.1.35-3 set to be updated
--> Package neon.i386 0.25.50-10.el5 set to be updated
--> Finished Dependency Resolution
```

依赖关系解析

| 软件包 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
| 安装 subversion | 1386 | 1.4.2-4.el5 | base | 2.3 M |
| 更新 neon | i1386 | 0.25.50-10.el5 | base | 101 k |
| 安装依赖项: peri-URI | noarch | 1.35-3 | base | 116 k |

事务摘要

安装 2 个软件包
更新 1 个软件包
移除 0 个软件包

总下载大小: 2.5 M
是否确认 [y/N]: []

图 7-2. 使用 yum 安装 subversion 软件包

通过回答提示，你指示 `yum` 开始安装 `subversion` 软件包并下载其依赖包（例如 `peri-URI.noarch`）。安装完成后，`subversion` 软件包将位于你的系统中。

### 使用 YUM 移除软件包

使用 YUM 移除软件包也会移除其依赖包（如果有的话）。要使用 `yum` 命令移除软件包，请使用 `remove` 选项。例如，如果你不再需要 `gcc` 软件包，可以通过输入以下命令将其从系统中移除：

```bash
yum remove gcc
```

你将看到一个摘要屏幕，询问你是否确定要移除该软件包，如图 7-3 所示。

```
--> Running transaction check
--> Package gcc_i1386 0:4.1.2-44.el5 set to be erased
--> Processing Dependency: gcc -- 4.1.2-44.el5 for package: gcc-c++
--> Running transaction check
--> Package gcc-c++_i1386 0:4.1.2-44.el5 set to be erased
--> Finished Dependency Resolution
```

依赖关系解析

| 软件包 | 架构 | 版本 | 存储库 | 大小 |
| --- | --- | --- | --- | --- |
| 移除 gcc | i1386 | 4.1.2-44.el5 | installed | 9.6 M |
| 依赖项 gcc-c++ | i1386 | 4.1.2-44.el5 | installed | 6.5 M |

```
事务摘要
安装 0 个软件包
更新 0 个软件包
移除 2 个软件包
```

是否确认 [y/N]:

## 7-3. 使用 yum 移除软件包

在此回答 y 将从你的系统中移除 `gcc` 软件包。注意，`g++` 也会被移除，因为它依赖 `gcc` 软件包。

### 使用 YUM 更新软件包

如果你知道某个软件包有更新，并想通过 YUM 将这些更新应用到系统中，可以通过 `update` 命令来实现。例如，如果你想将 `gcc` 软件包更新到更高版本，将使用此命令：

```bash
yum update gcc
```

与 `install` 和 `remove` 命令类似，`update` 命令也会提示你与目标软件包一起需要更新的以下软件包，如图 7-4 所示。

```
--> Package libgomp.i386 0:4.3.2-7.el5 set to be updated
--> Package cpp.i386:4.1.2-44.el5 set to be updated
--> Package libgcc.i386 0:4.1.2-44.el5 set to be updated
--> Finished Dependency Resolution
```

依赖关系解析

| 软件包 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
| 更新: | | | | |
| cpp | i1386 | 4.1.2-44.el5 | base | 2.7 M |
| gcc | i1386 | 4.1.2-44.el5 | base | 5.2 M |
| libgcc | i1386 | 4.1.2-44.el5 | base | 94 k |
| libgomp | i1386 | 0:4.3.2-7.el5 | base | 67 k |

事务摘要

- 安装 0 个软件包
- 更新 4 个软件包
- 移除 0 个软件包

总下载大小: 8.1 M
是否确认 [y/N]:

![](img/57e3c53e2eeaac1ba18c095c31e37c47_175_0.png)

回答 y 将使 YUM 下载更新后的软件包并将其应用到你的系统中。如果没有更新的软件包，YUM 将终止并通知你想要更新的目标软件包仍是最新版本。

### 使用 YUM 搜索软件包

你可以使用 `search` 命令通过 YUM 查找其存储库列表中可以安装的可用软件包。例如，如果你想知道安装 `bison` 软件包时哪些包会被添加到系统中，将输入：

```bash
yum search bison
```

YUM 中的 `search` 命令并不限制于完整的单词。如果你不确定要找的是什么，也可以使用包名的一部分来搜索软件包。例如，如果你知道有一个以 b 和 i 开头的解析器生成工具，并且你想在 YUM 中查找它，可以运行此命令：

```bash
yum search bi
```

你将看到所有 YUM 可以安装的以 bi 开头的软件包列表。

### 为 YUM 添加源

你可以使用 `search` 命令通过 YUM 查找其存储库列表中可以安装的可用软件包。例如，如果你想知道安装 `bison` 软件包时哪些包会被添加到系统中，将输入：

```bash
yum search bison
```

YUM 中的 `search` 命令并不限制于完整的单词。如果你不确定要找的是什么，也可以使用包名的一部分来搜索软件包。例如，如果你知道有一个以 b 和 i 开头的器生成工具，并且你想在 YUM 中查找它，可以运行此命令：

```bash
yum search bi
```

你将看到所有 YUM 可以安装的以 bi 开头的软件包列表。

# 第 7 章节 管理

## 为 YUM 创建存储库

现在你将使用 `yum` 创建包含安装 `gcc` 软件包所需包的存储库。

- 使用 `rpm` 或 `yum` 安装 `creatpo` 软件包。对于 `rpm`，使用 `rpm -Uvh createrepo-0.4.11-3.el5.i386.rpm`
- 创建作为存储库的新目录。对于我们的练习，你将在 `/var/tmp` 下创建 `compilerpackages` 目录。
- 复制安装 `gcc` 软件包所需的包。进入 CentOS DVD 或 CD 复制文件：
  - `kernel-headers-2.6.18-92.el5.i386.rpm`
  - `gcc-headers-2.5-44.i386.rpm`
  - `gcc-dev-2.5-42.i386.rpm`
  - `libgcc-common-1.2-42.i386.rpm`
  - `gcc-4.1.42.el5.i386.rpm`
  使用 `cp` 命令复制到 `/var/tmp/compilerpackages` 目录。
- 运行 `creatpo` 二进制文件，并将新存储库的路径作为其参数：`creatpo /var/tmp/compilerpackages`
- 这将在 `/var/tmp/compilerpackages` 目录生成所需的元数据文件和条目，供 YUM 获取文件使用。
- 你通过运行 `yum install gcc` 测试新的存储库。输出类似于图 7-5。

```
[root@localhost ~]# yum install gcc
compiler 100% [==========================] 951 B
primary.xmlz 100% [==========================] 2.3 kB
compiler ############################## 5.2 kB
base 100% [==========================] 1.1 kB
addons 100% [==========================] 951 B
extxtra 100% [==========================] 1.1 kB
Setting up install arguments
Parsing gcc-4.1.2-44.el5.i1386 is already installed.
Resolving Dependencies
-- Running transaction check
-- Package gcc.i1386-0:4.1.2-44.el5 set to be updated
-- Processing Dependency: libgomp >= 4.1.2-44.el5 for package: gcc
-- Processing Dependency: glibc >= 4.1.2-44.el5 for package: gcc
-- Processing Dependency: cp >= 4.1.2-44.el5 for package: gcc
-- Running transaction check
```

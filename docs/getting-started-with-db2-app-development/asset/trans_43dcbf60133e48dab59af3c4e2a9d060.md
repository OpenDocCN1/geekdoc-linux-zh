

![](img/5f6ba170efa3a607142589708531bef8_337_0.png)

图 10.1 - Python DB2 API 和用于访问 DB2 的驱动程序/适配器的高层视图

如图 10.1 所示，在 Python 应用程序中，你可以选择四种不同类型的数据库 API 及其驱动程序/适配器来访问 DB2 数据服务器。这些 API 及其驱动程序/适配器将在下一节中详细解释。

## 10.1.1 IBM 定义的 API 和 ibm_db 驱动程序

这是一组由 IBM 定义的专有 Python 数据库 API。ibm_db 驱动程序是该 API 的实现。通过此 API，你不仅可以在 Python 应用程序中发出 SQL 语句、调用存储过程和使用 pureXML，还可以访问 DB2 元数据信息。

ibm_db 驱动程序是作为 Python 模块的 C 扩展实现的，基于 DB2 的原生 CLI/ODBC 接口；因此，它可以提供最佳性能和最先进的功能。在后续章节中，我们将更详细地讨论此驱动程序。

**注意：**

ibm_db API 规范可以在 [http://code.google.com/p/ibm-db/wiki/APIs](http://code.google.com/p/ibm-db/wiki/APIs) 找到。

## 10.1.2 Python 数据库 API 和 ibm_db_dbi 驱动程序

Python 数据库 API 是一组为 Python 应用程序定义的开放标准数据库 API。ibm_db_dbi 驱动程序是一个简单的 Python 代码封装器，构建于 ibm_db 驱动程序之上，提供符合标准 Python 数据库 API 规范的数据库 API。与 ibm_db 驱动程序类似，它也允许你通过这些标准 API 发出 SQL 语句并调用存储过程。由于该 API 符合标准规范，它不提供 ibm_db API 支持的某些高级功能。但是，如果你有一个使用支持 Python 数据库 API 规范的驱动程序编写的应用程序，你可以轻松地切换到 ibm_db_dbi。

在撰写本文时，ibm_db_dbi 驱动程序支持 Python 数据库 API 规范 v2.0。

**注意：**

Python 数据库 API 是 Python 接口实现数据库管理系统的标准规范。你可以在 http://www.python.org/dev/peps/pep-0249/ 找到关于 Python 数据库 API 规范的详细信息。

## 10.1.3 SQLAlchemy 和 ibm_db_sa 适配器

SQLAlchemy 是一个开源 Python SQL 工具包和 **对象关系映射器**，为应用程序开发人员提供了 SQL 的全部功能和灵活性。SQLAlchemy 的核心称为 *"SQL 表达式语言"*，它允许用户使用基于函数的查询构建通过 Python 函数和表达式访问数据库，而不是使用普通的 SQL 语句。**ibm_db_sa** 适配器是一个基于 ibm_db_dbi 驱动程序构建的 Python 代码 DB2 适配器，并提供对 **SQLAlchemy** API 的支持。

在撰写本文时，ibm_db_sa 适配器支持 SQLAlchemy 0.4 规范 API。

> **注意：**
>
> 你可以在 http://www.sqlalchemy.org/ 找到更多关于 SQLAlchemy 的信息，包括 API 参考。

## 10.1.4 Django 框架和 ibm_db_django 适配器

Django 是一个流行的开源 Python Web 框架，用于快速应用程序开发。与 SQLAlchemy 类似，Django 框架 API 允许你通过 Python 函数和表达式访问数据库，而不是使用普通的 SQL 语句。**ibm_db_django** 适配器是一个基于 ibm_db_dbi 驱动程序构建的 Python 代码 DB2 适配器，并提供对 **Django** 框架 API 的支持。

在撰写本文时，支持 Django 1.2 规范 API。

> **注意：**
>
> 你可以在 http://www.djangoproject.com/ 找到更多关于 Django 框架的信息，包括 API 参考。

## 10.2 设置环境

要设置 Python 环境以与 DB2 配合工作，请遵循以下步骤：

- 1. 安装 Python 2.5 或更高版本。

你可以使用以下任一选项安装 Python：

- 使用 ActivePython 二进制分发包进行安装。

ActivePython 是由 ActiveState Software 提供的免费 Python 二进制分发包，适用于大多数操作系统。你可以从网站 http://www.activestate.com/activepython/downloads/ 下载它，并在 Windows 上运行 Windows 安装程序或在 Linux/UNIX 上运行 install.sh 来安装 Python。

- 在 Windows 上，你也可以从 http://www.python.org/download/ 下载免费的 Python Windows 安装程序，并通过运行 Windows 安装程序进行安装。

- 当然，对于所有操作系统，你也可以从 http://www.python.org/download/ 免费下载源代码并进行构建。

例如，要在 Linux 上从源代码构建和安装 Python 2.5.4，你可以下载源代码 `Python-2.5.4.tgz` 并使用 "`tar -zxvf Python-2.5.4.tgz`" 解压，然后切换到 `Python-2.5.4` 目录并运行 "`./configure`"、"`make`"、"`make install`" 命令来编译和安装 Python。

你可以通过运行以下命令验证 Python 版本：

```
python -V
```

- 2. 安装 **setuptools**

**setuptools** 是一个免费的程序，用于下载、构建、安装、升级和卸载 Python 包。你可以从 http://pypi.python.org/pypi/setuptools/ 下载它，并按照该网站的说明进行安装。你稍后可能需要它来安装某些 Python DB2 驱动程序。

- 3. 安装 IBM DB2 数据服务器客户端

安装上述软件后，你将能够安装 Python DB2 适配器和驱动程序。

## 10.2.1 Python 适配器 & 驱动程序

所有 Python-DB2 适配器和驱动程序都可以从 http://code.google.com/p/ibm-db/downloads/list 免费下载。或者，ibm_db/ibm_db_dbi 驱动程序和源代码也可以在 http://pypi.python.org/pypi/ibm_db 上获取。

如前一节所述，你可以根据想要使用的数据库 API 决定安装哪些驱动程序或适配器。例如，如果你想通过 IBM 定义的 API 或 Python 数据库 API 发出原始 SQL 语句，你只需安装 `ibm_db` 和 `ibm_db_dbi` 驱动程序。如果你想使用 SQLAlchemy 或 Django 框架，你不仅需要安装 `ibm_db_sa` 或 `ibm_db_django` 适配器，还需要安装这些适配器所基于的 `ibm_db`/`ibm_db_dbi` 驱动程序。

每个驱动程序或适配器的安装步骤在下节中说明。

### 10.2.1.1 安装 `ibm_db` 和 `ibm_db_dbi` 驱动程序

`ibm_db` 和 `ibm_db_dbi` 驱动程序捆绑在一个名为 `ibm_db` 包的安装包中。它们应该一起安装。在撰写本文时，这些驱动程序的最新版本是 1.0.2，并支持 Linux 和 Windows。

请遵循此步骤安装和设置这两个驱动程序：

- 1. 安装 ibm_db 包

如果你有互联网访问，在 Windows 上发出以下命令，如 *图 10.2* 所示： **easy_install ibm_db**

![](img/5f6ba170efa3a607142589708531bef8_340_0.png)

**图 10.2**- 使用 **easy_install** 从互联网安装 **ibm_db/ibm_db_dbi**

如 *图 10.2* 所示，**easy_install** 命令从互联网下载包，并将两个驱动程序安装在安装了 **setuptools** 的 site-packages 目录下。**easy_install** 是之前安装的 setuptools 包提供的程序。

如果你没有互联网访问，请从 [http://code.google.com/p/ibm-db/downloads/list](http://code.google.com/p/ibm-db/downloads/list) 下载适合你平台的 Python egg 文件，并发出以下命令：

```
easy_install <egg_file_name>
```

其中 <egg_file_name> 包含 egg 文件的路径。

例如，你可以使用下载的 egg 文件 **ibm_db-1.0.2-py2.5-win32.egg** 安装驱动程序，如 *图 10.3* 所示。

![](img/5f6ba170efa3a607142589708531bef8_341_0.png)

你也可以从源代码构建和安装驱动程序。从 http://pypi.python.org/pypi/ibm\_db/ 下载代码。说明文件包含在随驱动程序源代码提供的 README 文件中。你需要在你的平台上有一个 C 编译器来编译源代码中包含的 C 程序。

- 2. 创建一个名为 **PYTHONPATH** 的环境变量，并指定 ibm\_db egg 安装的路径。例如：

  - 在 Windows 上：

```
PYTHONPATH=<setuptools_install_path>\site-packages/<ibm_db-xx.egg>
```

  - 在 Linux (BASH shell) 上：

```
export PYTHONPATH=<setuptools_install_path>/site-packages/<ibm_db-xx.egg>
```

- 3. 从命令提示符开始，通过输入 **python** 进入 Python 交互式解释器，并输入类似于列表 10.1 的代码来测试连接，以测试你的设置。

```
(1) import ibm_db
(2) ibm_db_conn = ibm_db.connect('SAMPLE', 'db2admin', 'password')
(3) import ibm_db_dbi
(4) conn = ibm_db_dbi.Connection(ibm_db_conn)
(5) conn.tables('SYSCAT', '*')
```

列表 10.1 - 通过连接到一个 DB2 数据库来测试安装

在列表 10.1 中：

- (1) 导入 ibm_db 模块
- (2) 使用 ibm_db.connect 函数连接到 SAMPLE 数据库，其中 "db2admin" 是用户 ID，"password" 是


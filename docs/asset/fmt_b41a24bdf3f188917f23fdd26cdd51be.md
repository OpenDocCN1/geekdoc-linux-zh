
其中 `<egg_file_name>` 包含 egg 文件的路径。

例如，你可以使用下载的 egg 文件 `ibm_db-1.0.2-py2.5-win32.egg` 安装驱动程序，如 *图 10.3* 所示。

![](img/5f6ba170efa3a607142589708531bef8_341_0.png)

你也可以从源代码构建和安装驱动程序。从 `http://pypi.python.org/pypi/ibm_db/` 下载代码。说明文件包含在随驱动程序源代码提供的 README 文件中。你需要在你的平台上有一个 C 编译器来编译源代码中包含的 C 程序。

- 2. 创建一个名为 `PYTHONPATH` 的环境变量，并指定 `ibm_db` egg 安装的路径。例如：

  - 在 Windows 上：

```
PYTHONPATH=<setuptools_install_path>\site-packages\<ibm_db-xx.egg>
```

  - 在 Linux (BASH shell) 上：

```
export PYTHONPATH=<setuptools_install_path>/site-packages/<ibm_db-xx.egg>
```

- 3. 从命令提示符开始，通过输入 `python` 进入 Python 交互式解释器，并输入类似于列表 10.1 的代码来测试连接，以测试你的设置。

```
(1) import ibm_db
(2) ibm_db_conn = ibm_db.connect('SAMPLE', 'db2admin', 'password')
(3) import ibm_db_dbi
(4) conn = ibm_db_dbi.Connection(ibm_db_conn)
(5) conn.tables('SYSCAT', '*')
```

列表 10.1 - 通过连接到一个 DB2 数据库来测试安装

在列表 10.1 中：

- (1) 导入 `ibm_db` 模块
- (2) 使用 `ibm_db.connect` 函数连接到 SAMPLE 数据库，其中 "db2admin" 是用户 ID，"password" 是密码。您应该适当地替换这些值。我们将在后续章节中进一步讨论 `ibm_db.connect`。
- (3) 导入 `ibm_db_dbi` 模块
- (4) 调用函数 `ibm_db_dbi.Connection`
- (5) 列出架构 `SYSCAT` 下的所有表

### 10.2.1.2 安装 ibm_db_sa 适配器

在撰写本文时，支持 SQLAlchemy 0.4 的 `ibm_db_sa` 适配器最新版本 0.1.6 可在 Linux 和 Windows 上获取。

请按照以下步骤安装和设置 `ibm_db_sa` 适配器：

1. 安装 `ibm_db_sa` 包

如果您有互联网访问权限，请执行以下命令：

```
easy_install ibm_db_sa
```

此命令将从互联网下载该包，并将驱动安装在 *site-packages* 目录下。请注意，由于该适配器依赖于 `ibm_db`/`ibm_db_dbi` 驱动以及 `SQLAlchemy` 包，如果之前未安装这些依赖项，`easy_install` 将自动下载并安装它们。

例如，在 Windows 系统中，您可以从互联网安装适配器，如 *图 10.4* 所示。

![](img/5f6ba170efa3a607142589708531bef8_343_0.png)

如 *图 10.4* 所示，`easy_install` 命令将从互联网下载 `ibm_db_sa` 包以及所有先决条件包（如 `ibm_db`、`ibm_db_dbi` 和 `SQLAlchemy`），如果它们之前未安装，则会将它们安装在 setuptools 所在的 site-packages 目录下。

如果您没有互联网访问权限，请从 `http://code.google.com/p/ibm-db/downloads/list` 下载 Python egg 文件，并执行以下命令：

```
easy_install <egg_file_name>
```

其中 `<egg_file_name>` 包含 egg 文件的路径。

例如：

```
easy_install ibm_db_sa-0.1.6-py2.5.egg
```

请注意，如果您没有互联网访问权限，在安装 `ibm_db_sa` 包之前，应先安装依赖的 ibm-db 和 SQLAlchemy 包。

2. 在命令提示符中，输入 `python` 启动 Python 解释器，并输入类似于 *列表 10.2* 中的代码来测试 DB2 连接，从而测试您的设置。

```
(1) import sqlalchemy
    from sqlalchemy import *
(2) db2 = sqlalchemy.create_engine('ibm_db_sa://db2admin:password@localhost:50000/SAMPLE')
(3) metadata = MetaData()
(4) users = Table('users', metadata,
    Column('user_id', Integer, primary_key = True),
    Column('user_name', String(16), nullable = False),
    Column('email_address', String(60), key='email'),
    Column('password', String(20), nullable = False)
    )
(5) metadata.bind = db2
(6) metadata.create_all()
```

**列表 10.2 - 通过连接到 DB2 数据库来测试安装**

在 *列表 10.2* 中：

- (1) 导入 `sqlalchemy` 包
- (2) 创建一个 `db2` 数据库 Engine 对象，其中 "**SAMPLE**" 是你要连接的 **SAMPLE** 数据库，"**db2admin**" 是用户 ID，"**password**" 是密码，"**localhost:50000**" 是监听 50000 端口的本地实例。你应该适当替换为你自己的值。
- (3) 创建一个 `MetaData` 对象 `metadata`
- (4) 定义一个名为 `USERS` 的表
- (5) 将 `metadata` 对象绑定到 `db2` 引擎
- (6) 为所有表发出 `CREATE` 语句

### 10.2.1.3 安装 ibm_db_django 适配器

在撰写本文时，支持 Django 1.2 的 `ibm_db_django` 适配器最新版本 0.2.1 可在 Linux 和 Windows 上获取。

安装和设置 `ibm_db_django` 适配器的步骤如下：

1. 安装 Django 框架

由于适配器 `ibm_db_django` 依赖于 Django 框架包，因此在安装 `ibm_db_django` 适配器之前必须先安装 Django 框架。

请遵循 Django 网站 `http://docs.djangoproject.com/en/dev/topics/install/#installing-an-official-release` 上的说明安装 Django。

2. 如果你使用的是 Django 1.0.2，还需要在 Django 中应用一个补丁，以解决非标准 SQL 生成问题。对于 1.0.2 以上版本，无需补丁。有关补丁的详细信息位于 `http://code.djangoproject.com/ticket/9862`

- 从 `http://code.djangoproject.com/changeset/9703?format=zip&new=9703` 的补丁 zip 文件中提取 `creation.py` 文件
- 将此 `creation.py` 复制到 Django 安装目录下的 `site-packages/django/db/backends/`

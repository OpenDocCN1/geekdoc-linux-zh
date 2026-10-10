
密码。您应该适当地替换这些值。我们将在后续章节中进一步讨论 **ibm_db.connect**。

(3) 导入 **ibm_db_dbi** 模块

(4) 调用函数 **ibm_db_dbi.Connection**

(5) 列出架构 **SYSCAT** 下的所有表

### 10.2.1.2 安装 ibm_db_sa 适配器

在撰写本文时，支持 SQLAlchemy 0.4 的 ibm_db_sa 适配器最新版本 0.1.6 可在 Linux 和 Windows 上获取。

请按照以下步骤安装和设置 ibm_db_sa 适配器：

1.  安装 **ibm_db_sa** 包

    如果您有互联网访问权限，请执行以下命令：

    ```
    easy_install ibm_db_sa
    ```

    此命令将从互联网下载该包，并将驱动安装在 *site-packages* 目录下。请注意，由于该适配器依赖于 ibm_db/ibm_db_dbi 驱动以及 **SQLAlchemy** 包，如果之前未安装这些依赖项，**easy_install** 将自动下载并安装它们。

    例如，在 Windows 系统中，您可以从互联网安装适配器，如 *图 10.4* 所示。

![](img/5f6ba170efa3a607142589708531bef8_343_0.png)

如 *图 10.4* 所示，**easy_install** 命令将从互联网下载 **ibm_db_sa** 包以及所有先决条件包（如 **ibm_db**、**ibm_db_dbi** 和 **SQLAlchemy**），如果它们之前未安装，则会将它们安装在 setuptools 所在的 site-packages 目录下。

如果您没有互联网访问权限，请从 [http://code.google.com/p/ibm-db/downloads/list](http://code.google.com/p/ibm-db/downloads/list) 下载 Python egg 文件，并执行以下命令：

```
easy_install <egg_file_name>
```

其中 **<egg_file_name>** 包含 egg 文件的路径。

例如：

```
easy_install ibm_db_sa-0.1.6-py2.5.egg
```

请注意，如果您没有互联网访问权限，在安装 **ibm_db_sa** 包之前，应先安装依赖的 ibm-db 和 SQLAlchemy 包。

2.  在命令提示符中，输入 **python** 启动 Python 解释器，并输入类似于 *列表 10.2* 中的代码来测试 DB2 连接，从而测试您的设置。

    ```
    (1) import sqlalchemy
        from sqlalchemy import *
    (2) db2 = sqlalchemy.create_engine('ibm_db_sa://db2admin:password
        @localhost:50000/SAMPLE')
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

    -   (1) 导入 *sqlalchemy* 包
    -   (2) 创建一个 **db2** 数据库 Engine 对象，其中 "**SAMPLE**" 是你要连接的 **SAMPLE** 数据库，"**db2admin**" 是用户 ID，"**password**" 是密码，"**localhost:50000**" 是监听 50000 端口的本地实例。你应该适当替换为你自己的值。
    -   (3) 创建一个 *MetaData* 对象 *metadata*
    -   (4) 定义一个名为 *USERS* 的表
    -   (5) 将 metadata 对象绑定到 *db2* 引擎
    -   (6) 为所有表发出 **CREATE** 语句

### 10.2.1.3 安装 ibm_db_django 适配器

在撰写本文时，支持 Django 1.2 的 ibm_db_django 适配器最新版本 0.2.1 可在 Linux 和 Windows 上获取。

安装和设置 ibm_db_django 适配器的步骤如下：

1.  安装 Django 框架

    由于适配器 ibm_db_django 依赖于 Django 框架包，因此在安装 ibm_db_django 适配器之前必须先安装 Django 框架。

    请遵循 Django 网站 http://docs.djangoproject.com/en/dev/topics/install/#installing-an-official-release 上的说明安装 Django。

2.  如果你使用的是 Django 1.0.2，还需要在 Django 中应用一个补丁，以解决非标准 SQL 生成问题。对于 1.0.2 以上版本，无需补丁。有关补丁的详细信息位于 [http://code.djangoproject.com/ticket/9862](http://code.djangoproject.com/ticket/9862)
    -   从 [http://code.djangoproject.com/changeset/9703?format=zip&new=9703](http://code.djangoproject.com/changeset/9703?format=zip&new=9703) 的补丁 zip 文件中提取 `creation.py` 文件
    -   将此 `creation.py` 复制到 Django 安装目录下的 `site-packages/django/db/backends/`

3.  如果尚未安装，请安装 `ibm_db`/`ibm_db_dbi` 驱动 0.7.2.5 或更高版本。有关详细信息，请参阅前一节“*安装 ibm_db 和 ibm_db_dbi 驱动*”。

4.  安装 `ibm_db_django` 包
    -   从 [http://code.google.com/p/ibm_db/downloads/list](http://code.google.com/p/ibm_db/downloads/list) 下载 `ibm_db_django` 源代码 `ibm_db_django-x.x.x.tar.gz`，其中 `x.x.x` 指的是驱动程序版本。
    -   解压 gz 文件 `ibm_db_django-x.x.x.tar.gz`
    -   执行以下命令进行安装：
        ```
        cd ibm_db_django
        python setup.py install
        ```

5.  通过测试到 DB2 的连接来验证 `ibm_db_django` 适配器的安装
    -   执行以下命令创建一个新的 Django 项目：
        ```
        django-admin.py startproject myproj
        ```
    -   进入新创建的目录，并按照 *列表 10.3* 中所示编辑 `settings.py` 文件。
    -   (1) `DATABASE_ENGINE = 'ibm_db_django'`
    -   (2) `DATABASE_NAME = 'SAMPLE'`
    -   (3) `DATABASE_USER = 'db2admin'`
    -   (4) `DATABASE_PASSWORD = 'password'`
    -   **列表 10.3 - settings.py**

    其中：

    -   1. "`ibm_db_django`" 表示你想要访问 DB2 数据库服务器。这是从 django 适配器版本 0.1.2 开始的一种新格式。对于较早版本的 django 适配器，请使用 `DATABASE_ENGINE` = '`db2`'。
    -   2. "`SAMPLE`" 指的是 **SAMPLE** 数据库。
    -   3. "db2admin" 是用户 ID，你可以替换为你自己的 ID。
    -   4. "password" 是密码，你可以替换为你自己的密码。

    执行测试套件：

    `python manage.py test`

    > **注意：**
    > 上述所有四个 Python DB2 驱动程序的开源项目主页可在 <http://code.google.com/p/ibm-db/> 找到。

## 10.3 开发 Python DB2 应用程序

为简洁起见，本节仅关注 **ibm_db** 驱动，它为访问 DB2 数据服务器提供了最佳性能和最先进的功能支持。关于其他所有驱动程序或适配器，请参阅其 API 规范。

### 10.3.1 连接到 DB2 数据库

你首先必须在 Python 脚本中包含以下行以导入 **ibm_db** 驱动模块：

`import ibm_db`

然后，通过调用函数 **ibm_db.connect** 连接到 DB2 数据库，语法如下：

`IBM_DBConnection ibm_db.connect (string dsn, string user, string password[, array options])`

*表 10.1* 解释了 **ibm_db.connect** 的参数。

| 名称 | 描述 |
| :--- | :--- |
| **dsn** | 格式为 "**DATABASE=database; HOSTNAME=hostname; PORT=port; PROTOCOL=TCPIP; UID=username; PWD=password;**" 的数据库连接字符串 |
| **user** | 用于连接数据库的用户名；如果 **dsn** 字符串中已指定用户名，则指定空字符串 "" |
| **password** | 用于连接数据库的密码；如果 **dsn** 字符串中已指定密码，则指定空字符串 "" |
| **options** | 可选：一个连接选项字典，影响连接的行为。 |

*表 10.1* - 函数 **ibm_db.connect** 的参数

例如，如果 **SAMPLE** 是在客户端本地注册的数据库别名，你可以按照 *列表 10.4* 所示与其建立连接：

```
import ibm_db
conn = ibm_db.connect ("SAMPLE", "db2admin", "password")
```

**列表 10.4 – 连接到本地注册的 SAMPLE 数据库**

如果 **SAMPLE** 数据库是位于机器 *host:2* 上的远程数据库，实例监听端口 50000，且尚未在你的客户端中注册，你可以直接通过 TCP/IP 与其建立连接，如 *列表 10.5* 所示：

```
import ibm_db
conn = ibm_db.connect ("DATABASE=SAMPLE; HOSTNAME=host:2; PORT=50000;\nPROTOCOL=TCPIP; UID=db2admin; PWD=password;", "", "")
```

**列表 10.5 – 直接通过 TCP/IP 连接到远程 SAMPLE 数据库**

如果连接尝试成功，函数 **ibm_db.connect** 将返回一个 **ibm_db.IBM_DBConnection** 对象，该对象将在后续用于执行特定于此连接的进一步数据库操作，例如执行 SQL 语句以检索、插入、更新或删除数据。

> **注意：**
> ibm_db 驱动还支持创建持久连接，这些连接在关闭后仍保持活动状态在连接池中，并允许后续的连接请求重用具有相同凭据集的现有连接。有关详细信息，请检查函数 ibm_db.pconnect 的 API 规范
> [http://code.google.com/p/ibm-dbl/wiki/APIs](http://code.google.com/p/ibm-dbl/wiki/APIs)

### 10.3.2 检索数据

如果在编写应用程序时 SQL 语句未知，请参阅 *章节 10.3.4*，了解如何运行包含变量输入或参数标记的 SQL。

如果 SQL 语句已知，请遵循以下步骤选择和获取数据：

1.  使用 **ibm_db.connect** 函数连接到数据库，如果连接成功，该函数将返回数据库连接对象。
2.  通过调用函数 **ibm_db.exec_immediate** 直接执行 SQL **SELECT** 语句，如果 SQL 语句执行成功，该函数将返回与结果集关联的语句对象。

函数 **ibm_db.exec_immediate** 的语法如下：

```
IBM_DBStatement ibm_db.exec_immediate( IBM_DBConnection connection,
string statement [, array options])
```

*表 10.2* 解释了 **ibm_db.exec_immediate** 的不同参数。


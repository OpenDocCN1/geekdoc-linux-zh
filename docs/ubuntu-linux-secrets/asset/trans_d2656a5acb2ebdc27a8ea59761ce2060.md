

模型代码为应用程序中使用的每个表创建一个 Ruby 类。模型代码实现了 CRUD 的每个元素，以创建、读取、更新和删除表中的数据。所有与数据库的交互都通过模型代码执行。

控制器代码实现了客户端在应用程序中执行的操作，称为应用程序的表述性状态转移（缩写为 REST）。Web 应用程序的每个表述性状态都表示客户端针对应用程序中的数据所请求的操作，例如查看、添加或删除数据。表 29-3 显示了 Rails 中实现的 REST 操作。

### 表 29-3：Rails 的 REST 操作

| 操作 | 描述 |
| --- | --- |
| create | 从 HTML 表单中检索数据并创建表中的新数据记录 |
| destroy | 从表中删除现有数据记录 |
| edit | 为表中的现有数据记录显示 HTML 表单 |
| index | 显示表中所有记录的信息 |
| new | 显示用于在表中输入新数据记录的 HTML 表单 |
| show | 显示表中单条数据记录的值 |
| update | 从编辑表单中检索数据并更新表中现有数据记录的值 |

Rails 控制器代码生成一个 Ruby 类文件，其中包含应用程序中每个 REST 操作的方法。

视图代码使用 HTML 和 ERb 代码在网页中实现控制器代码的每个操作。它使用 ERb 代码检索控制器代码中计算出的数据元素，并将其显示在网页上。

感受 Rails 的最佳方式是亲自实践。以下各节将带领你在 Ubuntu 系统上创建并测试一个简单的 Rails 应用程序。

## 创建项目

要创建新的 Rails 项目，你需要使用 rails 程序。rails 程序会自动生成项目的基础框架代码，帮助你快速入门。

在本例中，我们将创建一个在线通讯录，用于存储朋友的姓名、地址和电话号码。首先，我们需要生成 Rails 项目框架。在工作站的终端会话或服务器的命令行中，输入以下命令：

```
$ rails addressbook
```

Rails 软件会在当前文件夹下创建一个名为 addressbook 的新文件夹，并在其中创建许多文件和文件夹。

自 Rails 2.0 起，Rails 默认使用 SQLite3 数据库系统来存储数据值。SQLite3 数据库系统使用单个文件来存储数据库中的所有表。Rails 流程的一部分是创建应用程序所使用的数据库文件。

如果你更倾向于使用 MySQL 服务器来存储 Rails 项目数据库，则必须确保你的 Ubuntu 服务器上已安装 MySQL。你可以通过安装 Ubuntu 服务器上的 LAMP 服务器（参见第 21 章“LAMP 服务器”）来实现，或者如果你不想同时安装 Apache 和 PHP，则仅安装 MySQL 服务器软件包。

确保已安装 MySQL 服务器后，你需要从 Synaptic 或 apt-get 添加名为 libmysql-ruby 的 MySQL Rails 库文件。这样 Rails 就可以从项目代码中访问 MySQL 数据库服务器。

在 Rails 和 MySQL 环境安装完成后，你可以在 rails 命令行中指定 MySQL 数据库：

```
rails -d mysql addressbook
```

Rails 应用程序会在为 Rails 项目创建的 config 文件夹中生成一个名为 database.yml 的文件。你需要编辑此文件，为你的 MySQL 服务器添加 MySQL root 用户帐户的密码。

创建 Rails 项目环境后，你就可以开始编写应用程序代码了。首先，你需要进入由 rails 命令新建的应用程序文件夹：

```
rich@testbox:~$ cd addressbook
rich@testbox:~/addressbook$
```

Rails 框架会创建一系列用于与 Rails 环境交互的 Ruby 脚本。generate 脚本会自动创建模型、控制器和视图代码文件。

Rails 还包含一个名为 scaffold 的特殊生成选项。scaffold 选项会创建模型和控制器代码文件，以及实现命令行中定义的表的完整 CRUD Web 应用程序所需的所有视图代码文件。

你只需定义控制器名称，以及表中所需的数据字段和数据类型。具体做法如下：在新建的 addressbook 文件夹中（确保你位于 addressbook 文件夹中，否则此过程将无法正常工作），输入以下命令（在一行内）：

```
rich@testbox:~/addressbook$ ruby script/generate scaffold person lastname:string firstname:string address:string city:string state:string zip:string phone:string comments:text
```

此命令仅是一条语句，应全部位于同一命令行上。它会生成实现 person 控制器所需的所有 MVC 文件，并与名为 people 的数据库表交互（Rails 会将所有表名从模型名变为复数形式）。



# 使用 Python

66 Python 职业应用
将你的技能用于专业场景

74 为 XBMC 制作扩展
通过本教程增强 XBMC 功能

80 科学计算
掌握 NumPy

84 即时通讯
使用 Python 开启聊天

90 清除代码中的 bug
确保你的软件项目安全

94 复制：创建一个属于自己的 cp
用 Python 3 开发 cp 的轻量级版本

98 查收邮件
创建一封封收信的清单

100 让你的 Pi 多任务处理
在你的 Python 代码中添加多任务功能

![](img/e016e192a91ffc1a9e474690a590742f_63_0.png)

> “大多数 Linux 发行版都包含一个 Python 解释器，用于运行系统脚本”

# 74

# 80

| 附加组件信息 |
| :--- |
| **LUUD Reddit Viewer** |
| **类型**：媒体源 |
| **作者**：LUD |
| **版本**：0.0.1 |
| **评分**：★☆☆☆☆ |
| **摘要**：LUUD Ent 示例 |
| **描述** |
| LUUD 示例附加组件，用于演示 XBMC 扩展系统。来源：AddonScript0xDE |

- 配置
- 更新
- 卸载
- 禁用
- 回滚
- 变更日志

![](img/e016e192a91ffc1a9e474690a590742f_64_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_65_0.png)

使用 Python

![](img/e016e192a91ffc1a9e474690a590742f_65_1.png)

# 职业 Python 应用

Python 被全世界的 Web 开发者、工程师和学术研究人员所依赖。以下是如何将你的 Python 技能用于专业场景

66 Python 书籍

## 系统管理

在系统日常维护中充分发挥 Python 的作用，保持系统健康

系统管理任务是**在维护自有系统时最令人生烦的事情**之一。正因如此，系统管理员一直在寻找方法来自动化这类任务，以最大化利用时间。他们最初使用基本的 shell 脚本，随后转向各种脚本语言。长期以来，Perl 一直是开发此类维护工具的首选语言。然而，Python 如今正逐渐成为常用的语言。它已发展到大多数 Linux 发行版都包含 Python 解释器以运行系统脚本的地步，因此你不应该有任何借口不编写自己的脚本。由于你将进行大量的系统级工作，你将对几个关键的 Python 模块有最大需求。第一个模块是 `os`。此模块提供了与底层系统交互的大部分接口。通常的第一步是查看脚本运行的环境，看看那里可能存在什么信息来帮助引导脚本。以下代码提供了一个映射对象，你可以与当前活跃的环境变量进行交互：

```python
import os
os.environ
```

你可以使用函数 `os.environ.keys()` 获取可用环境变量的列表，然后使用 `os.environ[key]` 访问单个变量。当你生成子进程时，也会使用这些环境变量。因此，你需要更改诸如 PATH 或当前工作目录等值，以便正确运行这些子进程。虽然有一个 "putenv" 函数可以为你编辑这些值，但遗憾的是它在所有系统上并不都存在。因此，更好的方法是直接编辑环境映射中的值。

你可能想要自动化的另一类任务涉及文件操作。例如，你可以使用类似以下代码获取当前工作目录：

```python
cwd = os.getcwd()
```

然后你可以使用以下代码获取该目录中文件的列表：

```python
os.listdir(cwd)
```

你可以使用函数 `os.chdir(new_path)` 在文件系统中移动。一旦你找到了你感兴趣的某个文件，你可以使用 `os.open()` 打开它，并设置为读、写和/或追加模式。然后你可以使用函数 `os.read()` 和 `os.write()` 对其进行读取或写入。完成后，你可以使用 `os.close()` 关闭文件。

![](img/e016e192a91ffc1a9e474690a590742f_66_0.png)

## 从 Python 运行子进程

Unix 的底层哲学是构建小型、专用的程序，每一种程序都极其擅长执行一项任务。然后你将它们串联起来以构建更复杂的行为。没有理由不在你的 Python 脚本中使用同样的哲学。有几个实用程序可供使用，只需你很少的工作。处理此事的旧方法是使用 os 模块中的函数如 `popen()` 和 `spawn()`，但运行其他程序的更好方法是使用 subprocess 模块。然后你可以使用以下代码启动程序，如 ls：

```python
import subprocess
subprocess.run("ls", "-l")
```

这为你提供当前目录的长文件列表。函数 `run()` 在 Python 3.5 中引入，是处理此事的建议方式。如果你有更旧的版本，或者需要比那更多的控制，那么你可以使用我们之前提到的底层 `popen()` 函数。如果你想获取输出，可以使用以下代码：

```python
cmd_output = subprocess.run(["ls", "-l"], stdout=subprocess.PIPE)
```

变量 `cmd_output` 是一个 CompletedProcess 对象，包含返回码和一个持有 stdout 输出的字符串。

## 使用 cron 进行调度

一旦你写好了脚本，你可能希望安排它们自动运行而无需你的干预。在 Unix 系统上，你可以使用 cron 按照所需的任何时间表运行你的脚本。实用程序 `crontab -l` 列出你的 cron 文件的当前内容，而 `crontab -e` 允许你编辑你想让 cron 运行的计划任务。

# Web 开发

Python 为你的各种 Web 开发任务提供了多个框架。我们将探讨一些更流行的框架

随着内容和大量计算托管在服务器上，Web 应用能够更好地保证最终用户的一致体验。流行的 Django 框架提供了一个非常完整的插件环境，并遵循 DRY 原则（不要重复你自己）。因此，你应该能够非常快速地构建你的 Web 应用。由于 Django 基于 Python 构建，你应该可以使用 "sudo pip install Django" 安装它。大多数发行版也应该有 Django 的包。取决于你想用应用做什么，你可能需要安装像 MySQL 或 postgresql 这样的数据库来存储你的应用数据。

有 Django 工具可以自动为你的新项目代码生成起点：

```
django-admin startproject newsite
```

此命令创建一个名为 "manage.py" 的文件和一个名为 "newsite" 的子目录。文件 "manage.py" 包含几个你可以用来管理新应用的实用函数。新创建的子目录包含文件 "__init__.py"、"settings.py"、"urls.py" 和 "wsgi.py"。这些文件及它们所在的子目录组成一个 Python 包，在你的网站启动时加载。你网站的核心配置可以在文件 "settings.py" 中找到。URL 声明，基本上是你网站的目录，存储在文件 "urls.py" 中。文件 "wsgi.py" 包含 WSGI 兼容 Web 服务器的入口点。

一旦你的应用完成，它应该托管在一个配置正确且加固的 Web 服务器上。但是，如果你在开发 Web 应用的过程中，这并不方便。为了帮助你，Django 在框架中内置了一个 Web 服务器。你可以通过更改目录到 "newsite" 项目目录并运行以下命令来启动它：

![](img/e016e192a91ffc1a9e474690a590742f_67_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_67_1.png)

左 Python 解释器与你的数据库合作以支持 Web 服务器

底 模型-视图-控制器架构常用于 UI

```
python manage.py runserver
```

这将启动一个监听本地机器 8000 端口的服务器。由于此内置服务器设计用于开发，它会为每个请求自动重新加载你的 Python 代码。这意味着你不需要重启服务器就能看到你的代码更改。

所有这些步骤让你拥有一个可运行的项目。你现在准备好开始开发你的应用了。在 "newsite" 子目录中，你可以输入：

```
python manage.py startapp newapp
```

这将创建一个名为 "newapp" 的新子目录，其中包含文件 "models.py"、"tests.py" 和 "views.py"，以及其他文件。最简单的视图由以下代码组成：

```
from django.http import HttpResponse
def index(request):
    return HttpResponse("Hello world!")
```

然而，这不足以使其可用。你还需要为视图创建一个 URLconf。如果文件 "urls.py" 尚不存在，创建它并添加代码：

```
from django.conf.urls import url
from newapp import views
urlpatterns = [ url(r'^*$', views.index, name='index'), ]
```

最后一步是在你的项目中注册 URL。你可以使用以下代码完成：

```
from django.conf import include, url
from django.contrib import admin
urlpatterns = [ url(r'^newapp/', include('newapp.urls')), ]
```

# 虚拟环境

当你开始开发自己的应用时，你可能开始陷入依赖地狱。几个 Python 包依赖于其他 Python 包。这是它的强项，也是它的弱点。幸运的是，你有 virtualenv 可以用来驯服这个丛林。

你可以为你的每个项目创建新的虚拟 Python 环境。谢天谢地，通过这样做，你可以创建隔离的环境来捕获你的包的依赖关系。


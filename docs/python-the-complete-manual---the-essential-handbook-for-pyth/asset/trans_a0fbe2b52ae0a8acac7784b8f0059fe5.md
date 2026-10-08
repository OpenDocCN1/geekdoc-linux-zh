

# 介绍 Python

# Python 基础

## 介绍 Python

奠定基础并构建你的知识

既然你已经迈出了 Python 的第一步，现在是时候利用这些知识来编写代码了。在本节中，你将了解到如何为 Android 操作系统（第32页）和全球网（第26页）开始编写应用程序。这些简单易懂的教程将帮助你巩固所学会的 Python 语言，同时开发一项在当前技术市场上非常有用的技能。最后，我们将为你提供 50 个核心 Python 技巧（第40页），帮助你快速增加知识储备。

![](img/c72194f2c3aec198936695a665a5167c_23_0.png)

![](img/c72194f2c3aec198936695a665a5167c_24_0.png)

# 介绍 Python

使用 Python 开发 Web 应用

### 你需要准备的……

- Python 2.7: https://www.python.org/download/release-2.7/
- Django 版本 1.4: https://www.djangoproject.com/

## 使用 Python 开发 Web 应用

Python 提供了一种快速简单构建应用程序的方法，包括 Web 应用。了解如何使用它来构建一个功能完备的 Web 应用

Python 以简单性和强大的功能而闻名。目前，它已经先进到几乎没有什么是 Python 做不到的，而征服网络只是其中的可能性之一。当你使用 Python 进行 Web 开发时，你可以获得海量的模块库和社区支持——请充分利用它们。

Web 开发可以通过许多不同的方式实现，从使用原始的 CGI 模块到利用成熟的 Web 框架。使用后者是使用 Python 构建 Web 应用最流行的方法，因为它允许你构建应用程序而无需担心所有底层的实现细节。Python 有许多 Web 框架可用，例如 Django、TurboGears 和 Web2Py。在本教程中，我们将使用我们目前的首选方案：Django。

### Django 项目杂志问题跟踪器

01 `django-admin.py` 文件用于创建新的 Django 项目。让我们为我们的问题跟踪器项目创建一个……

在 Django 中，项目（project）代表网站及其设置。而应用程序（application）代表网站的特定功能，如博客或标签。这种方法的好处是，你的应用程序变得可移植，并且可以以很小的代价与其他 Django 网站集成。

```bash
$ django-admin.py startproject issueTracker
```

将创建一个目录。这将作为你包含 Django 的开发 Web 服务器的根。在项目目录下，你将找到以下项：

- **manage.py**: 用于操作项目的 Python 脚本。
- **issueTracker**: 项目的 Python 包（一个包含 `__init__.py` 文件的项目目录）。

![](img/c72194f2c3aec198936695a665a5167c_25_0.png)

该包包含了你的项目设置和配置数据。
- `issueTracker/settings.py`: 该文件包含项目的所有配置。
- `issueTracker/urls.py`: 该文件包含 URL 映射。
- `wsgi.py`: WSGI 兼容 Web 服务器提供你项目的入口点。只有在你部署项目时才需要它。在本教程中我们不需要它。

现在更新路径选项：
```python
TEMPLATE_DIRS = (
    getabspath('templates'),
)

MEDIA_ROOT = getabspath('media')
MEDIA_URL = '/media/'
```

我们还需要在配置文件中启用它：
```python
INSTALLED_APPS = (
    'django.contrib.admin',
    'issuedis',
)
```

现在我们将为你的站点启用管理界面。这是 Django 的一个功能，允许自动创建网站的管理界面，并用于添加和管理网站的内容。取消以下行的注释：

### 配置 Django 项目

02 在开始开发应用程序之前，根据我们的需求配置 Django 项目。编辑 `issueTracker/settings.py` 如下（仅显示需要修改的部分）：
数据库设置：我们使用 SQLite3 作为数据库系统。
注意：文本编辑表示新代码或更新后的代码。

```python
'default': {
    'ENGINE': 'django.db.backends.sqlite3',
    'NAME': 'issuedis',
},
```

### 创建 issuedis 应用

03 在这一步中，我们为网站创建主应用 `issuedis`。为了实现这一点，我们将使用 manage 脚本：

```bash
$ python manage.py startapp issuedis
```

Django 要求目录设置使用绝对路径。但我们希望传递相对目录引用。为了实现，我们将添加一个辅助函数。将代码插入设置文件的顶部。

```python
import os
def getabspath(path):
    return os.path.join(os.path.abspath(__file__), path)
```

```python
INSTALLED_APPS = (
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.sites',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.admin',
    'issuedis',
)
```

### 创建数据模型

04 这部分是我们为应用定义数据模型。请查看注释以理解这里发生了什么。

```python
from django.db import models
# 我们正在导入在此应用中内置的用户身份认证模块
from django.contrib.auth import models
# 我们还将为应用创建一个管理界面
from django.db import admin

# 一个用于存储多字符字段的元组。
# 第一个表示显示名称的字段名
ISSUE_STATUS_CHOICES = (
    ('New', 'New'),
    ('accepted', 'Accepted'),
    ('reviewed', 'Reviewed'),
    ('started', 'Started'),
    ('closed', 'closed')
)

class Issue(models.Model):
    # owner 将是 Django 内置的 User 模型的外键
    owner = models.ForeignKey(
        models.User, null=True, blank=True, default="new"
    )
    status = models.CharField(
        max_length=20,
        choices=ISSUE_STATUS_CHOICES,
        default="new"
    )
    text = models.TextField()
    opened_on = models.DateTimeField(auto_now_add=True)
    modified_on = models.DateTimeField(auto_now=True)

class IssueAdmin(models.ModelAdmin):
    list_display = ('id', 'text', 'status', 'modified_on')
    list_filter = ('status', 'owner')
    date_hierarchy = 'opened_on'
    search_fields = ('text', 'status')

admin.register(Issue, IssueAdmin)
```

### 启用管理站点

05 管理站点已经启用，但我们需要在 `urls.py` 中启用它。如下所示更新 `urls.py` 文件：

```python
from django.conf.urls import path
from django.urls import include
from django.contrib import admin

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('issuedis.urls')),
]
```

### 启动 Django Web 服务器

06 Django 包含一个内置 Web 服务器，对于测试和调试 Django 应用程序非常方便。让我们看看我们的管理界面……启动 Web 服务器：

```bash
$ python manage.py runserver
```

如果你的代码没有错误，服务器应该在 8000 端口可用。要启动管理界面，请访问 `http://localhost:8000/admin`。系统会要求登录。输入用户名和密码。


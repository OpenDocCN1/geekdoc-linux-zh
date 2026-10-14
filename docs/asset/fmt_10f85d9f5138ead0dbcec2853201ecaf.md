
| 权限 | 角色 |  |  |
| --- | --- | --- | --- |
| Acquire permission settings? | Anonymous | Manager | WebsiteUser |
| Access contents information |  |  |  |
| Change HTML Methods |  |  |  |
| Change cache settings |  |  |  |
| Change permissions |  |  |  |
| Change proxy roles |  |  |  |
| Delete objects |  |  |  |
| FTP access |  |  |  |
| Manage properties |  |  |  |
| Take ownership |  |  |  |
| Undo |  |  |  |
| View |  |  |  |
| View History |  |  |  |
| View management screens |  |  |  |

图 5-5：DTML 内容 `login_html` 的权限分配

```python
permissions_for_WebsiteUsers = []

for item in old permissions:
    if item['name']=='View':
        permissions_for_websiteUsers.append(item['name'])
    else:
        new_permissions.append(item['name'])

instance.login_html.manage_acquiredPermissions(new_permissions)
instance.login_html.role('WebsiteUser', permissions_for_WebsiteUsers)

if REQUEST is not None:
    return self.manage_main(self, REQUEST)
```

## 15.4.5 编写 `__init__.py`

Zope 使用 `__init__.py` 来识别一个产品，并在每次 Zope 服务器启动时为每个产品执行 `__init__.py` 文件。如果一个产品包含一个字节码编译版本的 `__init__.py`（可以通过文件扩展名 `.py` 识别），启动时会进行检查，查看编译版本的修改日期是否比产品目录中的未编译版本更新。如果未编译的 `__init__.py` 的修改日期更新，则会从该文件编译一个新的 `__init__.py`。因此，如果你更改了 `__init__.py` 中的代码，当你重启 Zope 时将自动生成一个新的 `__init__.py`；编译仅在启动 Zope 服务器时发生，每当你对产品的 Python 文件（如 `__init__.py` 文件、主模块等）进行更改时，必须重启。如果你发现 Zope 安装了错误版本的产品，你必须从 Zope 控制面板中的 `Product_Management` 列表中删除你的产品，并重启 Zope 服务器以安装你的新版本产品。

[Refresh](http://www.zope.org/Almembers/Hathaw/Refresh/) 允许你在不重启整个 Zope 服务器的情况下重新编译并加载单个产品。此功能包含在 Zope 2.4.0 及更高版本中。

### 15.4.5.1 `__init__.py` 概述

一旦你创建了 `Website.py`，请在 `__init__.py` 文件中执行以下操作：

- 将产品导入到 `Website`。
- 定义 `initialize` 函数，该函数由 Zope 调用以注册你的产品。
- 在 `initialize` 函数中，调用内置的 `registerClass` 方法，并提供类、构造函数、添加的权限名称和图标路径。

### 15.4.5.2 导入主模块

为了访问我们在 15.4.2.3 节中创建的 `Website` 模块中定义的函数和类，我们必须使用以下代码语句导入它：

```python
import Website
```

### 15.4.5.3 定义 `Initialize` 函数

当 Zope 启动时，它将导入我们的产品目录，从而执行我们正在创建的 `__init__` 文件。一旦 Zope 导入产品，它会检查是否定义了一个名为 `initialize` 的函数。如果是，Zone 将为该产品调用此函数，并将注册上下文对象传递进去。该对象包含了 `registerClass` 方法，用于向 Zope 注册产品的类。

`Website__init__` 使用以下代码打开 `initialize` 函数定义：

```python
def initialize(context):
    """注册网站类"""
```

产品的 `Initialize` 函数通常会包含对 `context` 对象 `registerClass` 方法的一次或多次调用（由 Zone 传递）。该对象包含 `registerClass` 方法，用于将产品的类注册到 Zope。

表 15-4：`registerClass` 参数

| 参数 | 描述 |
| :--- | :--- |
| `instance_class` | 要注册的类 |
| `constructors` | 创建实例的方法 |
| `permission` | 创建实例所需的权限名称 |
| `icon` | 用作图标的文件的相对路径 |
| `permissions` | 用于该类的权限列表 |

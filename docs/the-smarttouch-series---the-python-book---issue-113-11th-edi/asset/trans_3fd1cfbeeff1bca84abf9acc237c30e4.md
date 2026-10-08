

## Web开发

### 自动装配管理界面

管理部分本身可能存在问题。Django 为你提供了一个可扩展的管理界面

![](img/e016e192a91ffc1a9e474690a590742f_136_0.png)

#### 01 创建管理用户

Django 使得内容管理变得极其简单，并且在默认项目中标准地提供了位于 http://127.0.0.1:8000/admin/ 的管理部分。要登录，你需要创建一个超级用户账户。运行相关命令，根据需要指定用户详情，然后继续登录。

```python
python manage.py createsuperuser
```

![](img/e016e192a91ffc1a9e474690a590742f_136_1.png)

#### 02 开启博客管理

登录管理界面后，你将看到管理用户和组角色及权限的功能，这些功能本身非常强大，由 Django 提供给你。然而，目前尚无法访问来管理我们的博客文章，因此让我们将其开启。

## 使用开发服务器

Django 附带了一个非常有用的内置开发服务器，在你完成所有文件更改后，它会自动编译并重新加载，从而帮助你。你只需在项目的目录中通过终端窗口运行 'python manage.py runserver' 命令即可启动服务器。

#### 03 启用管理管理

为了通过管理界面对我们的模块及相关模型进行管理，我们需要将它们注册到 admin 模块中。打开 blog/admin.py，然后依次导入并注册模型（尽管目前我们只有一个）。保存文件并刷新管理站点，即可看到现在可供管理的文章。

```python
from django.contrib import admin

# Register your models here.
```

#### 04 创建一个视图

随着管理界面接受针对我们 post 类的新提交，我们将创建一个视图页面来显示它们。打开 blog/views.py，并从模型中导入 Post 类。创建一个方法，用于从数据库获取所有文章并将它们作为字符串输出。

```python
from django.http import HttpResponse
from blog.models import Post

def index(request):
    post_list = Post.objects.order_by('-id')[:5]
    output = '<br />'.join([p.title for p in post_list])
    return HttpResponse(output)
```

#### 05 管理 URL

创建 'blog/urls.py'，并添加代码以导入刚刚在该模块中创建的视图以及相应的 URL 模式。打开 myblog/urls.py，并添加 URL 函数调用，以实现一个新 URL 供应用显示该视图。在你的浏览器中访问 http://127.0.0.1:5000/blog 以渲染新视图。

```python
# blog/urls.py
from django.conf.urls import patterns, url
from blog import views

urlpatterns = patterns('',
    url(r'^$', views.index, name="index"),
)

# myblog/urls.py
urlpatterns += patterns('',
    url(r'^blog/', include('blog.urls')),
    url(r'^admin/', include(admin.site.urls)),
)
```

# 托管 Python 应用

![](img/e016e192a91ffc1a9e474690a590742f_136_2.png)

## Heroku

### heroku.com

这个应用也许是其中最知名的云托管提供商之一。他们的堆栈服务器环境标准支持多种核心 Web 应用语言，包括 Python。其独特的 Toolbelt 命令行功能以及与 Git 仓库的集成，再加上极其快速且易于扩展和提升性能的特点，使其成为一个显而易见的选择。免费账户可以让你在一个 dyno 实例上运行 Python Web 应用而无需任何费用。

![](img/e016e192a91ffc1a9e474690a590742f_136_3.png)

## Python Anywhere

### pythonanywhere.com

另一个托管选项，并且是专门为 Python 应用创建的一般选项，是 Python Anywhere。免费的基本选项计划具有足够的权重和功率，可以让你无需扩展即可运行 Python Web 应用，但一旦你的项目获得关注，你就可以切换计划并提升计划性能。它标准地提供了极其令人印象深刻的模块范围，可立即导入到你的应用中以开始工作，包括如果你需要的话 Django 和 Flask。

## 使用 Flask、Jinja2 和 Twitter 创建动态模板

使用 Twitter 和 Flask 的渲染引擎 Jinja2 创建一个动态网页

### 资源

- Python 2.7+
- Flask 0.10.0: flask.pocco.org
- Flask GitHub: github.com/mitsuhiko/flask
- 一个 Twitter 账户
- 你最喜欢的文本编辑器
- 从 FileSilo 下载的代码

![](img/e016e192a91ffc1a9e474690a590742f_137_0.png)

该模板使用循环生成一个 Twitter 推文列表

当你希望处理 Twitter OAuth 过程并构建请求以获取令牌时，Python 和 Flask 是一个极好的组合。我们在这里使用 Twitter，是因为上面有大量易于消化的数据可用。然而，由于 Twitter 遵循 OAuth 1.0 设定的标准，我们用于签名和构建请求的代码可以稍加修改即可适用于使用相同标准的任何第三方 API，而无需大量工作。多年来，PHP 一直是模板生成的主力，但现在借助像 Flask、Sinatra 和 Handlebars 这样文档完善的框架，使用强大的脚本语言的能力极大地提高了我们制作优秀 Web 服务的能力。在这里，我们将使用 Python、Flask 及其模板引擎来显示推文。Flask 附带了超级便捷的 Jinja2 模板引擎。如果你熟悉 Node.js 或前端 JavaScript，其语法看起来会非常类似于 Handlebars 渲染引擎。

但是，在我们深入其中之前，我们需要整理一下我们使用的示例代码中的一些部分。

### 01 重新整理我们的代码

服务器代码很快就会变得杂乱且难以维护，因此我们要做的第一件事是将辅助函数移到另一个文件中，并将它们导入到我们的项目中，就像导入模块一样。这样，就很清楚哪些函数是我们的服务器逻辑和端点，哪些是通用的 Python 函数。打开从 FileSilo 下载的 TwitterAuthentication 文件（存储在 Twitter OAuth 文件下），定位 getParameters、sign_request 和 create_oauth_headers 函数。将它们剪切并粘贴到项目根目录中名为 helpers.py 的新文件中。在该文件的顶部，我们要导入一些库。

```python
import urllib, collections, hmac, binascii, time, random, string

from hashlib import sha1
```

现在我们可以回到 server.py 并将辅助函数重新导入到我们的项目中。我们通过简单地调用 `import helpers` 来实现这一点。由于 Python 很智能，它会先在当前目录中查找 helpers.py 文件，然后再查找系统模块。现在 helpers.py 中包含的所有函数都可以被我们的项目访问。我们要做的只是像以前一样调用它们：我们之前使用 `helper.function_name` 调用的方法将执行。对于 `sign_request`，我们将需要为每个请求传入我们的 `oauth_secret` 和 `consumer_secret`，而不是从会话中访问它。像这样调整函数声明：

```python
def sign_request(parameters, method, baseURL, consumer_secret, oauth_secret):
```

### 02 server.py 模块

随着该项目所需的大量模块被移动到 helpers.py 中，我们现在可以从 server.py 中移除其中大部分。如果我们修改第一个 import 语句为...

```python
import urllib2, time, random, json
```

...我们的项目将继续像以前一样工作。注意 json 模块的添加：我们将稍后在开始处理 Twitter 数据时使用它。让 Flask 使用渲染引擎非常简单。Flask 包装了 Jinja2 模板渲染引擎，所以我们不需要安装任何东西——我们只需要将包导入项目中。我们可以通过在 `from flask import [...]` 语句末尾添加 render_template 来实现这一点。

### 03 我们的第一个模板

既然我们有了渲染引擎，我们需要创建一些模板供其使用。在项目文件夹的根目录中，创建一个名为 templates 的新文件夹。每当我们尝试渲染一个模板时，Flask 都会在这个文件夹中查找指定的模板。为了掌握模板化，我们将重写部分身份验证逻辑，使用模板而不是手动请求端点。在 templates 中，创建一个 index.html 文件。你可以像处理其他文件一样处理这个 HTML 文件——本教程资源中包含一个 index.html，其中包含了该文件所需的所有 head 标签和 `<DOCTYPE>` 声明。

### 04 渲染我们的模板

在 server.py 中，让我们为 '/' 创建一个路由以处理授权过程。

```python
@app.route('/')
def home():
    if not 'oauth_token' in session:
        session.clear()
        session['oauth_secret'] = ''
        session['oauth_token'] = ''
    return render_template('index.html')
```

这是一个简单的函数：我们要做的就是检查是否已经有 oauth_token，并在 Flask 会话中创建这些属性，以便如果我们错误地尝试访问它时不会抛出错误。为了在响应请求时发送我们生成的模板，我们返回 `render_template('index.html')`。

### 05 模板变量

我们可以选择使用 `render_template('index.html', variableOne=value, variableTwo=value)` 向我们的模板发送变量，但在这种情况下我们不需要，因为每个模板都可以访问 request 和 session 变量。

```html
{% if session['oauth_token'] != "" %}
    <!-- 已授权 -->
    <div class="dialog">
        <!-- 你好，你已认证 --> 让我们 <a href='/get-tweets'>获取一些推文</a>
    </div>
{% else %}
    <!-- 需要授权 -->
    <div class="dialog">
        <!-- 我们需要 --> <a href='/authenticate'>认证</a>
    </div>
{% endif %}
```

采用 BSD 许可证的 Flask 易于设置和使用——查看网站以获取更多信息

![](img/e016e192a91ffc1a9e474690a590742f_138_0.png)

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello World!'

if __name__ == '__main__':
    app.run()
```

### 且易于设置

```bash
$ pip install Flask
$ python hello.py
* Running on http://localhost:5000/
```

### 感兴趣？

- 下载最新释放版 (0.10)
- 阅读文档或下载为 PDF 和打包的 HTML
- 加入邮件列表
- 在 github 上分支它
- 添加问题和功能请求


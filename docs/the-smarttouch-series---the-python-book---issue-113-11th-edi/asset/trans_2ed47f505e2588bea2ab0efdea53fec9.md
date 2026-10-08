
## 09 显示文章

创建你的第一个路由，以便我们能够返回并显示所有可用的文章。为了查询数据库，我们对存储的数据库连接执行一条 SQL 语句。然后，结果使用 Python 的 dict 方法映射为值，并保存为 posts 变量。

要渲染模板，我们调用 render_template() 并传入文件名以及要显示的变量作为第二个参数。

可以通过逗号分隔的列表传递多个变量。

```python
@app.get('/posts/')
def get_posts():
    cur = g.db.execute('select title, text from posts order by id desc')
    posts = [dict(title=row[0], text=row[1])
             for row in cur.fetchall()]
    return render_template('show_posts.html', posts=posts)
```

## 10 模板输出

Flask 期望模板位于项目根目录的 templates 目录中，因此请确保现在创建该目录。接下来，添加一个名为 'show_posts.html' 的新文件。动态值使用 Jinja2 模板语法进行管理，这是 Flask 应用的默认模板引擎。将此文件保存在 templates 目录中。

```html
<ul class="posts">
{% for post in posts %}
<li><h2>{{ post.title }}</h2>{{ post.text|safe }}
{% else %}
<li>抱歉，没有文章符合您的请求。
{% endfor %}
</ul>
```

## 11 创建 API 响应

为了创建 API 响应，我们可以定义一个带有特定 API 端点的新路由。再次，我们查询数据库中的所有文章。然后使用 JSONify 方法将数据作为 JSON 返回。如果你愿意，还可以添加特定值，如文章计数和自定义消息，以及格式化为 JSON 的实际 posts 变量。

```python
@app.route('/api/v1/posts/',
           methods=['GET'])
def show_entries():
    cur = g.db.execute('select title, text from posts order by id desc')
    posts = [dict(title=row[0], text=row[1])
             for row in cur.fetchall()]
    return jsonify({"count": len(posts), 'posts': posts})
```

```python
@app.route('/api/v1/posts/<int:post_id>',
           methods=['GET', 'DELETE'])
def single_post(post_id):
    method = request.method
    if method == 'GET':
        cur = g.db.execute('select title, text from posts where id=?', [post_id])
        posts = [dict(title=row[0], text=row[1]) for row in cur.fetchall()]
        return jsonify({"count": len(posts), 'posts': posts})
    elif method == 'DELETE':
        g.db.execute('delete from posts where id = ?', [post_id])
        return jsonify({"status": 'Post deleted'})
```

## 12 获取特定文章

要从 API 获取特定文章，我们需要创建一个新的路由，该路由将接受动态值作为 URL 的一部分。我们还可以选择将此路由用于多种请求方法，在这种情况下是 GET 和 DELETE。我们可以通过检查 request.method 值来确定方法，并在条件 if/else 语句中运行它。

## 13 运行应用程序

要运行你的 Flask 应用程序，请在活动的终端窗口中导航到项目根目录。确保你处于活动的虚拟环境 Python shell 中，输入运行主索引文件的命令。内置服务器将启动，并且网站可以在浏览器中的默认端口本地地址 http://127.0.0.1:5000 上访问。

```bash
python index.py
```

![](img/e016e192a91ffc1a9e474690a590742f_134_0.png)

## 14 API JSON 输出

应用程序的根目录将渲染我们之前创建的模板。可以生成多个路由以创建功能丰富的 Web 应用程序。在浏览器中访问 API 特定 URL 将返回格式整洁的 JSON 格式的请求数据。像版本化的 RESTful 端点那样定义自定义路由的能力是极其强大的。

## Python 的实际应用

对 Python 开发感兴趣？你将与目前正在使用它的大公司为伍

Disqus，这个流行的社交互动评论服务提供商，长期以来一直在其生产应用程序中使用 Python。Python 对开发团队的益处在于其能够有效扩展并满足大量消费者的需求，同时为内部和外部使用提供有效的底层 API。该公司现在开始使用 Go 运行一些生产应用程序，但大部分代码仍然运行在 Python 上。

世界知名的图片分享服务 Instagram 和社交图板 Pinterest 也将 Python 实施为其 Web 技术栈的一部分，选择 Django 来协助功能并满足向其服务发出的数千次内容查看和请求。

Mozilla、Atlassian 的 Bitbucket 仓库服务以及流行的讽刺网站 The Onion 均被记录为使用 Django 开发其产品。

![](img/e016e192a91ffc1a9e474690a590742f_134_1.png)

# Django 应用开发

Django 是一个功能强大的 Python Web 应用框架，拥有令人印象深刻的命令行工具

## 安装 Django

一旦安装了 Python，Django 的安装相对简单。通过我们在下面构建一个简单应用的过程，你可以自行验证

![](img/e016e192a91ffc1a9e474690a590742f_135_0.png)

**01** **创建虚拟环境**

为你的项目创建一个新的目录，并使用新的终端窗口导航到该目录内部。为此项目创建一个新的虚拟环境，选择使用最新的 Python 3。你的 Python 3 位置可能不同，因此请确保为二进制包设置正确的路径。

```bash
virtualenv -p /usr/local/bin/python3 venv
```

**02** **激活并安装**

使用终端窗口激活虚拟环境以开始项目特定的 shell。VirtualEnv 安装了 Python 包管理器 pip 的本地版本，因此运行命令安装 Django 相当简单。

```bash
venv/bin/activate
pip install Django
```

![](img/e016e192a91ffc1a9e474690a590742f_135_1.png)

**03** **创建核心项目**

Django 安装包含一些极其有用的命令行工具，它们将帮助你运行许多重复且困难的任务。让我们使用其中一个工具为我们创建一个全新的项目结构。运行 django-admin.py 脚本，并传入你想要创建的项目名称。

```bash
django-admin.py startproject myblog
```

![](img/e016e192a91ffc1a9e474690a590742f_135_2.png)

**04** **初始迁移**

通过终端窗口导航到项目目录。项目生成中包含的一些已安装应用程序需要数据库表。

使用助手工具，运行迁移命令以自动创建所有这些。终端窗口将让你了解你的所有进度以及迁移应用的内容。

```bash
cd myblog
python manage.py migrate
```

**05** **创建应用**

每个 Django 项目至少由一个应用程序或模块组成。运行 startapp 命令创建一个新博客应用模块，这将在主项目结构旁边生成所需的代码。

```bash
python manage.py startapp blog
```

## 数据库模型与迁移

Django 管理数据库模式和项目模型的迁移与维护的能力非常令人印象深刻

**01** **生成模型**

打开 blog/models.py 并创建第一个模型类，提供每个属性的名称和类型。你可以在此处的文档中深入了解字段类型：bit.ly/Yfn1Kn。

完成后，打开 myblog/settings.py 并将 blog 应用添加到允许安装的 application 列表中，以便项目能够加载它。

```python
class Post(models.Model):
    title = models.CharField(max_length=200)
    text = models.TextField()
```

```python
INSTALLED_APPS = (
    'django.contrib.admin',
    ..., 'django.contrib.staticfiles', 'blog'
)
```

![](img/e016e192a91ffc1a9e474690a590742f_135_3.png)

**02** **数据迁移**

任何模型的创建或数据的更改都需要进行迁移。为此，我们需要从模型数据创建迁移文件，这些文件将生成顺序编号的文件。

然后我们运行特定的迁移以生成所需的 SQL，最终的执行命令执行数据库迁移。

```bash
python manage.py makemigrations blog
python manage.py migrate blog 0001
python manage.py migrate
```


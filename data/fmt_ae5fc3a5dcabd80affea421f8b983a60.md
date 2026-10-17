
```python
from django.conf.urls import path
from django.urls import include
from django.contrib import admin

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('issuedis.urls')),
]
```

06 Django 包含一个内置 Web 服务器，对于测试和调试 Django 应用程序非常方便。让我们看看我们的管理界面……启动 Web 服务器：

```bash
$ python manage.py runserver
```

如果你的代码没有错误，服务器应该在 8000 端口可用。要启动管理界面，请访问 `http://localhost:8000/admin`。系统会要求登录。输入用户名和密码。

## 使用 Python 开发 Web 应用

### 介绍 Python

![](img/c72194f2c3aec198936695a665a5167c_28_0.png)

![](img/c72194f2c3aec198936695a665a5167c_28_1.png)

在建模应用的同时进行开发吗？它们没有出现在这里是因为它们不支持被暴露给用户。

`created_` 将自动设置为创建日期，`modified_` 将自动设置为该问题创建的日期。

```python
include(admin.site.urls)
```

这确保了所有的请求将首先由 ludussices 处理。

另外一点是，`owner`（所有者）字段会自动填充站点中的所有用户。

> 此时，管理界面已经可以工作了。我们需要一种方法使用管理界面来显示我们拥的数据。但目前还没有公共界面。让我们现在就创建它。

我们已经在模型中定义了列表来显示 ID、name、status、owner 和 'modified'。你可以通过访问 `http://localhost:8000/admin/ludussices/issue/` 来进入此视图。

在应用目录 (`ludussices/urls.py`) 中创建一个 py 文件，内容如下：

```python
# 我们将必须开始编辑主 urls.py (ludussitracker/urls.py)
urlpatterns = patterns(
    ('', include('ludussices.urls')),
    ('admin/', 
)
```

- `import patterns`, `include url`
- 使用列表模型
- 从 `models` 导入
- 包含所有内容的字典

![](img/c72194f2c3aec198936695a665a5167c_28_2.png)

```python
# ludicules 中的对象
info = {
  'queryset': ludicules.objects.all(),
}
```

### 我们在 Python 代码之外使用列表

### 我们正在使用列表-详情通用视图 (list-detail generic view)

```python
# listdetail 是我们正在使用的视图名称
urlpatterns = patterns(
    'django.views.generic.listdetail',
    # list-issue 和 issue-detail 是模板名称
    # 它们将链接到默认模板目录中
    {
      'object_name':'object',
      'list_name':'list_info',
      'url':'<id>/<object>',
      'detail_name':'item-detail',
    })
```

为了显示列表和详情，我们使用了 Django 的特色通用视图。在这种情况下，它们允许我们创建列表视图和详情视图。这些视图会在使用 `list.html` 和 `detail.html` 模板时应用。在接下来的步骤中，我们将创建模板文件。

09 在这一步中，我们将创建模板和媒体目录。已经提到模板目录为

`TEMPLATE_DIRS =`

```python
path('templates')
```

它对应 `ludussitracker/ludussitracker/templates/`。由于我们是解耦，我们将从应用页面访问模板，完整路径为 `ludussitracker/ludussitracker/templates/`。在你的项目文件夹中创建这些文件夹。此外，创建 `ludussitracker/ludussitracker/media/` 来处理 CSS 文件。你可以从代码文件夹的 resources 目录提供 css。为了从该目录提供文件，请使其可用。打开 `settings.py` 并在 `ludussitracker/ludussitracker/urls.py` 中添加这些行：

```python
# 在 Django 中，我们从 ludussitracker/ludussitracker/templates/base.html 开始。将其视为主模板，可以由从属所有者启用。
```

`ludussitracker/ludussitracker/templates/base.html`

```html
<!DOCTYPE HTML>
<html PUBLIC "-//http://www.w3.org/TR/HTML1/Strict//EN" "http://www.w3.org/TR/html11-strict.">">
<head>
<title>{% block title %}{% block %}LUD Issues{% endblock %}</title>
<link rel="stylesheet" href="{{ MEDIA_URL }}.style.class" type="text/css" media="screen"/>
</head>
<body>
<div id="head">
<h1>Issue Tracker/<span></span></h1>
</div>
</div><div id="mn">
<ul>
<li><a href="{% url list-issue %}" class="View Issues">a</a></li>
</ul>
</div>
<div id="bd">
{% block content %}{% endblock %}
</div>
</div>
</body>
</html>
```

```python
from django.contrib import admin
admin.autodiscover()
```

```python
urlpatterns = patterns(
    (r'^', include('ludussices.urls')),
    (r'admin/', include(admin.site.urls)),
    (r'media/', static/(?P<path>.*), django.views.static.serve,
        'document_root': settings.MEDIA_ROOT})
))
```

10 在这一步中，我们将创建

来自 `ludussitracker/ludussitracker/templates/` 的

为了显示列表和详情，我们使用了 Django 的特色通用视图。在这种情况下，它们允许我们创建列表视图和详情视图。这些视图会在使用 `list.html` 和 `detail.html` 模板时应用。在接下来的步骤中，我们将创建模板文件。

![](img/c72194f2c3aec198936695a665a5167c_30.png)

| Issue | Description | Status | Owner |
| :--- | :--- | :--- | :--- |
| 1 | 有一个问题。 | {{ status }} | {{ owner }} |
| 2 | 这是另一个问题。 | {{ status }} | {{ owner }} |
| 3 | 我们 own一些问题。 | {{ status }} | {{ owner }} |
| 4 | 这是一个测试。 | {{ status }} | {{ owner }} |
| 5 | 另一个问题。 | {{ status }} | {{ owner }} |

`{{ status }}` `{{ owner }}` `{{ status }}` `{{ owner }}`

我们现在使用 Django 的特色通用视图。在这种情况下，它们允许我们创建列表视图和详情视图。这些视图会在使用 `list.html` 和 `detail.html` 模板时应用。在接下来的步骤中，我们将创建模板文件。

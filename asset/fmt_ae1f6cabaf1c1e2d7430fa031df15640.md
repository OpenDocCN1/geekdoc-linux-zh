
```python
return render(request, 'index.html', {

    'sidebar_list': sidebar_list,

    'list': post_list,

    'month_timeline': month_timeline

})
```

## 16 管理

如果我们喜欢这些文章，可以开始编写 `admin.py` 来添加此功能：

```python
from .models import Post, Comment
from django.contrib.admin import admin

class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'pub_date']
    fields = ['title', 'pub_date', 'post']

admin.site.register(Post, PostAdmin)

class CommentAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'post']

admin.site.register(Comment, CommentAdmin)
```

## 22 完成你的侧边栏定义

编辑 `index` 命令以包含侧边栏信息：

```python
return render_to_response(request, 'index.html',
    'sidebar_list': sidebar_list,
    'list': post_list,
    'month_timeline': month_timeline
)
```

然后将此内容添加到你的 `index.html`，页面就可以渲染了：

```html
<a href="{% url 'month_timeline' year, month %}">{{ month }}</a>
```

现在显示侧边栏中的所有信息：

## 19 开始定义 month_timeline

我们需要从这里获取信息：

```python
def month_timeline(request):
    year, month = datetime.now()[:2]
    begin = Post.objects.filter(pub_date__year=year, pub_date__month=month)
    list = []
```

## 23 网页上的侧边栏

添加第一个实例。如果文章的某行发生变化：

```html
{% for month in sidebar_list %}
<ul>
    <li><a href="{% url 'month_timeline' month.year, month.month %}">{{ month.month }}</a></li>
</ul>
{% endfor %}
```

## 17 评论侧边管理功能

我们现在可以在后台的情况下添加评论功能：

```python
class CommentAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'post']

admin.site.register(Comment, CommentAdmin)
```

这将在管理站点上显示评论，你可以看到评论，它连接到：

## 20 完成你的定义

我们现在按月份对文章进行排序，从我们的第一个开始：

![](img/3c5b3591dd9ac4cceb489cee11bd7908_152_1.png)

```python
for y in range(year, year, -1):
```

## 24 侧边栏终结

显然现在还不对——那是 HTML 和 CSS 的工作。不过信息已经在那里，你可以以任何想要的方式处理它。然而，博客现在对读者友好得多。

```python
from calendar import calendar, month_name
我们将定义两个函数，
month_timeline，并制作侧边栏。
```

```python
(Wait, I noticed a typo in the source text logic, but following follow the structure)
for m in range(start, end, -1):
    sidebar_list.append((Y, m))
    month_name(m)
return month_list
```

![](img/3c5b3591dd9ac4cceb489cee11bd7908_152_2.png)

## Web 开发

## 资源

Python ：
http://www.python.org/download/
Django 源码：https://www.djangoproject.com/download/

## 使用额外功能增强你的博客

在之前的教程基础上，我们将介绍你可以利用 Django 强大功能的一些更高级的功能。

![](img/3c5b3591dd9ac4cceb489cee11bd7908_153_0.png)

我们一直在构建博客，以便创建和显示文章、允许人们发表评论，并像经典博客那样按月份筛选文章。要让它看起来和运行起来更像一个经典的博客，我们还有一段路要走。

模型引用以及它在后台站点中的工作原理。我们还将介绍如何更改数据库，以及 Django 在创建 SQL 查询时如何提供帮助。

最后，RSS 馈送是 Django 标准库的一部分，我们将学习如何使用它来显示最新的条目，并点击跳转到文章。在本教程结束时，你的 Django 博客就大功成了！

在本教程中，我们将添加摘要、摘录，最后是 RSS 馈送。这允许我们查看几点内容 - 首先，我们将更好地理解跨-

![](img/3c5b3591dd9ac4cceb489cee11bd7908_153_1.png)

## 手动摘录

如果你不想自动摘要，我们可以在文章模型中添加一个编辑字段，这样你可以手动创建一个。

```
excerpt = models.TextField()
```

为了限制摘录中的字符数，我们像处理作者部分一样使用 `CharField`。

## 01 摘要

在普通博客中，我们将会有较长的文章。我们可以像这样在索引页面模板上为每篇文章生成一个摘要：

```
{{ post.content|truncatewords:30 }}
```

这会自动获取文章的前三个单词 - 当然，你可以使用任何数量的单词。

![](img/3c5b3591dd9ac4cceb489cee11bd7908_153_2.png)

## 03 写摘录

为了编写摘录或将其附加到之前的文章，我们必须将其添加到后台页面。打开任何后台页面并编辑 `post` 类的字段部分，添加 `excerpt`：

```
fields = ['title', 'post_date', 'author', 'post', 'excerpt']
```

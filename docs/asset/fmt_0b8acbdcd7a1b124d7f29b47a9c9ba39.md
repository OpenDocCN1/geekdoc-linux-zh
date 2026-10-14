
```python
comment = form.save(commit=False)

comment.post = post

comment.save()

return redirect(reverse('blog.post_detail', args=[post_id]))
```

需要 `CSRF` 令牌来防止跨站请求伪造。

![](img/287427b4a3b7d7792fc1ca7834fce232_147_1.png)
![](img/287427b4a3b7d7792fc1ca7834fce232_147_2.png)
![](img/287427b4a3b7d7792fc1ca7834fce232_147_3.png)
![](img/287427b4a3b7d7792fc1ca7834fce232_147_4.png)
![](img/287427b4a3b7d7792fc1ca7834fce232_147_5.png)
![](img/287427b4a3b7d7792fc1ca7834fce232_147_6.png)
![](img/287427b4a3b7d7792fc1ca7834fce232_147_7.png)

## 14 评论模板

通过向 `post.html` 添加以下内容为文章页面准备评论：

```html

<Comments>

    {% for comment in comments %}

        <div>{{ comment.text }}</div>

    {% endfor %}

</Comments>

<form method="POST" action="/">

    {% csrf_token %}

    <input type="hidden" name="post_id" value="{{ post.id }}">

    {{ form.author }}

    {{ form.text }}

    <input type="submit" value="提交">

</form>

```

## 15 定义你的评论

第一步是在 `blog/urls.py` 中定义评论，这很简单：

```python

def add_comment(request, post_id):

    post = Post.objects.get_or_404(id=post_id)

    if request.method == 'POST':

        form = CommentForm(request.POST)

        if form.is_valid():

            comment = form.save(commit=False)

            comment.post = post

            comment.save()

            return redirect(reverse('blog.post_detail', args=[post_id]))

    else:

        form = CommentForm()

    return render(request, 'blog/comment.html', {'form': form, 'post': post})

```

## 16 开始定义

Django 让按年份和月份美化文章变得简单，但我们首先需要在 `blog/py` 中定义新模型：

## 17 评论端管理

我们可以在引起任何更改的情况下添加评论管理功能：

## 18 侧边栏开始

Django 让按年份和月份美化文章变得简单，但我们首先需要在 `blog/py` 中定义新模型：

## 19 开始定义

我们需要添加：

## 20 完成你的定义

现在我们将按月份并从我们的第一个月份开始定义文章。

## 21 网页上的侧边栏

现在我们将显示侧边栏

## 22 完成你的评论

然后我们将此行代码添加到：

## 23 侧边栏结束

显然，它现在的工作是 HTML 和 CSS。信息已经在那里了，你可以通过某种方式对其进行操纵。然而，侧边栏现在是你的读者的朋友了。

## Web 开发

资源
- Python 基础：http://www.python.org/download/
- Django 源码：https://www.djangoproject.com/download/

# 使用额外功能增强你的博客

在之前的教程基础上，我们将涵盖你可以利用 Django 的一些高级功能。

我们一直在构建 Django 博客，以创建和显示文章、允许人们评论，并像经典博客一样按月份筛选文章。要使其看起来和运行起来更像经典博客，我们还有一段路要走。

模型引用以及它在后台站点的工作原理。我们还将介绍如何更改数据库，以及 Django 如何在创建 SQL 查询时提供帮助。

在本教程中，我们将添加摘要、节录，最后是 RSS 馈送。这允许我们查看几个内容——首先，我们将更好地理解跨-

最后，RSS 馈送是 Django 标准库的一部分。我们将学习如何使用它来显示可以点击文章的最新条。你的 Django 博客就大功告成了！

![](img/287427b4a3b7d7792fc1ca7834fce232_149_0.png)

## 02 手动节录

如果你不想自动摘要，我们可以在文章模型中添加节录（excerpt），这样你就可以手动创建一个，

```python

excerpt = models.TextField()

```
要限制节录中的字符数，请像我们的作者部分一样使用 `CharField`。

![](img/287427b4a3b7d7792fc1ca7834fce232_149_1.png)

## 01 摘要

在博客中，我们将会有很长的文章。我们可以在索引页面模板上为每篇文章生成摘要，如下所示：

```python

{{ post.post|truncatewords:3 }}

```
这会自动获取文章的前三个单词——当然当然，你可以使用任何数字。

![](img/287427b4a3b7d7792fc1ca7834fce232_149_2.png)

## 03 编写节录

为了编写节录或将其附加到之前的文章中，我们必须将其添加到后台页面。打开 `admin.py` 并编辑 `Post` 模型的字段，添加 `excerpt`：

```python

fields = ['title', 'pub_date', 'author', 'post', 'excerpt']
```

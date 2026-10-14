
- Django: https://www.django.com/project

对数据库进行读写。这些都是简单的操作，但当然，这是为了从零开始用 Django 开发网站。在这里我们将对网站的前端进行改造，使其超出你对现代博客的预期。它将包含侧边栏、页面以及添加和修改内容的能力。在此过程中，我们将更多地了解使用 Django 开发网站的优势。

在上一个教程中，我们开始构建最基础的博客，并学习了如何在项目中使用一点 Django。现在我们可以设置一个新项目，创建数据库并编写基础代码了。

你应该像之前一样，在本次教程中继续使用 Django 4。

## Web 开发

![](img/516df994db593237169e2aff6d3e6840_146_0.png)

```python
from django.shortcuts import render, get_object_or_404

def list(request):
    posts = Post.objects.all().order_by('-pub_date')
    return render(request, 'blog/list.html', {'posts': posts})
```

Django 太棒了！

| 文章标题 | 日期 | 评论 |
|---|---|---|
| 文章 | 2023年3月24日 | 0 |

### 06 链接到页面

让我们让主页上的链接工作。打开 `index.html` 文件并进行以下更改：

```html
<h2><a href="{% url 'post:' post.id %}">{{ post.title }}</a></h2>
```

这是一个使用绝对链接的非常简单的方法，不需要对视图或模型进行更改。

![](img/516df994db593237169e2aff6d3e6840_146_1.png)

### 01 新博客

我们之前的博客是按时间顺序显示文章，这对于读者没有帮助。为了纠正这一点，打开博客文件夹并编辑以下内容：

```python
post_list = Post.objects.all().order_by('-pub_date')
```

这确保了文章按倒序（最新优先）显示。

### 02 查看文章页面

你可能希望能够链接到单个文章页面，为了做到，我们必须在 `urls.py` 文件中定义它：

### 07 分页

我们需要将文章划分到不同的页面，因此我们需要对 `urls.py` 进行以下添加内容：

![](img/516df994db593237169e2aff6d3e6840_146_2.png)

```python
post_list = Post.objects.all().order_by('-pub_date')
paginator = Paginator(post_list, 5)
page_obj = paginator.get_page(request.GET.get('page', 1))
```

### 04 编辑 URLs

在我们的 `urls.py` 中，我们需要对文章详情页和分页添加一些修改，进行以下更改：

```python
url('blog/', views.post_list),
url('post/<int:id>/', views.post_detail, name='post'),
url('blog/<int:page>/', views.post_list, name='page'),
```

### 08 请翻页

我们现在需要添加编辑的索引模板链接，打开以下：

![](img/516df994db593237169e2aff6d3e6840_146_3.png)

### 03 清理你的代码

你可能需要使用函数来定义索引 - 这是一个让编写代码变得简单的快捷方法。尝试让它运行：

```html
{% if post_list.has_next %}
    <a href="{% url 'page' page_obj.page_number + 1 %}">Next</a>
{% endif %}
{% if post_list.has_previous %}
    <a href="{% url 'page' page_obj.page_number - 1 %}">Previous</a>
{% endif %}
```

### 05 文章模板

我们将使用文章来指向一个我们需要创建的模板。在下一步中，创建带有以下代码的 `post_detail.html`，以组装首页：

```html
<h2><a href="{% url 'post:' post.id %}">{{ post.title }}</a></h2>
<p>{{ post.content }}</p>
```

```python
from django.shortcuts import render_to_template
```

我们建议你编辑索引代码以匹配 `post_page`。

## Web 开发

### 09 错误页面

`from django.core.paginator import Paginator, EmptyPage, InvalidPage`

```python
try:
    post_list = paginator.list(page)
except (EmptyPage, InvalidPage):
    post_list = page
```

最后一部分替换了 `post_list = page_number`

### 12 表单评论

我们需要能够处理 `forms` 中的数据和元数据，所以在 `blog` 文件夹中添加以下类：

```python
from django.forms import ModelForm
class Comment(ModelForm):
    class Meta:
        model = Comment
        exclude = ['post']
```

### 14 评论模板

通过向 `post.html` 添加此内容准备评论：

```html
{% for comment in comments %}
<p>{{ comment.author }}: {{ comment.text }}</p>
{% endfor %}
<br>
<strong>Add comment
<form action="{% url 'blog.add_comment' post.id %}" method="POST">
    Name: <input name="author">
    <textarea name="text"></textarea>
    <input type="submit" value="Submit">
</form>
```

### 10 每个人都可以评论你的博客文章。我们从编辑 models.py 开始：

```python
class Comment(models.Model):
    text = models.TextField()
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    def __str__(self):
        return self.text
```

我们可以让他们提交评论。

### 13 在文章页

我们需要列出在文章页上的评论，所以我们更新 `post_detail` 视图：

```python
from django.shortcuts import render, get_object_or_404
def post_detail(request, pk):
    post = get_object_or_404(Post, pk)
    comments = Comment.objects.filter(post=post)
    return render(request, 'blog/post_detail.html', {'post': post, 'comments': comments})
```

### 11 回到评论

我们需要在 `urls.py` 中添加评论链接，以便他们将评论发布回原始页面：

```python
path('blog/add_comment/<int:post_id>/', views.add_comment, name='blog_comment'),
```

此 URL 模式携带关联的文章 ID。

### 15 定义评论

最后一步是在 `views.py` 中定义评论并添加评论表单：

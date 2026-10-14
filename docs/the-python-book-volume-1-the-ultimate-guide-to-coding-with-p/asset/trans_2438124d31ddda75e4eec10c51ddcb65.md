

## 01 新的博客排序

上次我们停留在博客按时间顺序显示文章，这对读者来说帮助不大。为了纠正这个问题，打开 blog 文件夹中的 urls.py 并编辑以下行：

```
post_list = Post.objects.all().order_by("~-pub_date")
```

这确保文章按倒序显示（最新在前）。

## 02 一个页面的视图

你当然希望能够链接到特定页面，为此我们首先需要在 blog 文件夹的 urls.py 文件中定义这些页面包含的内容：

```
def post_page(request, post_id):
    post_page = Post.objects.
    get(pk=post_id)
    return render_to_response('blog/post.html', {'post_page': post_page})
```

## 03 清理你的代码

你可能会注意到我们对 index 定义使用了不同的 return 命令——这是一个快捷方式，让编写代码变得更容易。要使其工作，添加：

```
from django.shortcuts import render_to_response
```

我们建议你编辑 index 代码以匹配 post_page。

## 04 编辑 URL

在 myblog 中的 urls.py 我们需要做一些增添和修改，以便网站能正确指向文章：

```
url(r'^myblog/$', 'blog.urls.index'),
url(r'^myblog/(?P<post_id>\d+)/$', 'blog.urls.post_page'),
```

post_id 是文章的编号，由系统自动生成。$ 很重要，能使重定向正常工作。

## 05 文章模板

我们让 post_page 指向一个模板，现在需要创建它。在与 index.html 相同的位置，创建 post.html 并使用以下格式使其与首页相似：

```
<h2>{{ post_page.title }}</h2>
{{ post_page.author }} on {{ post_page.pub_date }}
<p>{{ post_page.post }}</p>
```

## 06 链接到页面

让我们从主页面让这些链接生效。打开 index.html 文件并做出以下更改：

```
<h2><a href="/myblog/{{ post.pk }}">{{ post.title }}</a></h2>
```

这是一个非常简单的增添，使用绝对链接，且无需对 views 或 model 进行调整。

## 07 分页

为了让博客文章分布在多个页面上，我们需要在 blog 文件夹的 urls.py 中做一些增添：

```
post_list = Post.objects.all().order_by("~-pub_date")
paginator = Paginator(post_list, 3)
try: list_page = request.GET.get("list_page", '1')
except ValueError: list_page = 1
post_list = paginator.page(list_page)
return render_to_response('blog/index.html', {'post_list': post_list})
```

## 08 请翻页

现在我们需要为博客添加导航链接，因此打开 index 模板进行编辑：

```
{% if post_list.has_previous %}
<a href="?list_page={{ post_list.previous_page_number }}">Newer</a>
{% endif %}
{% if post_list.has_next %}
<a href="?list_page={{ post_list.next_page_number }}">Older</a>
{% endif %}
```

## Web development

## 09 错误的页面

让我们添加一段小代码，如果用户输入错误的 URL 就将其返回到上一页：

```
from django.core.paginator import Paginator, EmptyPage, InvalidPage

try:
    post_list = paginator.page(list_page)
except (EmptyPage, InvalidPage):
    post_list = paginator.
page(paginator.num_pages)
The last part replaces 'post_list = paginator.page(list_page)'.
```

![](img/3b256f430f51c98f1315671f6e4eec19_145_0.png)

## 10 发表你的看法

每个人在互联网上都有自己的观点。你可以让读者发表评论，我们先从编辑 models.py 开始：

```
class Comment(models.Model):
    author = models.CharField(max_length=50)
    text = models.TextField()
    post = models.ForeignKey(Post)
    def __unicode__(self):
        return self.post, self.text
We've made it so they can put their name with a comment.
```

![](img/3b256f430f51c98f1315671f6e4eec19_145_1.png)

## 11 回到评论

我们现在需要在 myblog 中的 urls.py 文件里添加一行小代码，以便评论可以发布然后返回到原始页面：

```
url(r'^myblog/add_comment/(\d+)$/', 'blog.urls.add_comment'),
This URL pattern calls the ID of the page that you're on.
```

## We need to be able to process the data and metadata in the forms

## 12 形成评论

我们需要能够处理表单中的数据和元数据，所以让我们在 blog 文件夹的 urls.py 中添加一个类，内容如下：

```
from django.forms import ModelForm
from blog.models import Post, Comment
class CommentForm(ModelForm):
    class Meta:
        model = Comment
        exclude = ['post']
```

![](img/3b256f430f51c98f1315671f6e4eec19_145_2.png)

## 13 在文章中

我们需要将评论归属于它们所发表的文章，因此更新 post_page 定义：

```
from django.core.context_processors import csrf
import csrf
def post_page(request, post_id):
    post_page = Post.objects.get(pk=post_id)
    comments = Comment.objects.filter(post=post_page)
    d = dict(post_page=post_page, comments=comments, form=CommentForm())
    d.update(csrf(request))
    return render_to_response('blog/post.html', d)
The CSRF tag is to prevent cross-site request forgery.
```

![](img/3b256f430f51c98f1315671f6e4eec19_145_3.png)

## 14 评论模板

让我们通过在 post.html 中添加以下内容来为文章页面准备评论功能：

```
<p>Comments:</p>
{% for comment in comments %}
    {{ comment.author }}
    <p>{{ comment.text }}</p>
{% endfor %}
<strong>Add comment</strong>
<form action="{% url blog.urls.add_comment comment_id %}" method="POST"{% csrf_token %}">
Name {{ form.author }}
<p>{{ form.text }}</p>
<input type="submit" value="Submit">
</form>
```

## 15 定义你的评论

最后一步是在 blog.urls.py 中定义评论，这一步比较大：

```
def add_comment(request, comment_id):
    p = request.POST
    if p.has_key('text') and p['text']:
        author = 'Anonymous'
        if p['author']: author = p['author']
    p['author']
    comment = Comment(post=Post.objects.get(pk=comment_id))
    cf = CommentForm(p, instance=comment)
    cf.fields['author'].required = False
    comment = False
    cf.save(commit=False)
    comment.author = author
    comment.save()
    return HttpResponseRedirect(reverse('blog.urls.post_page', args=[comment_id]))
This ensures text has been entered, and if not specified author is 'Anonymous'. Before testing, run syncdb so comment tables can be created.


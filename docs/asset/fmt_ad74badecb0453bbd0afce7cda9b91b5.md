
> 我们将添加摘要、节录和 RSS 馈送

# 《Python Book》

- 为你的博客添加自动摘要或手动编写的节录
- 将文章分类作为博客的独立功能进行创建和管理
- 学习修改数据库以创建带有分类的文章，并将其添加到其他文章中
- 使用 Django 内置函数创建 RSS 馈送

## 04 用于摘要的节录

你可以替换索引模板中的文章内容，但我们可以将其保留为节录块。

## 05 数据库错误

如果你决定测试这些更改，

![](img/287427b4a3b7d7792fc1ca7834fce232_150_0.png)

> 你注意到我们的服务器停止工作了。这是因为数据库中没有 `excerpt` 列。因此，我们需要在 `orders` 中添加一个 `excerpt` 列。要找到如何操作，运行：`$ python manage.py sqlmanage`

## 06 数据库查询

输出将向你显示添加到模型中的 SQL 代码。我们需要专门修改该字段，即：`'excerpt' NOT NULL`；请记住它。

![](img/287427b4a3b7d7792fc1ca7834fce232_150_1.png)

## ALTER "blog_post"

然后像这样输入我们记录的代码：`ADD "excerpt" text;`

## 08 保存更改

我们删除了 `NULL`，因为我们已经有有了没有节录的条目，而且如果可以的话，我们想让它自动摘要。使用 `COMMIT;` 保存更改，然后退出 shell：`quit`

![](img/287427b4a3b7d7792fc1ca7834fce232_150_2.png)

## 09 测试一下

现在我们可以测试节录代码——创建一个新文章或编辑现有文章以带有节录。如果你按照我们的步骤正确操作，它应该可以正常工作；如果没有，你可能需要进行一些修复。

## 07 修改表

要进入数据库 shell 并修改字段，运行 `$ python manage.py dbshell`。然后我们需要使用 `ALTER QUERY`：

## Web 开发

评论，我们想在 `Post` 模型中添加一个 `ForeignKey`，以便将文章归类到分类。添加此行：`category = models.ForeignKey(Categories)`
并将 `categories` 移动到 `models` 的顶部。

> 我们现在可以单独创建分类了

![](img/287427b4a3b7d7792fc1ca7834fce232_151_0.png)

![](img/287427b4a3b7d7792fc1ca7834fce232_151_1.png)

## 10 Categories 模型

我们为博客分类添加了一个模型：

```python
class Categories(models.Model):
    name = models.CharField(unique=True, max_length=100)
    slug = models.SlugField(unique=True)
    parent = models.ForeignKey('self', blank=True, null=True, related_name='children')
    def __str__(self):
        return self.name
```
这允许父子分类。

![](img/287427b4a3b7d7792fc1ca7834fce232_151_2.png)

## 13 数据库分类

在此之前，我们找到修改表所需的 SQL。使用 `python` 执行此博客将返回与之前不同的代码：`"category_id" INTEGER NOT NULL "blog_categories"` 是我们获取的 ID，而不是文本，来自上面的表。

![](img/287427b4a3b7d7792fc1ca7834fce232_151_3.png)

## 16 分类显示

当我们的博客目录下的 `urls.py` 获取所有文章时，我们在索引模板中添加：

```python
path('category/<int:category_id>/', views.category_list, name='category_list'),
```

![](img/287427b4a3b7d7792fc1ca7834fce232_151_4.png)

## 14 修改表

再次修改数据库：使用 `python db shell` 将执行 `ALTER TABLE "blog_categories" ADD COLUMN "category_id" INTEGER NOT NULL`。最后执行 `COMMIT`：

## 17 分类页面

首先我们需要在 `blog/urls.py` 中定义分类。导入 `categories` 然后添加：

```python
path('category/<int:category_id>/', views.category_detail, name='category_detail')
```
显示相应的文章。

![](img/287427b4a3b7d7792fc1ca7834fce232_151_5.png)

## 11 管理分类

通过在 `admin.py` 中创建一个 section 来添加项：

```python
class CategoriesAdmin(admin.ModelAdmin):
    list_display = ('name', 'slug', 'parent')
admin.site.register(Categories, CategoriesAdmin)
```
在创建分类之前，我们需要迁移数据库：

```bash
python manage.py migrate
```

![](img/287427b4a3b7d7792fc1ca7834fce232_151_6.png)

## 15 管理分类 - 部分 2

现在我们可以回到 `PostAdmin` 添加新的分类字段：`list_display = ['title', 'author', 'pub_date', 'category'] = ['pub_date', 'author', 'excerpt']`。我们之前的博客文章没有显示。为了修复这个问题，我们需要修改 `Post` 模型：`category = models.ForeignKey(Categories, blank=True, null=True)`这样我们现在可以单独创建分类，并分配给没有分类的文章。

## 12 文章

与我们对分类显示的方式类似：`<a href="/blog/category/{{post.category.slug}}">{{post.category.name}}</a></p>` 这可以放在分类、文章和索引模板中。

```javascript
// comment.save()
return HttpResponse(object_to_redirect('/blog/post-page/', args={'id': comment.id}))
post = Post.objects.get(id=args['id'])
comment.post = post
comment.user = request.user
comment.date = datetime.now()
comment.save()
for y in range(post.date.year, 2000, -1):
    posts = Post.objects.filter(year=y)
    if posts.exists():
        break
```

![](img/287427b4a3b7d7792fc1ca7834fce232_152_1.png)

## 22 RSS

Django 有一个内置的 RSS 框架。要使用它，在 `settings.py` 的 `INSTALLED_APPS` 中添加 `django.contrib.syfeed`，然后从 `django.contrib.sy.feed` 导入 `RSSFeed` 并定义一个类：

```python
class BlogFeed(RSSFeed):
    title = "My Blog Link"
    def get_items(self):
        return Post.objects.all().order_by('-date')[:5]
    def get_object_url(self, obj):
        return obj.get_absolute_url()
```

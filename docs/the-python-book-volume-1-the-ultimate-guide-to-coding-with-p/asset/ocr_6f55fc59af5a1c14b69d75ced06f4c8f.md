# Web development

# 16 Administrate

Like the posts, we can get the Admin page to see comments. Start editing blogs/admin.py to get this feature added:

```
from blog.models import Post, Comment
from django.contrib import admin
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'pub_date']
    fields = ['title', 'pub_date', 'author', 'post']
admin.site.register(Post, PostAdmin)
```

# 17 Comment-specific admin features

Now we can add the comment-specific admin features without causing any clashes:

```
class CommentAdmin(admin.ModelAdmin):
    list_display = ['text', 'author', 'post']
admin.site.register(Comment, CommentAdmin)
```

This will show the comments on the admin site, and you can see the comment, the author and the post it's connected to.

# 18 Sidebar beginnings

Django makes it pretty easy to order posts by years and months, but first we need to import some new models into blog/urls.py:

```
import time
from calendar import month_name
```

We're going to define two new functions, month_timeline and month, to make the sidebar.

# 19 Start to define month_timeline

First we need to get all the information from the posts:

```
def month_timeline():
    year, month = time.localtime()[0:2]
    begin = Post.objects.order_by('pub_date')[0]
    month_begin = begin.pub_date.month
    year_begin = begin.pub_date.year
    month_list = []
```

The '[2]' makes sure we only get the time information we need.

# 20 Finish your definition

Now we will order the posts by month and year starting from our first month.

```
for y in range(year, year_begin-1, -1):
    start, end = 12, 0
    if y == year: start = month
    if y == year_begin: end = month_begin-1
    for m in range(start, end, -1):
        month_list.append((y, m, month_name[m]))
return month_list
```

# 21 Return to reader

With the list organised, we can now define month so we can display it on the blog:

```
def month(request, year, month):
    post_list = Post.objects.filter(pub_date__year=year, pub_date__month=month)
    return render_to_response('blog/index.html', dict(sidebar_list=object_list, month_list=month_timeline()))
```

Now we need to link it up to the index template.

# 22 Finalise your sidebar definition

Edit the return command on the index function to include the sidebar information:

```
return render_to_response('blog/index.html', dict(post_list=post_list, sidebar_list=post_list.object_list, month_list=month_timeline()))
```

Then add this line to urls.py in myblog so a month page can be rendered:

```
url(r'^myblog/month/(\d+)/(\d+)$', 'blog.urls.month')
```

All we need to do now is display the information on the site.

# 23 Sidebar on the web

Go to the index template. First of all, change the first line of the post forloop to:

```
{% for post in sidebar_list %}
```

Simple enough. Now we need to add the sidebar information:

```
{% for month_list %}
<p><a href="{% url blog.urls.month month.0 month.1 %}">{{ month.2 }}</a></p>
{% endfor %}
```

# 24 Sidebar finale

Obviously it's not at the side right now – that's a job for the HTML and CSS. The info is there, though, and you can manipulate it any way you want. However, your blog is now a lot more friendly to your readers.

![](bbox=[0.11, 0.22, 0.6, 0.42])

![](bbox=[0.32, 0.42, 0.58, 0.55])

![](bbox=[0.11, 0.62, 0.28, 0.7])

![](bbox=[0.32, 0.68, 0.58, 0.78])

![](bbox=[0.62, 0.62, 0.78, 0.78])
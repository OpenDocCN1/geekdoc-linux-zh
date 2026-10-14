

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_83_0.png)

Zinnia 应用本身就相当令人印象深刻。

我们还需要告诉 uWSGI Nginx 的配置方式，因此需要将它捆绑的参数复制到你的项目目录中：

```
(env) $ cp /etc/nginx/uwsgi_params ~/django/my_demo
```

要为你的演示站点配置 Nginx，现在需要创建一个文件 /etc/nginx/sites-available/mysite_nginx.conf，其内容如下，并在适当的地方将 'user' 替换为你的用户名：

```
upstream django {
  server 127.0.0.1:8001;
}
# configuration of the server
server {
  listen 8000;
  server_name 127.0.0.1; # substitute your machine's IP address or FQDN
  charset utf-8;
  client_max_body_size 75M;
  location /media {
    alias /home/user/django/my_demo/media;
  }
  location /static {
    alias /home/user/django/my_demo/static;
  }
  location / {
    uwsgi_pass django;
    include uwsgi_params;
  }
}
```

将此文件链接到 /etc/nginx/sites-enabled，确保该文件夹包含在你的 nginx.conf 中，然后启动 Nginx。完成之后，在目录 ~/django 中运行以下命令启动 uWSGI：

```
(env) $ uwsgi --socket 8001 --module mysite.wagi
```

希望你会发现所有组件都能相互通信，并且你的 Django 站点现在可以通过 http://localhost:8000 访问——这次它是由一个成熟的 Web 服务器提供服务，该服务器通过运行在 8001 端口的网关访问它，而网关则直接与 Python 应用通信。使用 Unix socket 而不是 TCP 作为网关是更好的做法，因为它开销更小、速度更快，因此将 /etc/nginx/sites_available/mysite_nginx.conf 中 upstream{} 块中的 server 行替换为：

```
server unix:///home/user/django/mysite.sock;
```

使用以下命令启动 uWSGI：

```
(env) $ uwsgi --socket mysite.sock --module mysite.wagi --chmod-socket=666
```

一切应该如前一样出现，但这次你应该能感受到那种因运行更高效而产生的温暖愉悦感。由于 Nginx 默认不允许与用户 socket 通信，因此有必要强制使用这种较为宽松的权限。在更正式的设置中，uWSGI 将在系统范围内运行，并由一个适当受限的系统账户运行，可能与 Nginx 守护进程的所有者属于同一组。

好了，孩子们，今天的课程就到此结束。我祝愿你在构建干净、模块化且可扩展的网站的冒险中一切顺利。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_83_1.png)

哦，主啊，你不会买给我……本网站使用 Django CMS 构建。

## 使用 Django 和 Zinnia 创建博客

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_84_0.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_84_1.png)

### 1 启动 Zinnia

重启 Web 服务器后，你应该会在顶部栏看到 Zinnia 菜单。在这里点击 New entry 会笨拙地在左侧面板中放置一个富文本输入表单。在此你可以创建你的第一篇 Zinnia 博客文章，如果你愿意的话。我们可以做得更好，特别是我们可以将博客应用集成到我们选择的布局中。

### 2 创建一个页面

让我们为博客创建一个新页面，选择 Page > Add Page > New Page。将其命名为 'blog'，或更具创意的名字。Slug 是页面在 URL 中引用的方式，并会根据标题自动完成。这意味着你的博客可以被网络蜘蛛和机器人轻松高效地索引。点击保存以创建页面。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_84_2.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_84_3.png)

### 3 创建布局

选择顶部的结构视图，然后点击内容栏右侧的菜单。添加一个包含两列的多列环境。最初两列大小相同，这是不理想的。但点击保存后展开多列环境并按需配置列。我选择左侧 50%，右侧 25%。

### 4 定义条目列表

接下来前往右侧列，从右侧菜单添加一个 Latest Entries 插件。编辑插件设置，使其仅显示最新条目，并使用 entry-detailed 模板。在此之下，你需要再添加一个 latest entries 元素，偏移量为 1，并使用默认的 entry-list 样式。这将仅显示你之前所有条目的标题。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_84_4.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_84_5.png)

### 5 添加额外功能

与此同时，在右侧列中添加一个 Tag Cloud、Calendar Entries 和管理控件。这足以让我们获得一个干净但功能齐全的 Zinnia 应用视图，并且完全集成在 Django CMS 中。管理工具将使你能够登录、发布新条目、审核评论以及执行任何你认为合适的其他博客相关操作。

### 6 开始写博客

它很好地展示了内容，在本例中是 ITER Tokamak 融合反应堆的乐高模型。随着你开发网站，你将能够按心意自定义并添加新的小部件和功能。当然，真正的乐趣始于你开始编写自己的模板，但即便不写一行代码也能取得如此多的成果，仍然令人印象深刻。



如图所示，`SCHEMA_MIGRATION` 表仅包含一列，即 `VERSION` 列，用于跟踪迁移版本号。版本号是迁移文件名上的数字前缀。例如，对于文件 `20100611202808_create_books.rb`，版本号为 `20100611202808`。

最简形式的 `rake db:migrate` 将运行所有尚未运行的迁移的 `up` 方法。如果你想要特定的版本，Active Record 将运行所需的迁移（`up` 或 `down`），直到达到指定版本为止。例如，要迁移到版本 `20100705000000`，请运行：

```
rake db:migrate VERSION=20100705000000
```

如果该版本大于当前版本，即正在向上迁移；则在所有迁移上调用 `up` 方法，包括 `20100705000000` 在内；如果正在向下迁移，则在所有迁移上调用 `down` 方法，直至但不包括 `20100705000000`。要回滚到上一个迁移，请使用：

```
rake db:rollback
```

现在让我们看看为此应用程序构建的内容。如果 `WEBrick` Web 服务器未启动，请使用此命令启动它：

```
<app_home>\bookapp> ruby script/server
```

然后在浏览器中输入 `http://localhost:3000/books`。*图 7.23* 显示了输出结果。

![](img/5f6ba170efa3a607142589708531bef8_270_0.png)

**图 7.23 – 书籍列表页面**

点击*新书*链接，并如*图 7.24*所示创建新书条目。

![](img/5f6ba170efa3a607142589708531bef8_270_1.png)

**图 7.24 – 创建新的书籍项目**

请注意，通过 RoR 应用程序，XML 文档已正确存储在 `BOOKS` 表中，如使用 IBM Data Studio 的*图 7.25*所示。

![](img/5f6ba170efa3a607142589708531bef8_271_0.png)

**图 7.25 – 从 IBM Data Studio 查看 XML 文档**

如果你将浏览器指回 `http://localhost:3000/books`，你将能够看到刚才创建的书籍。这在图 7.26 中有说明。你还能看到 RoR 自动创建的其他操作，例如 Show、Edit 和 Destroy。

![](img/5f6ba170efa3a607142589708531bef8_271_1.png)

**图 7.26 – 书籍列表**

既然我们可以使用 `book` 资源添加、删除和更新书籍，我们需要处理另一个允许列出所有书籍的资源。让我们使用此命令为此目的创建 `catalog` 资源：

```
<app_home>\bookapp>ruby script/generate controller catalog index
```

在上述命令中，控制器的名称是 *catalog*，并且还创建了一个名为 *index* 的默认视图页面。*图 7.27* 显示了此命令的输出。

![](img/5f6ba170efa3a607142589708531bef8_272_0.png)

> **注意：**
>
> 一旦 *catalog* 资源被创建，你必须重启 Web 服务器，否则你可能会遇到与路由器相关的错误。

以下操作将为 *catalog* 控制器构建列出所有书籍的基本逻辑。复制并粘贴*清单 7.1*中显示的代码到文件 `<app_home>\bookapp\app\models\book.rb`

```
class Book < ActiveRecord::Base
  def self.find_books
    xquery=
    "select i.TITLE, i.ID, t.AUTHOR, t.INFO, i.STATUS from books i,
    xmtable('$DESCRIPTION/Info'
    , columns AUTHOR varchar(100) path 'Authors'
    , INFO varchar(400) path 'Description'
    ) as t"
    find_by_sql(xquery)
  end
end
```

**清单 7.1 - 用于列出所有书籍的 book.rb 文件内容**

在清单 7.1 中：

- 定义 `Book` 类

- 我们将在目录中使用的 `find_books` 方法。

- `find_books` 方法中使用的 `xquery` 语句。此 `xquery` 语句从两个表中检索列：`BOOKS` 表（使用别名 *i*）；以及使用 `XMLTABLE` 函数创建的表（使用别名 *t*）。有关 `XMLTABLE` 函数的更多信息，请参阅*第 2 章，DB2 pureXML*

- 可用于执行原始 SQL 的内置方法 `find_by_sql`。

> **注意：**
>
> 有关 Ruby on Rails API 的更多信息，请查看 `http://api.rubyonrails.org/`。

复制并粘贴清单 7.2 中显示的代码到文件 `<app_home>\bookapp\app\controllers\catalog_controller.rb`

这告知 `catalog` 控制器从哪里获取书籍。

```
class CatalogController < ApplicationController
  def index
    @books=Book.find_books
  end
end
```

**清单 7.2 - catalog_controller.rb 文件的内容**

在清单 7.2 中：

- 定义 `CatalogController` 类

- 定义了一个 `index` 方法。它获取由 `find_books` 返回的实例变量 `@books`，该方法在 `Book` 模型中定义。

复制并粘贴清单 7.3 中显示的代码到文件 `<app_home>\bookapp\app\views\catalog\index.html.erb`

```
<h1>DB2 on Campus Book Series</h1>
<% for book in @books -%>
<div class="entry" >
<h3><%= link_to h(book.title) ,book ,:id => book%></h3>
<h3>Authors</h3>
<%= book.author %>
<h3>Description</h3>
<%= book.info %>
<h3>Status</h3>
<span class="status" ><%= book.status %></span>
</div>
<% end %>
```

**清单 7.3 - index.html.erb 文件的内容**

上述 html 代码告诉视图如何显示书籍信息。

现在让我们看看代码的运行效果！将浏览器指向 [http://localhost:3000/catalog](http://localhost:3000/catalog)。它应该显示一个带有目录列表的页面，如下面的*图 7.28*所示。

![](img/5f6ba170efa3a607142589708531bef8_274_0.png)

**图 7.28 - 目录列表**

### 7.3.2 自定义布局

让我们使用层叠样式表（CSS）改进页面的外观。浏览到目录 `<app_home>\bookapp\public\stylesheets` 并创建一个名为 `style.css` 的文本文件。复制并粘贴*清单 7.4*中显示的代码到文件 `style`。

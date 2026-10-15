
此URL丢失了指定"MIT"的部分，因为学生的ID在系统中是唯一的；因此，如果我们确切知道想要哪个学生，再指定"MIT"就没有好处了。这种参数化形式对于URL概念最为核心；URL `/students/1`精确指向单个资源——一个特定的学生。索引资源可以在不同情况下显示不同的内容，但`/students/1`将始终显示学生1的当前状态。

前面示例中的*students*部分，当然，暗示了一个比我们示例更大的系统。Dancer实际上使得以这种方式扩展部分变得简单。我们可以稍后轻松地将`/students/`部分添加到我们的示例中。这意味着可以单独创建系统的各个部分，然后稍后将它们作为更大网站的子章节包含进来。在这个附录的后半部分，我们会看到这一点；现在，让我们定义一个路由处理器，该处理器将根据ID获取学生。

以下示例是`Example.pm`的缩写版本。列出的代码可以添加到现有代码之后，但当然要在`true;`行之前，该行必须始终位于模块的最后。

> 3. 这样做可能没有意义；这里的重点在于说明URL和协议（HTTP与file）之间的区别。

## 示例 E.7

```perl
# (Example.pm (abridged))

package Example;

use Dancer ':syntax';

use Student;

use List::Util qw(first);

# [abridged]

get '/:id' => sub {

    my $student = first { $_->idnumber == param->{id} } @students;

    if (! $student) {

        status 'not_found';

        send_file '404.html';

    }

    template 'index', {

        'students' => [ $student ]

    };

};
```

## 说明

我们将使用`List::Util`的`first`函数来查找ID与参数匹配的第一个学生。在这种情况下这是必要的。如果我们使用数据库或外部服务来查找这个学生，我们只需传递参数即可。习惯上，所有`use`行应放在同一位置，即顶部。

为了简洁，`$VERSION`和`@students`的定义，以及`get '/'`的路由处理器已被省略。

这个新的路由处理器将处理带有ID的根请求。语法`:id`有两个作用。首先，它指定路径在此处必须包含某部分；其次，它将包含的任何内容收集到名为`id`的参数中。如果没有提供此处，则此路由不匹配，并且另一个路由处理器`get '/'`像往常一样运行。

`params`由Dancer提供，代表请求中可用参数的哈希引用。因为路由定义指定了一个名为`id`的参数，每当这个路由处理器运行时，Dancer都会将信息收集到`params`哈希引用中的`id`键中。`List::Util::first`用于查找`idnumber`与参数`id`匹配的第一个学生。

如果未找到具有此`idnumber`的学生，则进入此代码块。

Dancer提供了`status`函数来更改响应的HTTP状态码。404 Not Found是对互联网上每个人都非常熟悉的状态码。`status`可以接收`404`或`not_found`。如果未找到学生，我们合理地设置状态码为`not_found`。

## 说明（续）

- 7. 并非返回常规模板，而是返回 `404.html` 文件。该文件位于默认 Dancer 安装的 `public/` 目录中。Dancer 为我们创建了此文件。它的样式与其他页面不同，但足以向用户告知错误信息。`send_file` 会发送 `public/` 目录中的任何文件，并立即结束响应。因此，这一行可以被视为从该子程序中返回；如果第 7 行已执行，则第 8 行不会执行。
- 8. 如果找到了某名学生，则使用与展示学生列表完全相同的模板来展示这单一的学生。
- 9. 模板 `index.tt` 期望在 `'students'` 变量中接收一个学生数组。数组以数组引用的形式发送给 TT。相应地，构造了一个匿名数组引用，以包含搜索找到的那唯一一名学生。该模板仅渲染一名学生——即由 `:id` 定义的学生。

记得重启之前运行的 `app.pl`，以编译新代码并获得新行为。

只需在浏览器 URL 中添加一个数字即可查看结果。文件中定义的学生其 `:idnumber` 值为 123 和 321。因此，在 URL 中添加这些数字将返回相应 `:idnumber` 的学生（见图 E.3）；任何其它数字将返回 404 页面（见图 E.4）；而不添加任何数字则返回学生索引，如图 E.2 所示。

![](img/8556abcb353c0991f12099420ec28735_850_0.png)

![](img/8556abcb353c0991f12099420ec28735_851_0.png)

**图 E.4** 对 URL _http://0.0.0.0:3000/124_ 的响应是 404，因为未找到该资源。

对于这一单一视图，我们使用与多视图相同的模板这一点很重要。毕竟，无论是因为索引中只有一名学生的原因，还是我们明确请求了一名学生，展示单一结果都应该是相同的。这鼓励了一致性，使得人类和机器都更容易理解我们返回的页面。这也使其更容易维护，因为需要理解用途的文件数量大大减少。

接下来，我们解决另一种参数化类型：查询字符串。查询字符串通常使用键/值对的 ampersand/equals 符号格式，但这并非必须。Dancer 会自动将此格式拆分为 `_params_` 哈希引用，但如果路由处理程序不期望此格式，它也提供了直接访问查询字符串的方法。

以下示例是 `_Example.pm_` 中现有 `_get '/'_` 路由处理程序的替代方案，再次为简洁起见进行了删节。

### 示例 E.8

```perl
# Example.pm (abridged)

package Example;

use Dancer ':syntax';

use Student;

use List::Util qw(first);

# [abridged]

2 get '/' => sub {

3   my @filtered_students;

4   if (!$params()) {

5       $filtered_students = @students;

6   } else {

7       my $params = params;

8       for my $student (@students) {

9           if ($params->{name}

10               && $student->name =~ /\@($params->{name})/i) {

11               push $filtered_students, $student;

12               next;

13           }

14           if ($params->{major}

15               && $student->major =~ /\@($params->{major})/i) {

16                   push $filtered_students, $student;

17                   next;

18               }

19               if ($params->{course}) {

20                   if (first { $_ eq $params->{course} }

21                       @{$student->courses}) {

22                       push $filtered_students, $student;

23                       next;

24                   }

25               }

26           }

27       }

28       

29       my $template_data = {

30           students => \@filtered_students,

31       };

32       

33       template 'index', $template_data;

34   };

35   

36   # [abridged]
```


```
MYSQL_CONNECT($db_server, $db_username, $db_password) OR DIE("Unable to connect to database");
@MYSQL_SELECT_DB("symetix") or die("Unable to select database");
```

## 从数据库读取数据

在 `browse_column()` 中，有一个从数据库读取数据的简单示例：

```
result=mysql_query('SELECT * FROM items WHERE category_id=$category_id');
$num_results=mysql_num_rows($result);
```

在第一条语句中，我们对 `items` 表运行了一个简单的 `SELECT` 语句。结果存储在 `$result` 变量中。在第二条语句中，我们对接收到的结果数量计数。

```
$row=mysql_fetch_array($result);
```

在这条语句中，我们正在从结果集中提取第一条数据。然后可以使用以下命令从该数据中提取每个字段：

```
$item_id=$row["item_id"];
```

在这种情况下，我们只是将变量 `$item_id` 设置为 `$results` 当前行 `item_id` 字段中包含的信息。从结果字符串中提取数据也有许多方法。PHP 是弱类型语言，这意味着持有各种类型信息（如数字、文本）的变量之间几乎没有区别；PHP 会根据变量的上下文进行判断。这使得代码代码编写非常容易。当然，如果你愿意，可以始终使用 `settype()` 强制将变量设置为特定类型。

## 安全

对于破解者来说，很容易注意到他正在使用会话 #443，并简单地更改自己的代码使其会话变为 #443，从而有效地劫持另一个用户的会话。最流行的购物车和安全 Web 应用通过组合日期、时间、随机数、用户 IP 地址或主机名等生成一个唯一且难以猜测的会话 ID 来对抗这一点。一个复杂且精密的方案是不可破解的。

## 针对 IT 管理员

### Linux 在 Web 服务方面真的比 NT/2000 更有优势吗？

Linux 提供了 UNIX 的所有传统优势，如稳定性、可扩展性和可靠性，但它还提供了易用性、大量强大且功能完备的实用、大量实用的免费软件以及一种与 NT/2000 区分开来的设计范式。在 Linux 中，就像在 UNIX 中，重点在于构建小型、模块化的程序，这些程序可以通过命令行连接在一起。尽管微软多年来一直尝试朝着这个方向发展（例如 COM/DOM/DOM），但他们的大多数应用程序和工具仍然是大型的单体应用，试图独立完成所有工作。相比之下，Linux 工具的设计旨在协同工作。打个比方，这意味着如果你用来筑塔的某个特定构件颜色不对，你可以将其拔出并替换为另一个，而不会导致整个结构崩塌在你头上。

微软相对于 Linux 的唯一优势之一就是其开发工具的易用性。然而，即使这一点也存在争议。微软的工具使得开发变得如此容易，以至于设计往往在原型出来后被忽视或丢弃。正如任何 DBA 都会说的，在开始任何编码之前，良好的数据库设计至关重要。微软工具试图让用户远离任务的复杂性。通常情况下，这是 Linux 正在的发展方向。

## 总结

在本章中，使用 PHP 和 MySQL 构建了一个购物车应用程序。我们期待听到对该代码的实现。完整应用程序（包括源代码、数据库转储和安装说明）根据 GNU 通用许可证第二版（GPLv2）免费发布在 `sourceforge.net`。

# 常见问题

- ：我们内部没有 PHP 专家，但有很多 Perl 专家。还有其他开源购物车应用吗？

答：最完整的购物车应用之一是 Minivend，它是用 Perl 编写的（http://www.minivend.com）。另一个优秀的基于 Perl 的购物车应用是 OpenCart（http://www.opencart.com, http://www.opencart.com/）。更多示例，包括 PHP 及其他语言的，请查看 Freshmeat（http://www.freshmeat.net）。

- Q：哪个 Web 服务器最快？

答：这取决于你提供的内容，当然取决于问谁。通常，对于提供静态 Web 页面（如 HTML 页面）以及不是由 PHP、ASP或其他语言生成的页面，最简单的 Web 服务器最快。更复杂的服务器包含缓存等功能以增强处理密集型功能（如动态页面生成）的速度，但这些功能

如果不需要它们，它们本身会产生一定的开销。通常情况下，安全功能也会极大减慢服务器的速度。因此，如果速度是主要目标，你需要仔细权衡各种选项，并根据你的需求进行平衡。

总的来说，Apache 是大多数用场景的最佳解决方案，因为它在功能和性能之间提供了卓越的平衡。

问：使用本章提供的购物车应用程序我需要任何特定的权限吗？

答：该购物车应用程序设计在一个由 Hurricane Electric 托管的服务器上，地址为 http://www.he.net。不需要 root 权限或其他异常访问权限。

问：我可以在哪里找到 PHP 专业人士？

答：如果你在寻找时很难找到合格的 PHP 专业人士，最好去他们经常出没的地方寻找。推荐的方法是在 http://phpbuilder.com 或 http://www.schaffner.net/emp/ 的职位板上发布信息。或者，你也可以向其中一个 PHP 邮件列表发送信息。

## 返回目录

## 附录 A

购物车应用程序的 PHP 脚本

```php
<?php
// 购物车应用程序
// 由 Jamie Becker 编写
// 版权所有 (c) 2000, Jamie Becker, jamiebecker@ring0.com

// 此程序是免费软件；你可以根据 GNU 通用许可许可证的条款 重新分发和/或修改它，// 以该许可证，或（根据你的选择）任何后续版本。

// 分发此程序是希望它有用，// 但**不提供任何保证**；即使没有对于 // 商业性或针对某一特定用途的适用性的隐式保证。请参阅 //
// GNU 通用许可许可证获取详细信息。

// 你应该已经收到 GNU 通用许可许可证的副本，
// 与此程序一起；如果没有，请写信给 Free Software
// Foundation, Inc., 55 Temple Place - Suite 330, Boston, MA 02111-1307, USA。

// 请访问 www.gnu.org 或 www.wsf.org 查看许可证的全文。

// 源代码已修改为 80 列。(JamieBecker, 1999/2/16)

// 强烈建议将此函数分离到独立的非公共
// 文件中并在此处包含。

function init_db_variables() {
    global $db_server;
    global $db_username;
    global $db_password;
    $db_server='localhost';
    $db_username='username';
    $db_password='password';
    $db_name='shopcart';
}
```

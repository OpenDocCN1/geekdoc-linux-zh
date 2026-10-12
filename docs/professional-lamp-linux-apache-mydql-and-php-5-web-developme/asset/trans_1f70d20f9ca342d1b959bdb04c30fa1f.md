
`stream_open()` 的最后一个动作是将组装好的 GD Lib 图像转换为 PNG 数据。这通过一种简单的方式实现：要求 GD Lib 将图像输出为 PNG，并使用输出缓冲区来捕获结果。

每次调用 `stream_read()` 都会返回另一部分 PNG 数据，并丢弃已经返回过的部分。

由于这是一个由即时生成数据组成的只读流，因此剩余的大部分流访问方法都没有意义。关于数据可以说的一点是还剩多少可供读取，这使得 `stream_tell()` 可以被定义。

使用此类代码的人无需了解它将 `nzmg://` 请求与响应匹配的具体操作。就其关心的内容而言，`nzmg://6482089266771200500` 只是另一个文件，恰好包含一张中央奥克兰 1 公里宽快照的 PNG 图像。

但请等一下。如果它只是 PNG 数据，而且只是一个文件，那么从所有实际目的来看，它就是一个 PNG 文件。确实如此。下面是一个使用该封装类的示例。假设类位于自己的 `orthophoto_stream.php` 文件中，且假设纬度和经度已经转换为北向和东向坐标，并且半径不会太大或太小。

```php
include_once('orthophoto_stream.php'); // 类必须先声明
                                    // 然后才能使用，当然。
function display_orthophoto($northring, $easting, $radius)
{
	$filename = sprintf('nzmg://64807%d0%d8%d', $northring, $easting, $radius);
	
	// 所有基于流的操作都在这里发生。
	$image = imagecreatefrompng($filename);
	
	// 进行一点后处理，使这段代码超越平凡。
	// 绘制一个指定半径的圆（图像毕竟是方形的），并在中心放置一个十字。
	// 我们需要找到图像的白色值
	$white = imagecolorexact($image, 255, 255, 255);
	if ($white == -1) // 好吧，它还不存在。
	$white = imagecolorallocate($image, 255, 255, 255);
	// 圆以图像为中心，大小刚好能触及边缘。
	$imageSize = imagesx($image);
	$middle = $imageSize >> 1;
	imageellipse($image, $middle, $middle, $imageSize, $imageSize, $white);
	imageline($image, $middle, $middle - 5, $middle, $middle + 5, $white);
	imageline($image, $middle - 5, $middle, $middle + 5, $white);
	imagestring($image, 0, 0, 0,
		'Sourced from Orthophoto R11 Auckland Crown Copyright Reserved.',
		$white);
	imagepng($image);
	imagedestroy($image);
}
```

不用说，这个示例是在实际使用和教育用途之间做出的妥协，`orthophoto_stream` 类还有许多可以改进的方向。

# 第 3 章

其中一个方向是，提供的 21 位数字文件名可以附加一个扩展名，以指示所需的图像格式，而不是固定生成 PNG。其他方向包括更现实（或至少更灵活）的存储机制，用户可以通过包含主机名和路径的更完善的 URL 来控制。还要考虑将部分读取工作移入 `stream_read()`，从而减少在任何给定时间需要保留的图像数据量。（然而请注意，由于 GD Lib 缓冲区只处理完整图像，你需要编写自己的代码来输出图像数据，该数据是正确的，但在等待未来输入之前仍不完整。）

如果你遵循 RFC 3986 中定义的流资源命名 URL 系统，并参考 RFC 2718 中的指南，你会受益匪浅。事实上，可能已经有一个正在使用的命名方案与你的应用程序相匹配。（官方注册表由互联网号码分配机构在 http://www.iana.org/assignments/uri-schemes/ 维护。）如果有，请使用它。这样，你的应用程序将来就能与其他使用相同方案的应用程序协作，而无需额外的 URL 转换层来粘合它们。（实际上，对于任何数据格式或通信协议也是如此——如果世界其他地方已经对你想要的东西达成了公认标准，就使用它，省去自己创建新标准的时间和精力。）

> 请注意，所有 PHP URL 都要求在使用方案名称后使用 `://`，无论是否涉及命名权限（主机），因为 PHP 使用该字符序列来区分 URL 和局部文件路径。在 RFC 3986 的术语中，PHP 仅实现了“hier-part”组件给出的四个生成式中的第一个，并将“naming-authority”组件设为可选。符合 RFC 的变通方法是将使用 `://`，隐式地将本地主机指定为命名权限。

## 总结

这是对 PHP 原生函数集中一些利用较少领域的简要介绍。通过使用这些功能，你的代码可以更紧凑、更可靠，同时不牺牲可读性。数组函数通常可以替代有时复杂的循环，将任务简化为单行代码和一个可以捕获并存储在库中以便重用的辅助函数。函数处理函数允许你在运行时不仅决定要使用哪个函数（switch 语句可以做到这一点），还可以决定要从哪些函数中选择，甚至从头创建函数。流允许你隐藏外部数据读写实现细节，使程序的其他部分能够将其视为另一个文件。

PHP 总是有新功能被添加——新的初始化设置以微调其操作，新参数增强现有函数的实用性（甚至久经考验的函数 `str_replace()` 在 PHP5 中也被赋予了新参数），新函数，甚至整个新的函数类别。这使得学习 PHP 成为一个持续的过程，总有一些你还不了解的东西。

![](img/ab27c6ac898db1f934d39fa127b14657_98_0.png)

# 第 4 章：高级 MySQL

大多数动态网站的关键要素之一是为其提供数据的数据库。从简单的新闻页面到复杂的出版系统或 CMS，数据库在管理网站内容方面发挥着核心作用。为了使网站顺利运行，了解数据库系统的一些技巧和诀窍是很有帮助的。在本章中，你将学习如何创建数据库，管理访问系统的各种用户账户，以及组合和优化你的 SQL 代码以执行复杂和精细的查询。

## 回顾基础

在着手更高级的功能之前，让我们快速回顾一下 MySQL 的使用。假设你刚接手一个新客户，一家汽车经销商。经销商的经理希望你创建一个网站，帮助他们跟踪汽车库存。没问题，你说，然后坐下来开始规划他们的 Web 应用程序。

在规划过程中，你想出了一个简单的多表数据库方案来存储他们汽车场地的数据。为了这些练习的目的，你决定创建类似于图 4.1 的数据库表。

你创建的是一个非常简单的数据库结构，涉及四个表。在 `New_Vehicles` 表中，显然你要存储新汽车的数据。可以为每辆库存汽车指定里程、价格、颜色和描述等属性。`Used_Vehicles` 表的结构与 `New_Vehicles` 几乎相同，但旨在存储你可能猜到的是二手车的记录。`Used_Vehicles` 表额外提供了几列，用于指示车辆是否经过认证或带有保修，以及一列用于里程。最后两个表 `Make` 和 `Model` 存储该经销商销售的各种品牌的通用制造商和型号名称。

**制造商（Makes）**

| 列 | 类型 |
| :--- | :--- |
| make_id | int |
| make_name | varchar(100) |

**型号（Models）**

| 列 | 类型 |
| :--- | :--- |
| model_id | int |
| model_name | varchar(200) |
| make_id | int |

**New_Vehicles**

| 列 | 类型 |
| :--- | :--- |
| vehicle_id | int |
| model_id | int |
| modelyear | int |
| price | decimal(10,2) |
| color | varchar(200) |
| description | text |

**Used_Vehicles**

| 列 | 类型 |
| :--- | :--- |
| vehicle_id | int |
| model_id | int |
| modelyear | int |
| mileage | int |
| price | decimal(10,2) |
| color | varchar(200) |
| certified | tinyint |
| warranty | tinyint |
| description | text |

*图 4.1*

## 创建数据库

你需要做的第一件事是在 MySQL 中创建数据库和表。首先，在命令行启动你的 MySQL 客户端，或者如果你有其他更习惯使用的程序，并且可以直接输入 MySQL 命令，请随意使用它。

```bash
shell$ mysql
```

这将打开 MySQL 监视器，其外观应类似于以下内容（如果你正在使用命令行客户端）：

```text
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2 to server version: 4.1.11-1og
Type 'help;' or '\h' for help. Type '\c' to clear the buffer.
mysql>
```

在许多情况下，你需要使用登录名和密码来访问 MySQL 客户端。为此，只需在 `mysql` 命令末尾添加 `-u username -p`，MySQL 就会提示你输入密码，如下所示：

```bash
shell$ mysql -u username -p
```



通过这个小程序，您已创建一个用户表单，验证了必填字段（以及电子邮件字段），并将输入收集到一个整洁的小数组中供您使用。您可以设置任意数量的规则，以确保脚本验证必填字段是否已输入，格式是否正确（数字、字母等），并且如您前面所见，还可以检查诸如正确格式的电子邮件字段等项。您还可以设置默认值以及您能在表单中实现的其他任何功能（如上传文件和使用图像作为“提交”按钮）。

## HTML Table

您可以使用此包轻松输出数据表，数据来源可以是数据库查询结果集中的数据，或者是仅存放在某个数组中等待您释放的数据。快速看看一个示例，以了解这个包是多么易用：

```php
<?php

require_once ("HTML/Table.php");

//set up attributes for our table, using common HTML attributes as
//array keys and their values as array values
$attributes = array("width" => "50%", "border" => "1");

//create a new table object
$table = new HTML_Table($attributes);

//configure table
//AutoGrow is for an unknown number of rows
//AutoFill inserts text for every empty cell
//Because we are pretending not to be sure how big our table will be, we
//will set this option to true.
$table -> setAutoGrow(true);
$table -> setAutoFill("-");


//get some data for our table
$rows = array(
	'0' => array("Number One", "Number Two", "Number Three"),
	'1' => array("Numero Uno", "Numero Dos", "Numero Tres"),
);

//populate the table
for($nr = 0; $nr < count($rows); $nr++) {
	//the header row comes first
	$table -> setHeaderContents( $nr+1, 0, (string)$nr);
	for($i = 0; $i < 3; $i++) {
		if("" != $rows[$nr][$i])
		//the cell contents come next
		$table -> setCellContents( $nr+1, $i+1, $rows[$nr][$i]);
	}
}

//set background for every other row
//skip the first row so we use a value of 1 to start
$altRow = array("bgcolor"=>"#FFFCCC");
$table -> altRowAttributes(1, null, $altRow);

//set header info for each cell of the table
//based on coordinates, 0,0 is top left cell.
//the third value is the contents to be shown
$table -> setHeaderContents(0, 0, " ");
$table -> setHeaderContents(0, 1, "Field 1");
$table -> setHeaderContents(0, 2, "Field 2");
$table -> setHeaderContents(0, 3, "Field 3");

//set attributes for the header rows and first column
//first row and column = 0 .
$ShrAttrs = array("bgcolor" => "#FFF6AD");
$table -> setRowAttributes(0, $ShrAttrs, true);
$table -> setColAttributes(0, $ShrAttrs);

//send it to the browser
echo $table -> toRTML();

?>
```

您可以想象，根据用户输入或数据库结果创建表格是多么容易，以及通过改变这里那里的几个变量所能实现的自定义程度。

### 还有其他什么？

请浏览完整的 PEAR 包列表（可在 `http://pear.php.net/packages.php` 找到），您将会开始欣赏 PEAR 社区的广度与深度。可用的优秀包如此之多，本书篇幅有限，无法涵盖所有内容。为了简要列出除本章讨论过的之外更实用的主题，这里提供一些列举：

- 基准测试
- 缓存
- 配置
- 加密
- 事件
- 文件格式
- 文件系统
- Gtk 组件
- HTTP
- 图像
- 国际化
- 日志记录
- 邮件
- 数学
- 网络
- 数字
- 支付
- 流
- 系统
- 文本
- 工具和实用程序
- 验证
- Web 服务
- XML

## 探索 PECL

虽然 PECL 没有 PEAR 那么庞大，但这并不意味着它没有价值。与 PEAR 相比，可用包的文档和功能范围更为有限。许多 PECL 包仍处于测试阶段，属于实验性质；因此，使用这些包可能需要一些适应过程。然而，PECL 中确实包含一些非常有用且有时是特定用途的包，我们将简要查看其中一些更受欢迎的包，以让您了解它们包含的内容。如果您希望获得关于 PECL 包的更详细解释，我们在第 10 章中已经对 PDFLib 进行了说明。

### Fileinfo

`Fileinfo` PECL 包是 PECL 站点上的热门下载之一，并且其实用性极高。借助此扩展，您可以获取文件的各种信息，例如 *MIME* 类型。此包可以从 `http://pecl.php.net/Fileinfo` 下载。

此包的文档相对有限，这与许多 PECL 包的情况相同；不过，PHP Wiki（`http://www.wiki.cc/php/Fileinfo`）上有一篇简短的 Wiki 文档提及了此包。

### PDO

截至本文撰写时，`PDO` 仍处于测试阶段，被视为实验性功能，但它对 PHP 未来在数据库交互方面的发展具有巨大潜力。此包的目的是与 Data Objects 进行交互，并允许您轻而易举地更改数据库类型。无需使用特定于数据库的函数（例如 `mysql_connect` 或 `pg_connect`）进行编码，您可以创建一个新的 `PDO` 对象，它会为您处理这些事项。然后，只需在对象实例化期间更改一个参数，即可从 `MySQL` 切换到 Postgres（或许多其他数据库）。您可以从 `http://pecl.php.net/package/PDO` 下载 `PDO`。

随着 `PDO` 影响的扩大，其文档也在增加。PHP 手册（`http://us3.php.net/manual/en/ref_pdo.php`）中有关于此扩展的文档，此外在前文提到的 PHP Wiki（`http://www.wiki.cc/php/PDO_Basics`）上也有相关内容。

### Xdebug

这是另一个热门的 PECL 下载，可在 `http://pecl.php.net/package/Xdebug` 获取。其功能是通过提供有关代码、激活、执行和变量值的信息，协助 PHP 开发人员调试脚本。它还提供内存分配和保护，防止无限循环，以及堆栈和函数跟踪。

此包的文档比其他包更为详尽；它甚至拥有自己的网站 `http://www.xdebug.org`。

## 摘要

至此，您应该已经做好了深入研究 PEAR 和 PECL 的准备，并且能够停止反复编写和重写相同的代码。一旦您熟悉了 PEAR 和 PECL 的设置，也许您会将一些已编写的代码贡献出来，加入那些备受推崇的贡献者行列，将其作为新包分享给大众。

## 代码效率

您提供页面的速度越快，您的网站就越能在不造成用户延迟的情况下处理更多业务。本章介绍了提高网站性能的方法，以及如何确定哪些方法可能最有效。

“在更短的时间内提供更多内容”是其中的基本原理。正如有些汽车爱好者会在每一个空闲时刻深入汽车的内部，试图将四分之一英里的时间再缩短零点一秒一样，也有网站开发人员想要将登录页面的显示时间再缩短一毫秒。事情可以做得过头！

您不希望把时间浪费在无人会察觉的改进上，因此本章的第一部分将介绍几个小案例，用以说明即使巨大的改进有时也可能带来微乎其微的差异，微小的改进又能带来多大的区别，以及在动手修改之前了解整个系统的重要性。



```
echo "Quantity: $this->quantity<br>\n";
}

public function buyProduct($amount) {
$this->quantity -= $amount;
}

public function addProduct($amount) {
$this->quantity += $amount;
}
?>
```

现在，你可以在任何需要它的程序中使用 Product 类。你只需在使用该类之前，使用 include() 函数将 Product.inc.php 代码包含进来以定义该类即可。

+   2. 在 /var/www 文件夹中创建一个名为 ProdTest.php 的文件，并添加以下代码：

```
<?php
include("Product.inc.php");

$prod1 = new Product("Carrots", 1.50, 10);
echo "Just added product:<br>\n";
$prod1->printProduct();
$prod2 = new Product("Onions", 2.00, 15);
echo "<br>Just added product:<br>\n";
$prod2->printProduct();
echo "<br>Buying 4 carrots.\n";
$prod1->buyProduct(4);
$quant = $prod1->getQuantity();
echo "Quantity is now: $quant<br>\n";
echo "Buying 3 onions...\n";
$prod2->buyProduct(3);
$quant = $prod2->getQuantity();
echo "Quantity is now: $quant<br>\n";
echo "Adding 10 more carrots...\n";
$prod1->addProduct(10);
$quant = $prod1->getQuantity();
echo "Quantity is now: $quant<br>\n";
?>
```

Product.inc.php 文件包含 Product 类的类定义代码。将类定义代码放在单独文件中是一种常见做法，这样你就可以在任何想要的 PHP 程序中使用该类。

图 30-7 显示了此代码生成的输出。

将类文件命名为与类名相同并不是必需的，但这确实会让生活更轻松！你只需使用 include() 函数将类定义代码引入应用程序代码。一旦包含类定义，就可以使用它创建任意数量的类对象来处理数据。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_797_0.png)

图 30-7：在程序中使用 Product 类的输出。

## PECL 与 PEAR

由于 PHP 是一个开源项目，共享是其核心理念。有两个大型的 PHP 资源集散地：

+   ◆ PHP 扩展社区库（PECL）
+   ◆ PHP 扩展与应用库（PEAR）

PECL 为查找执行特定任务的 PHP 扩展提供了绝佳场所，例如与 POP3 邮件服务器交互。扩展为 PHP 语言提供了额外功能。

PEAR 提供了一个发布实际应用程序的存储库。这些应用程序大多以面向对象的形式发布，因此使用它们就像在项目中包含源代码并使用对象方法一样简单。其中发布的各种软件包涵盖了许多新奇的功能，例如生成交互式日历以及通过远程 SMTP 服务器发送电子邮件。

## 小结

Ubuntu 在 LAMP 环境中提供了完整的 PHP 开发和生产环境。本章讨论了如何确保你已安装 LAMP 环境，然后逐步介绍了 PHP 编程语言的基础知识。PHP 提供了你所期望的所有标准编程特性，外加一些额外功能。它还提供了将数据库与网页衔接的函数，让你能够向数据库提交 SQL 查询并检索结果。PHP 还为专业编码项目提供了更高级的面向对象特性。PECL 和 PEAR 网站是资源集散地，让你能够与他人分享自己巧妙的 PHP 作品——也能受益于他人的辛勤劳动。只需在网站中添加几行 PHP 代码，就可以创建一个完整的动态 Web 应用程序。

感谢你与我一起踏上这段 Ubuntu Linux 系统之旅。我希望你喜欢使用 Ubuntu，并学到了许多可以在系统上做的新事物。但不要就此结束你的 Ubuntu 学习之旅。Ubuntu 每 6 个月发布一个新版本。每个新版本中总有新东西值得探索。与 Ubuntu 社区保持联系，并持续关注新的进展和功能。

## 索引

A
A（命令），145
a（命令），145
A（互联网地址）记录，473，475
AbiWord，24
关于 GNOME（菜单选项），84
关于 Ubuntu（菜单选项），84
绝对文件路径，450–451
绝对路径名，758
.acc（高级音频编码），278
Access（Microsoft），180，182。另见 Base 包；数据库
访问控制，421。另见权限
访问控制组，373–374
无障碍功能，101–105，106
F5 键和，38
键盘和，104
鼠标和，104–105
键入工具，103
视觉工具，102–103
Writer 和，164
无障碍功能键，104
附件子菜单，82
账户管理对话框，237
账户对话框（Pidgin），214
操作行特殊字符（procmail），576
Active Directory（AD）网络，523
AD（Active Directory）网络，523
添加规则对话框，248
添加/删除应用程序，322–327
加载项（Tomboy），159
附加组件（Firefox），210–212，224，306，307。另见插件
附加组件对话框，211
添加/删除应用程序工具，322–327
添加/删除子菜单，82
通讯录（Evolution），250–252
通讯录联系人编辑器对话框，251
通讯录联系人窗口，251
通讯录搜索，92
调整颜色窗口（F-Spot），275
管理。见系统管理；用户管理工具
管理（菜单选项），84
ADSL（非对称数字用户线路），340
高级音频编码（.acc），278
高级加密标准（AES），343
高级 Linux 声音架构。见 ALSA
高级选项窗口，66–67
高级搜索对话框，241
AES（高级加密标准），343
ALSA（高级 Linux 声音架构），199，281
混音器窗口，283
项目网站，279
alsa-utils，434
备用安装 CD（Ubuntu 安装过程），67–70。另见软件仓库 v.，316，317
服务器 LiveCD 安装 v.，70–71
用其升级 Ubuntu，76
总在最前（插件），300
amaroK，17
AMP，498。另见 LAMP
Apache Web 服务器，499–505
配置文件，500
与 LAMP，499–505
模块，500–501
测试，503–505
与虚拟主机，502–503


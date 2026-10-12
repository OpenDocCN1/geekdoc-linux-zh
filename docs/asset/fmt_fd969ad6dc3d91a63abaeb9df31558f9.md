
`$query = "SELECT id, item, price FROM specialoffers ORDER BY id LIMIT 15 OFFSET " . $input;`

```

观察第一行，你可以看到你没有过滤名为`$input`的变量。这意味着该变量在SQL语句的某行中使用，它可能包含攻击者想要使用的任何代码。随着经过构造的注入被注入，会引起各种混乱。

另一个例子是更新管理员的密码。例如，一个正常的SQL语句PHP代码可能像这样：

```php
$query = "UPDATE credentials SET passwd='$password' WHERE userid='$id';";
```

通过向此语句附加SQL，例如像`'sysop%'`这样的用户，你的SQL变得非常不严格，让数据库搜索类似于`sysop`的其他用户名，然后更新它们的密码。

遗憾的是，还可能在SQL中包含执行shell命令。

## 在 PHP 中缓解 SQLi

正如我所说，这个主题太大，无法详细介绍，但我将简要介绍如何过滤输入来缓解SQLi攻击。多种PHP函数可以帮助你完成这一任务。在写作期间，PHP从`5.6`版本重大移动到了`7.0`。旧版本（到`5.3`）中，你的主配置文件（`php.ini`）可以通过魔法引号（`magic quotes`）过滤所有输入。这显然被废弃了因为它过度依赖它。

为了保护第一个示例中的变量，你可能想通过`addslashes`运行用户输入。示例如下：

```php
$input = addslashes($variable);
```

使用`mysqli`，它可能像这样：

```php
$input = mysqli_real_escape_string($variable);
```

为了防止不受欢迎的输入，还有`trim`用于从变量中移除空格，与`strip_tags`以相同的方式用于HTML和其他标记。这些都可以链在一起，例如：

```php
$input = strip_tags(trim($input));
```

除了PHP`5.5.0`版本，你可以使用`mysql_real_escape_string`函数来清理你的字符串：

```php
$input = mysql_real_escape_string($input);
```

然而，从`7.0.0`开始，几乎总是想要使用`mysqli`驱动（改进后的`MySQL`）来对抗SQLi。益于此增强，你可以使用更高级的方法剥离执行代码中不必要的且危险的字符。使用`mysqli`的示例与之前的不同：

```php
$input = mysqli_real_escape_string($input);
```

使用`mysqli`通过以下方法连接到数据库：

```php
$mysqli = new mysqli("localhost", "userid", "DB_Name");
```

缓解SQL攻击的另一种方法是使用预处理语句（prepared statements）。这种安全添加背后的思想是数据库引擎完全处理任何使用的参数。在这种理论下，攻击者无法向他们创建的查询注入代码。示例如下：

```php
$input = $mysqli->prepare("INSERT INTO table_name (column_name) VALUES (?)");

$input->bind_param("s", $actual_user_input);

$input->execute();

$input->close();
```

额外的帮助是这种函数只需要读取一次，所以如果在几个页面上使用多次，PHP引擎的工作就更少。

另一种方法自PHP早期版本起可用并使用PHP Data Objects (`PDO`)。这里有一个好的讨论：`https://stackoverflow.com/questions/60174/how-can-i-prevent-sql-injection-in-php`。

哪种方法最好，但`PDO`看起来非常流行。`PDO`的示例看起来如下：

```php
$input = $pdo->prepare('SELECT * FROM special_offers_table WHERE offerer = :name');

$input->execute(array('name' => $variable));
```

关于`PDO`有很好的信息位于`http://whatever.com/blog/2014/08/28/the-heart-of-darkness/`。值得一读，仅仅是为了帮助你在PHP后期版本（`7.0.0`及以后）中选择方法来对抗SQLi注入。

## 利用 SQL 漏洞

现在你已经查看了几种防御SQLi的方法，你将学习黑客可能如何攻击你的在线服务。有很多可用工具，我将关注`sqlmap` (`http://sqlmap.org`)，它是黑客、法医科学家和渗透测试人员中一种流行的开源工具。使用这种复杂的工具可能会造成混乱，因此请确保你完全意识到在自己的服务器上测试它时可能造成的损害，更不用说属于别人的服务器了。我绝对建议使用开发服务器或沙箱虚拟机以确保安全。

`sqlmap`广泛的能力让大多数反对者担心。根据其网站，`sqlmap`支持以下数据库服务器：`MySQL`, `Oracle`, `PostgreSQL`, `SQL Server`, `Microsoft Access`, `IBM DB2`, `Firebird`, `Sybase`, `SAP DBD`和`HQDB`。

让我们看看如何安装`sqlmap`。它包含在`Kali Linux`等某些安全发行版中，但如果它不在你的包管理器仓库，还有其他的安装方法。

你可以使用`Git`命令使用`GitHub`上的`sqlmap`仓库：

```bash
$ git clone https://github.com/sqlmapproject/sqlmap.git sqlmap-dev
```

从`https://github.com/sqlmapproject/sqlmap/zipball/master`还有一个Zip文件可用。

`![](img/0de912db8d05f7607e7b5b15fbf73eaa_125_0.png)`

## 第 10 章：SQL 注入攻击

你也可以从`https://github.com/sqlmapproject/sqlmap/tarball/master`下载tar包。

一旦你按照安装说明完成操作，应该能够进入运行以下命令的阶段（在运行之前的`Git`命令后，这就是你入门需要做的全部工作）：

```bash
# cd sqlmap-dev

# python ./sqlmap.py -h
```

此命令将为你提供一个选项列表。

## 启动攻击

现在让我们来看看`sqlmap`功能的核心，即攻破远程机器。

但请注意，测试你的`sqlmap`技能最耗时的方面可能是搭建你自己的易受测试服务器，或者合规地识别易受攻击的网站。你可能会对读这些内容感到惊讶，因为由于URL的构造方式，`Google`可以很容易地识别漏洞网站。希望不言而喻，我不提倡攻击通过`Google`或任何其他方法发现的任何网站。不过，为了假设可能被利用的URL，你可以输入如`inurl:website.php?id=`或`inurl:product.php?id=`这样的查询语句。第一个搜索词返回了令人担忧的`170`万条结果。

通过`Google`不专业地暴露漏洞的网站和其他在线资源获得了一个绰号——`Geogledords`（谷歌搜索出的漏洞）。有一个网站列出了其中许多站点；值得一看，可以在`www.hackersforarchy.org/ghdb/`找到。这些列表包含了许多可能的机密登录页面、敏感目录以及提到用户名的文件。请负责地使用这些信息。

顺便提一下，你可以通过`Python`运行`sqlmap`，这意味着你需要在机器上安装某种类型的`Python`实现版本。

在`10.1`节中你可以看到开发者们非常希望与非法活动保持距离。这种强大的工具总是容易被滥用。

让我们继续。看看下面的示例，使用`sqlmap`命令所需的语法非常简单：

```bash
# python sqlmap.py -u "http://www.a-vulnerable-website.com/product.php?id=1111"
```

## 图 10.1

启动`sqlmap`时的界面，包含所有权声明

```
sqlmap-dev # python sqlmap.py -u "http://www.a-vulnerable-website.com/product.php?id=1111"

(1.0-dev-aee7d3)

****** http://sqlmap.org

[i] 法律声明：未经事先许可使用 sqlmap 攻击目标是违法的。用户有责任遵守任何相关的当地、州和联邦法律。开发者不承担责任，且不对本程序的任何误用负责

[*] 启动于 16:02

[INFO] 正在测试与目标 URL 的连接
```

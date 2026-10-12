
# 背景与挑战

问题是，没有人预料到 Facebook 会像现在这样方式增长。PHP 和 MySQL 并不是为了处理 1,000,000,000 个用户而设计的。由于规模的原因，许多可以在 `HHVM` 中实现的功能可能需要几个月，或者在较低的性能水平下可能永远无法实现。

- 1. 优化运行在其上的所有工作
- 2. 优化你的自定义基类，使其能够处理相应的负载。

Facebook 选择了开发速度而非成本，因此他们确实在使用的技术上投入了时间和金钱。作为他们工作的结果，Hack 让 Facebook 桌面站执行速度翻了一倍，且没有影响开发。Facebook 项目的下一步，是一个用于将 PHP 转换为 C++ 的开源工具。

# 开始上手

我们首先需要做的是获取 `HHVM`。使用 `Apt` 完成这非常简单。让我们添加 Hack 的存储库并安装它。

```bash
echo deb http://packages.facebook.com/ubuntu trusty | sudo apt-get update
sudo apt-get install hhvm
```

几分钟后，Hack 应该就绪了。让我们创建一个新的测试并插入以下内容：

```php
echo "hello";
```

现在，让我们在 `hhvm test.php` 中运行代码。在终端中，你应该看到一个类似 `3.x` 的新版本。如果是这样，你就准备好配置 Hack 并与我们的服务器连接了。`Hack/HHVM` 包含了所有可以作为服务器运行的内容。这在 `3.0` 版本中被移除，因为目标是使用 `HHVM` 作为 JIT 编译器。

# Hacklang 简介

安装 Hacklang，配置 Apache 服务器并构建一个 Hack 应用

## 特性

必须初始化它们，但仅当 `$this` 执行那些声明的变量且我们尚未设置值时——这就是为什么如果我们写 `$this->connection`，它将只存在于调用 `$this` 的作用域内，因此其他需要它的对象将无法使用。

将图 03 中的函数添加到 `connect.php` 中的 `Database` 类中；这段优美的代码将处理我们创建的数据库连接查询，首先初始化类。

```php
class Database{
    private boolean $connection = False;
    private Object $connection;

    public function connect(string $addr, string $user, string $pw, string $db) {
        int $int;
        if($db == null()) {
            return 0;
        }
        $this->connection = mysqli_connect($addr, $user, $pw, $db) or die("" . mysqli_error($connection)");
        if($this->connection == null) {
            return 1;
        } else {
            $this->connection = False;
            return 0;
        }
    }
}
```

## 发起第一个请求

让我们继续现在发生。回到 `index.php`，在 `require_once` 语句之后添加图 04。

如果你访问服务器上的 `index`，你应该再次更改数据库中 `posts` 的内容；但仍然有点简单。让我们用一些 `GET` 和 `POST` 参数来改变一下。

## 缺点是什么？遗漏了什么吗？

为了获得优化（尤其是 Hack 能够实现的那些优化），必须牺牲一些东西。在大多数情况下，Hack 缺失的 PHP 函数和功能列表是不可接受的——例如像 `arrays()` 这样的函数在任何地方都不会运行，循环中没有 `break` 或连接，而且没有位运算符。

然而，最显著的 PHP 特性是 Hack 认为成功的关键——与 HTML 内容的无缝互操作。这种逻辑背后的思想是 Facebook 对 PHP 做出决策的关键。

PHP 是一种模板语言，而 Hack 是一种计算语言。Hack 的工作是能够处理和输出数据，而不是构建显示它的页面。不过不用担心，Hack 与 PHP 构建的模板是可以交互的：

```php
public function query(string $q) void {
    if($this->connected == True) {
        $result = $this->connection->query($q);
        return $result;
    }
}
```

```php
$db = new Database();
$db->connect("127.0.0.1", "USER", "PASSWORD", "DATABASE");
$var_dump($db);
$q = $db->query("SELECT * FROM posts");
$data = array();
while($row = $q->fetch_array($q)) {
    $object = array("name" => $row["name"], "tag" => $row["tagline"], "content" => $row["content"], "date" => $row["date"]);
    array_push($data, $object);
}
echo json_encode($data);
```

![](img/a17757b82ff78d9c8d36ac46319604f3_52_0.png)

# 高级特性与工具

## LinuxDeveloper

```php
function fetchGET(): Map<string, mixed> {
  return Map::fromArray($GET);
}
```

```php
function fetchPOST(): Map<string, mixed> {
  return Map::fromArray($POST);
}
```

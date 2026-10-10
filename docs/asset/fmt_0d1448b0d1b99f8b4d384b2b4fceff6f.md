
PHP 程序可以像列表 12-1 所示编写，并放置在 `/var/www/html/` 目录中。与 CGI 脚本类似，它通过执行 `dht` 程序来与 DHT 传感器接口，产生图 12-6 所示的输出（参见 `chp12/hello.php`）。

### 列表 12-1: `/var/www/html/hello.php`

```php
<?php $temperature = shell_exec('/usr/local/bin/dht'); ?>

<?php $cpu_temp = (float)

$file = file_get_contents('/sys/class/thermal/thermal_zone0/temp'); ?>

<html><head><title>RPi PHP</title></head>

<body>

<h1>Hello from the Raspberry Pi!</h1>

<div>Your IP address is: <?php echo $_SERVER['REMOTE_ADDR']; ?></div>

<div><?php echo $temperature?></</div>

<div>The CPU temperature is: <?php echo $cpu_temp/1000; ?>°C*</div>

</body>

</html>
```

> 注意：要输入 Unicode 符号，可以按 Ctrl-Shift-u 并输入 Unicode 值，例如 `00b0` 表示度数 (°)。按回车键后符号就会出现。此外，`00a9`=°，`00b1`=±，`00b5`=µ，`00d7`=×，以及 `007f`=≠。

## 第 III 部分 高级接口与交互

![](img/8d97725dcf071daded8acede3920e981_521_0.png)

图 12-6: 一个基于 PHP 的 Web 天气传感器

## GNU CGIC 应用（进阶）

通用网关接口（CGI）允许浏览器使用 HTTP POST 或 GET 请求向脚本/程序传递环境和应用程序信息。几乎所有的编程语言都可以用于构建 CGI 应用，因为它们在事务中的作用是解析由服务器发送的输入，并构建合适的 HTML 输出响应。

GNU CGIC 是一个用于构建 CGI 应用的 C++ 库。它非常强大，并极大简化了构建应用程序的过程，允许你通过基于 HTML 表单的接口通过互联网与树莓派（RPi）进行交互。可以认为这是解决嵌入式 Web 服务器与浏览器客户端交互问题的“过时方法”——它自 1990 年代以来一直存在着。在某种程度上事实确实如此。目前有强大的替代方案，如 Java Servlets、Node.js、Dart 和 PHP；然而，这种方法：

- 对树莓派的开销较低，因为代码是编译的而非解释执行的
- 允许直接访问系统调用
- 可以使用 `wiringPi` 等代码库直接与硬件交互

缺点是它并不真正适合初学者，输出语法很冗长，且会话管理很复杂。尽管如此，值得指出的是，大型 Web 应用（包括 Google 和亚马逊的应用）在其服务器上使用 C++ 处理性能关键型系统。树莓派不是高端服务器，因此任何性能优化都是受欢迎的，甚至可以以增加复杂性为代价。
可以使用以下步骤下载并安装 CGIC：

```
pi@rpi $ mkdir cgcic
pi@rpi $ cd cgcic
pi@rpi ~/cgcic $ wget http://ftp.gnu.com/gnu/cgcic-3.2.16.tar.gz
pi@rpi ~/cgcic $ tar xvf cgcic-3.2.16.tar.gz
pi@rpi ~/cgcic $ cd cgcic-3.2.16/
pi@rpi ~/cgcic/cgcic-3.2.16 $ ./configure --prefix=/usr
```

## 第 12 章 · 物联网 495

```
pi@erpi ~ /cgic/cgic-3.2.16 $ sudo make
pi@erpi ~ /cgic/cgic-3.2.16 $ sudo make install
pi@erpi ~ /cgic/cgic-3.2.16 $ ls /usr/lib/libcgic
```

# 498 第三部分 高级接口与交互

# LAMP 与 MEAN (继续)

```javascript
var server = app.listen(5050, function () {
  var host = server.address().address;
  var port = server.address().port;
  console.log('Application listening at http://%s:%s', host, port);
});
```

这段 Node.js 代码创建了一个 Express 服务器，它在端口 5050 上监听连接。你可以使用 浏览器连接到该服务器，如图 12-8 所示。

```
pi:-http:// node hello.js
Application listening at http://:5050
```

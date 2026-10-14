
```
# tar zxvf php-3.0.14.tar.gz
```

接下来，将目录切换到包含解压后源代码的子目录：

```
# cd php-3.0.14
```

你可以通过以下两种方式之一从源代码构建 PHP：

- **作为 Apache 的动态共享对象（DSO）：** 使用此选项，你无需重新编译 Apache。Apache 将从外部文件加载 PHP 模块。这是编译和安装 PHP 的首选方法。如果你使用的是 Apache 1.3.6 或更高版本，可以使用此选项。本章将介绍如何将 PHP 构建为 Apache 的 DSO。
- **作为 Apache 的静态对象：** 使用此选项，你需要使用 PHP 支持重新编译 Apache。对于早期版本的 Apache，或者如果你选择不使用动态 Apache 模块，请使用此方法。

> **注意：** 本章中的安装说明假定 Apache 已按照第 23 章“Apache 与万维网”中的说明安装。

编译和安装需要四个步骤：

1. 使用 `configure` 命令配置源代码以进行安装。以下是最基本的 `configure` 命令：

```
# ./configure --with-apxs=/usr/local/apache/bin/apxs
```

`--with-apxs` 参数的值应为 Apache 发行版附带的 `apxs` 脚本的完整路径。如果你使用默认设置从 Apache 源代码安装 Apache，则此路径为 `/usr/local/apache/bin/apxs`。

在 Red Hat 6.2 上，此脚本通常安装在 `/usr/sbin/apxs`。除了 `--with-apxs` 选项之外，PHP 的 `configure` 脚本还支持大量参数，允许你自定义 PHP 支持的功能。这些参数将在本章后面的“PHP 安装配置参数”中讨论。

2. 使用以下命令编译源代码：

```
# make
```

3. 使用此命令安装编译后的软件：

```
# make install
```

4. 使用此命令重启 Apache：

```
# /usr/local/apache/bin/apachectl restart
```

在 Red Hat Linux 上，你可以使用以下命令重启 Apache：

```
# /etc/rc.d/init.d/httpd restart
```

安装并运行 PHP 后，最好测试一下安装是否成功。为此，请创建一个测试 PHP 文档。最简单的 PHP 文档将包含一条命令：

```php
<? phpinfo(); ?>
```

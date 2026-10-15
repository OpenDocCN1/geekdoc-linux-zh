
```php
foreach ($settings as $setting)
{
    $value = $setting['value'];
    // 将布尔值转换为 ini_get() 的值
    switch (strtolower($value))
    {
        case 'off':
        case '0':
        case 'false':
        case 'no':
            $value = '';
            break;
        case 'on':
        case 'true':
        case 'yes':
        case '1':
            $value = '1';
            break;
    }
}
```

接下来，你获取配置变量的名称。由于像数组一样访问属性返回一个 `simplexml_element` 对象，你需要将其显式转换为 `string` 以便稍后与 `string` 值进行比较：

```php
// 扁平化名称
$name = (string) $setting['name'];
```

现在你已经拥有了 XML 配置文件中要求的设置的名称和值，你可以将其与运行时设置进行比较。首先，你检查该配置设置是否存在于运行时配置数组中，然后将其与 XML 文件中的值进行比较。再进一步，如果该设置存在但不匹配，请尝试使用 `ini_set()` 更改当前的运行时配置变量。如果设置不匹配 *且* 你无法在运行时更改该设置，系统将生成一条错误消息，并且该函数将返回 `false`：

```php
// 检查配置值，如需要则设置
if (!array_key_exists($name, $cfg) or
    ($value !=
        $cfg[$name]['local_value']) and
    ini_set($name, $setting['value']) === false))
{
    $returnValue = false;
    $this->message = "Warning: " .
        $name .
        " not set to the required value of: " .
        $setting['value'] . "\n";
}
return $returnValue;
}
```

现在你已经拥有了这个由类和配置文件组成的小型层次结构来检查运行时环境，你需要在脚本中实际调用它们。在下面的 test.php 代码中，你可以看到调用配置检查器是多么简单：

```php
<?php

// 检查 PHP 环境
require_once 'class.ConfigManager.php';
$cfg = new ConfigManager('reqs.xml', 'xml');
$cfg->processConfig();
```

你所需要做的就是包含主要的 `ConfigManager` 类文件，创建一个新的 `ConfigManager` 对象，在实例化时传递文件名和类型，并调用 `processConfig()` 方法来实际检查设置。

## 摘要

希望你现在已经熟悉了一些可以为你的应用程序注入生命力的不同的配置设置和函数。了解运行时设置的价值通常有助于避免难以诊断的 bug，而能够在运行时更改值可以使你的应用程序足够灵活，以应对各种配置。这种知识和力量，结合自动配置检查，应有助于使你的应用程序在面对不熟悉的服务器可能带来的未知麻烦时，尽可能具有“厚脸皮”（即健壮性）。

## 6 Apache 技巧

本章暂时不再谈论 PHP，转而讨论一些你可能不知道的 Apache 特性。你已经知道 Apache 是最流行和最强大的 Web 服务器，并且 PHP 是设计为与 Apache 协同工作的，但你可能不知道你可以扩展 Apache 本身，以使你的站点运行得更有效。秉承其开源的本性，有许多优秀的模块可供 Apache 使用，这些模块扩展了其功能，并为作为站点管理员的你提供了有用的特性。

本章讨论了其中三个模块。`Mod_rewrite` 允许你提供 URL 替换以适应站点更改，但如果你正确使用它，你可以用它来保护你的站点并使其对搜索引擎更友好。`Mod_speling` 帮助纠正访问你站点的访客无意中犯的拼写错误。`Mod_deflate` 允许你在向用户发送内容时对其进行压缩，从而为你节省带宽费用。`Mod_auth_mysql` 让你通过利用用户数据库的功能结合 Apache 的身份验证来加强你站点的防护。`Mod_ssl` 允许你加密流向你的 Web 服务器和从其流出的数据。最后，`mod_dav` 允许你将你的 Apache Web 服务器用作分布式文件存储库。

## URL 重写

如果你召集世界上所有的 Web 开发人员和管理员，让他们列出可以与 Apache 一起使用的最重要模块，那么 `mod_rewrite` 一定会出现在那个列表中——这是有充分理由的。

`Mod_rewrite`，对于不熟悉的人来说，是一个提供 URL 重写功能的 Apache 模块。虽然这听起来可能很简单，但实际上 `mod_rewrite` 是 Apache 模块的瑞士军刀。你可以用 `mod_rewrite` 做什么？除了显而易见的简单 URL 重写之外，`mod_rewrite` 让你能够保持查询字符串输入的安全，使你的站点对搜索引擎友好，使你的 URL 对用户友好，在重新构建后保留“旧”URL，并阻止盗链。你会发现 `mod_rewrite` 很快就会不仅仅是一个简单的 URL 更改机器人。

# 第 6 章

### 启用 mod_rewrite

在着手配置 mod_rewrite 之前，你需要做的第一件事是检查它是否已经安装。在命令行中输入：

```
/path/to/httpd -l
```

*显然，请替换为你自己 Apache 的 httpd 路径。*

如果你看到 `mod_rewrite.c` 被列出，说明它已经编译进了 Apache。如果没有，请检查它是否作为 Apache 的动态模块存在：

```
ls /path/to/apache/modules/
```

如果文件列表中存在 `mod_rewrite.so`，则可以通过稍后在本节中展示的 `httpd.conf` 文件的少量调整，让 Apache 将其作为模块加载。如果它既没有编译进 Apache，也不作为共享对象可用，你可以使用操作系统提供的任何包管理系统来安装它；或者，如果你是更喜欢动手的类型，你可以自己重新编译 Apache 以包含 mod_rewrite。

在 Apache 中启用功能时，通常有两种选择：将其静态构建到 Apache 二进制文件中，或者将模块编译为可加载的共享对象。当将模块静态构建到 Apache 中时，它们无需额外的配置指令即可使用，但无论你是否需要该模块，只要 Apache 在运行，该模块就会一直处于激活状态并消耗内存。将模块构建为可加载的共享对象可以保持你的 Apache 二进制文件精简，不包含任何你可能需要也可能不需要的“*可选*”项，但需要在 `httpd.conf` 中手动配置。两种方法都可以接受，但如果你不确定选择哪种，共享模块路径因其灵活性而成为一种流行的选择。

在从源码构建 Apache 时，若要静态构建 mod_rewrite，请确保你的 configure 文件包含 `--enable-rewrite`，例如：

```
./configure \
--enable-rewrite \
# ...以及你使用的任何其他 configure 设置
```

如果你选择了动态模块路径，只需在启用 mod_rewrite 的行末尾添加 =shared：

```
./configure \
--enable-rewrite=shared \
# ...以及你使用的任何其他 configure 设置
```

然后，只需简单地制作并安装服务器到你的系统即可。如果你静态构建了 mod_rewrite，可以通过重新运行 `httpd -l` 来确认你的重新配置是否成功。如果 `mod_rewrite.c` 出现，说明它已成功添加到 Apache 二进制文件中。

相反，如果你选择了动态模块，首先检查它是否实际存在于 Apache 模块目录中，作为一个名为 `mod_rewrite.so` 的文件。

```
ls /path/to/apache/modules/
```

假设一切顺利，且 `mod_rewrite.so` 存在于模块目录中，你需要在 `httpd.conf` 中启用它，方法是取消注释现有行或添加类似以下的新行：

```
LoadModule rewrite_module modules/mod_rewrite.so
```

> 不要对任何静态编译进 Apache 的模块使用 `LoadModule` 行——仅限动态共享对象。对静态模块使用 `LoadModule` 只会生成错误。

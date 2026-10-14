
# 面向系统管理员的 Python

了解 Python 如何帮助系统管理，它敢于取代常见的 shell 脚本……

## 资源

- Python-devel Python 开发库，用于编译第三方 Python 模块
- setuptools setuptools 允许您轻松地下载、构建、安装、升级和卸载 Python 包

系统管理是我们计算环境的重要组成部分。无论你是在工作中还是在家中管理系统，这都无关紧要。Linux 作为基于 UNIX 的操作系统，已经拥有系统管理员所需的一切，例如世界级的 shell（不止一个，而是很多，包括 Bash、csh、zsh 等）、方便的工具，以及许多其他特性，使 Linux 系统成为管理员的梦想。那么，当 Linux 已经内置了一切时，为什么我们还需要 Python？作为一种动态脚本语言，Python 非常易于阅读和学习。这不仅仅是我们说的，许多 Linux 发行版实际上都在核心管理部分使用了 Python。例如，Red Hat（和 Fedora）的系统设置工具 Anaconda 就是用 Python 编写的（再读一遍这句话，明白与蛇的联系了吗？）。此外，像 GNU Mailman、CompizConfig Settings Manager (CCSM) 以及数百个小型 GUI 和非 GUI 配置工具都是使用 Python 编写的。Python 并不限制你选择用户界面——你可以使用 Python 构建命令行、GUI 和 Web 应用程序。这样，它几乎覆盖了所有可能的界面。

在这里，我们将研究如何使用 Python 执行与系统管理相关的任务。

## 解析配置文件

配置文件为应用程序提供了一种存储各种设置的方式。为了编写允许你修改特定应用程序设置的脚本，你应该能够解析该应用程序的配置文件。

在本节中，我们将学习如何解析 INI 样式的配置文件。尽管古老，但 INI 文件格式在许多现代开源软件中仍然非常流行，例如 PHP 和 MySQL……

php.ini 配置文件摘录。

```
[PHP]
engine = On
zend.ze1_compatibility_mode = Off
short_open_tag = On
asp_tags = Off
precision = 14
y2k_compliance = On
output_buffering = 4096
;output_handler = 
zlib.output_compression = Off

[MySQL]
; Allow or prevent persistent links.
mysql.allow_persistent = On
mysql.max_persistent = 20
mysql.max_links = -1
mysql.default_port = 3306
mysql.default_socket = 
mysql.default_host = localhost
mysql.connect_timeout = 60
mysql.trace_mode = Off
```

Python 提供了一个名为 ConfigParser（在 Python 3.0 中称为 configparser）的内置模块。你可以使用该模块来解析和创建配置文件。

```
@code:writeconfig.py
@description:The following demonstrates adding MySQL section to the php.ini file.
@warning: Do not use this script with the actual php.ini file, as it's not designed to handle all aspects of a complete php.ini file.
import ConfigParser
config = ConfigParser.RawConfigParser()
config.add_section('MySQL')
config.set('MySQL', 'mysql_trace_mode', 'Off')
config.set('MySQL', 'mysql.connect_timeout', '60')
config.set('MySQL', 'mysql.default_host', 'localhost')
config.set('MySQL', 'mysql.default_port', '3306')
config.set('MySQL', 'mysql.allow_persistent', 'On')
config.set('MySQL', 'mysql.max_persistent', '20')

with open('php.ini', 'a') as configfile:
    config.write(configfile)
```

输出：php.ini
```
[MySQL]
mysql.max_persistent = 20
mysql.allow_persistent = On
mysql.default_port = 3306
mysql.default_host = localhost
mysql.trace_mode = Off
mysql.connect_timeout = 60
```

```
@code:parseconfig.py
@description:Parsing and updating the config file
import ConfigParser
config = ConfigParser.ConfigParser()
config.read('php.ini')
# Print config values
print config.get('MySQL', 'mysql.')
```

## 注意

本文针对 Python 2.X 系列编写，因为它仍然是所有平台上（包括所有 Linux 发行版、BSD 和 Mac OS X）最流行和默认的 Python 版本。


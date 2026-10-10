
TWD=`"/var/db/tripwire"`

其他赋值设置文件类，用于告诉 Tripwire 给定目录中驻留的文件类型。Tripwire 根据文件类型执行不同类型的检查。例如，下面这行设置了二进制文件的名称：

```
SEC_BIN     = $(ReadOnly) ;     # Binaries that should not change
```

随后的定义可以使用`*SEC_BIN*`来引用二进制文件。这些定义告诉 Tripwire 关于单个文件或整个目录的信息。例如，这些行告诉 Tripwire 如何处理其自身的二进制文件：

```
# Tripwire Binaries

(

  rulename = "Tripwire Binaries",

  severity = $(SIG_HI)

)
```

### 规则定义示例

```
$(TWIN) -> $(SEC_BIN)

$(TWIN)/triptwire -> $(SEC_BIN)

$(TWIN)/twdmin -> $(SEC_BIN)

$(TWIN)/twprint -> $(SEC_BIN)

}
```

该定义由两部分组成。第一部分由普通括号（`( )`）包围，包含规则名称和严重性级别的赋值。第二部分由花括号（`{ }`）包围，使用一种不寻常的赋值运算符（`->`）来告诉 Tripwire 如何处理特定的目录或文件。尽管本示例中未使用，但配置行前面可以加一个感叹号（`!`）来表示停止——Tripwire 不应检查指定子目录中的文件。你可以利用此功能将子目录排除在原本应被检查的目录树之外。

### 初始化与更新数据库 (Initializing and Updating the Database)

通过 FreeBSD 端口安装时，Tripwire 会自动初始化其数据库。如果你对该程序进行了大量更改，你可能会想要完全重新初始化它。如果是这样，你可以通过输入以下内容来实现：

```
/usr/local/sbin/tripwire --init
```

此命令运行 Tripwire 的整个初始化过程，在该过程中，它计算配置文件中指定的所有文件的各种校验和，并创建校验和数据库文件。为了完成这些任务，你必须输入站点口令和本地口令。

Tripwire 支持两种不同的更新操作。这些功能仅更新数据库文件，或者更新数据库文件和整个 Tripwire 配置。在更新或安装 FreeBSD 软件包、端口或受监控的配置文件之后，你可能需要仅更新数据库文件。为此，请键入以下命令：

```
/usr/local/sbin/tripwire --update
```

如果你更改了 Tripwire 配置本身，则需要使用另一个命令。此命令将文本模式的 `twcfg.txt` 和 `twpol.txt` 文件转换为它们的加密二进制形式。此命令还会更新配置文件本身的数据，就像单独使用 `--update` 选项一样。执行所有这些操作的命令是：

```
/usr/local/sbin/tripwire --update-policy /usr/local/etc/tripwire/twpol.txt
```

与初始化命令一样，你必须输入站点和本地口令才能使用此命令。不幸的是，如果检测到配置文件以外的文件有任何更改，仅使用此命令可能会失败；它拒绝更改校验和数据库文件。要覆盖此行为并强制 Tripwire 实施对数据库文件的更改，请添加 `--secure-mode low` 选项。

这三个命令预计都需要几分钟时间才能完成。

### 使用 Tripwire 检测入侵 (Using Tripwire to Detect Intrusions)

一旦配置了准确数据库的 Tripwire，你可以使用其 `--check` 选项将系统的当前状态与其数据库中记录的状态进行检查：

```
/usr/local/sbin/tripwire --check
```

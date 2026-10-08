
# 877 mp

# mpss.so.1 — 设置页面大小的共享对象

## 概要

```
/usr/lib/lp/locale/C/mpss.so.1
```

## 描述

使用 mpss.so.1 共享对象，通过 Solaris 环境变量，选择性地配置应用程序及其子进程的堆和栈页面大小。要启用 mpss.so.1，必须在环境变量中包含以下格式的 MPSS 设置：

## 注意事项

由于资源限制或对齐要求，设置首选页面大小并不保证获得相应的大小。

## 环境变量

```
MPSSHEAP=size
MPSTACK=size
```

MPSSHEAP 和 MPSTACK 指定了堆和栈的大小。大小可以使用 K、M、G 或 T 转换为 KB、MB、GB 或 TB。

MPSSCFILE 是包含以下格式或多个 MPSS 配置的文件：

```
exec-name:heap-size:stack-size
```

exec-name 指定应用程序或可执行文件的名称。它可以是全路径、基名或模式字符串。如果没有指定堆大小或栈大小，则不会设置相应的首选页面大小。MPSSCFILE 的优先级高于 MPSSHEAP 和 MPSTACK。

## 示例

以下示例使用 MPSSCFILE 配置首选页面大小。

```
example$ LD_PRELOAD=$LD_PRELOAD:mpss.so.1
example$ MPSSCFILE=mpsscfg
example$ export LD_PRELOAD MPSSCFILE
example$ cat $MPSSCFILE
foo*:512K:64K
example$
```

以下示例使用 MPSSHEAP 和 MPSSSTACK 配置首选页面大小。

以下 Bourne shell 命令为所有具有 MPSSHEAP 和 MPSSSTACK 环境变量的应用程序配置 512K 堆和 64K 栈的首选页面大小。

```
example$ LD_PRELOAD=$LD_PRELOAD:mpss.so.1
example$ MPSSHEAP=512K
example$ MPSSSTACK=64K
example$ export LD_PRELOAD MPSSHEAP MPSSSTACK
example$
```

应用程序启动后，可以使用 pmap（参见 proc(1)）查看配置的实际页面大小。

```
example$ foobar &
example$ pmap -s `pgrep foobar`
```

如果未配置所需的页面大小（在 pmap 输出中显示），可能是由于 MPSS 配置文件或环境变量存在错误。检查错误日志（默认为 /var/adm/messages）以获取错误。如果没有发现错误，可能是资源或对齐限制导致的。

MPSSCFILE 中的首选页面大小配置将覆盖 MPSSHEAP 和 MPSSSTACK。按照上一个示例中的命令操作，将为所有应用程序配置 512K 堆和 64K 栈的首选页面大小，但 ls 命令和所有以 ora 开头的应用程序除外。

```
example$ MPSSCFILE=mpsscfg2
example$ export MPSSCFILE
example$ cat $MPSSCFILE
ls::
ora*:4m:4m
example$
```

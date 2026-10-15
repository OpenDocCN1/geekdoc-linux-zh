
如果出现真正的内存短缺（即用于应用程序和内核的内存不足），扫描器再次被允许从应用程序夺取页面。默认情况下，优先级分页是禁用的。在 Solaris 7 之后的 Solaris 版本中，可能会默认启用。要使用优先级分页，你需要 Solaris 7、带有内核补丁 `105181-13` 的 Solaris 2.6，或者带有 `103640-25` 或更高版本的 Solaris 2.5.1。要启用优先级分页，请在 `/etc/system` 中设置以下内容：

```
* Enable Priority Paging
set priority_paging=1
```

在运行的 32 位系统上启用优先级分页，请使用 `adb` 设置以下内容：

```
# adb -kw /dev/ksym /dev/mem
lotsfree/D
lotsfree: 730 <- 打印 freesree 的值
cachefree/E 0t160 <- 在 2 倍 freesree 的值前插入 0t (十进制)
dyncachefree/W 0t160 <- 在 2 倍 freesree 的值前插入 0t (十进制)
```

```
cachefree: 1460
dyncachefree/D
dyncachefree: 1460
```

在运行的 64 位系统上启用优先级分页，请使用 `adb` 设置以下内容：

```
# adb -kw /dev/ksym /dev/mem

lotsfree/E

lotsfree: 730 <- 打印 freesree 的值

cachefree/E 0t160 <- 在 2 倍 freesree 的值前插入 0t (十进制)

dyncachefree/W 0t160 <- 在 2 倍 freesree 的值前插入 0t (十进制)

cachefree: 1460

dyncachefree/D

dyncachefree: 1460
```

将 `priority_paging=1` 设置在 `/etc/system` 中会将 `cachefree` 设置为 `lotsfree` 的两倍水位。优先级分页区分可执行文件和常规文件，取决于它们是否具有执行位。这种机制将内存映射到地址空间，但要确保常规文件不具有执行位。

在 Solaris 7 中，扩展的分页计数器允许我们看到正在发生的分页。现在可以通过 `memstat` 命令看到内存短缺与分页之间的差异。`memstat` 的输出与 `vmstat` 类似，带有额外的类型。

### 表 15-1 memstat 分页计数器

| 列 | 描述 |
| :--- | :--- |
| pi | 总换入 |
| po | 总换出 |
| fr | 总空闲页 |
| sr | 每秒扫描率 |
| epi | 可执行文件换入 |
| epf | 可执行文件空闲页 |
| api | 应用程序换入 |
| apo | 应用程序换出 |
| apf | 应用程序空闲页 |

```
# /read test6

# memstat 3

      paging          --executable -- anonymous -- cpu

memory free re po fr sr epi epf api apo fpi f fps us sy id

2080 0 749 521 828 0 264 0 0 512 549 749 0 2 1 7 92 0

1912 0 736 384 707 0 133 0 290 0 384 418 762 0 0 1 4 94 0

1768 0 738 426 610 0 123 0 0 318 0 426 434 738 0 42 14 82 0

1920 0 781 469 665 0 103 0 216 0 512 597 781 3 37 8 91 0

2048 0 754 514 786 0 195 0 152 0 512 597 754 2 56 1 8 91 0

2024 0 741 600 850 0 228 0 101 0 597 693 741 2 56 1 8 91 0

2064 1 757 426 589 0 143 0 0 72 8 426 498 749 0 18 1 7 92 0
```

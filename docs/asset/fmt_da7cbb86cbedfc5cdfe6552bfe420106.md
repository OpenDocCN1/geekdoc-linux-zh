
`bash` 命令 `pwd` 指定当前目录。

除了 `bash` 包含的版本外，`pwd` 还可以作为一个独立的命令单独用，通常文件名为 `/bin/pwd`。请注意，在某些情况下，这两个变体的 `pwd` 可能不会产生相同的结果。这是因为 `bash` 版本的 `pwd` 是基于相对路径的，而外部命令处理的是绝对值。指向目录的符号链接可以在某种程度上欺骗 `bash` 版本的 `pwd`。

## 示例

在以下示例中，`In` 创建了一个指向 `/tmp` 目录的符号链接。`cd` 切换到该目录。`bash` 认为该目录是当前目录，而 `/bin/pwd` 识别出 `/tmp` 实际上是当前目录。

```
user In -s /tmp symlink

user$ cd symlink

user$ pwd

(bash version of pwd)

/home/kofler/symlink

user$ /bin/pwd

(standalone pwd command)

/tmp
```

`pwgen [options] [n]`

来自同名软件包的 `pwgen` 生成一整列表随机但易于记忆的密码。其思路是用户选择其中一个密码，然后在别人从你肩膀看过去看到密码之前，使用 `Ctrl+L` 清除屏幕。与 `makepasswd` 生成的密码相比，`pwgen` 生成的密码随机性较低，因此安全性也较低，但它们对于许多用例来说仍然足够。

默认情况下，密码长度为8个字符。你可以通过指定可选参数 `n` 生成更长的密码。

- `-0` 密码中使用未使用数字。
- `-1` 仅提供 1 个密码而不是 100 个。
- `-B` 避免根据字体可能容易混淆的字母或数字，即 O 和 0 以及 l 和 1。这会降低密码的安全性。
- `-y` 在密码中也包含特殊字符。

## 示例

如示例所示，即使是默认设置生成的密码也绝非易事：

```
user pwgen

Ohshu3yo Ewaledoe OhCh2Zua Aili80oc Xu4iyix uag3Geeash2hu Eeth6mah

eM0Jio xiele60ob ob8Yah9 shaif0Ed uep8Eve lang3Eho thaiS7xa Sah3S5ee4

...
```

以下命令生成一个包含特殊字符的 80 字符密码：

```
root# pwgen -1 -y 80

AhB9eivjoo~s0go2ievaF7eePe6oyoo7C

...[i
```

## `qalc [expression]`

来自同名软件包的 `qalc` 计算一个表达式。为了避免特殊字符，必须用引号括表达式：

```
user$ qalc "(2+3)*5"

25

user$ qalc sqrt(16)

4

user$ qalc sin(45)

0.707106

user$ qalc log(2)

0.693147
```

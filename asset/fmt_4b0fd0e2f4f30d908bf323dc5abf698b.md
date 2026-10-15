
```
printf "%s\n" "Processing files for $COMPANY..."
```

这个脚本比位置参数版本短。脚本必须查找的是 `OPTSTRING` 中列出的、未被 `switch` 语句处理的合法开关。

作为一个特殊情况，如果通过 `getopts` 命令作为额外参数提供，`getopt` 可以处理变量而不是脚本参数。这可以用于使用特定参数测试开关。

## getopt 命令

`getopt` 命令让脚本编程变得稍微容易，但它并不遵循 Linux 开关标准。特别是，`getopt` 不允许双连横号长开关。

为了绕过这一点，`getopt` 让脚本编程变得稍微容易，它并不遵循 Linux 开关标准。特别是，`getopt` 不允许双连横号长开关。


972 wait
S
132

## Linux 技巧

pts/1

Ajay Kumar Tiwari

```
0:00 /bin/bash ./nice-test.sh
```

[Note: 第 6 列的值为 0 是 nice 值。]

现在，让我们使用不同的 nice 值执行相同的 shell 脚本，如下所示。

```
$ nice -10 ./nice-test.sh &
```

```
[1] 13016
```

```
$ ps axl | grep nice-test
```

```
0509 13016 12863 30 10 4236 968 wait
```

```
pts/1 0:00 /bin/bash ./nice-test.sh
```

SN

[Note: 第 6 列的值为 10 是 shell 脚本的 nice 值。]

如何为 shell 脚本分配高优先级？（降低 nice 值）

在下面的示例中，让我们将 nice 值 -10（负 10）分配给 nice-test.sh shell 脚本。

```
$ nice -10 ./nice-test.sh &
```

```
[1] 13021
```

```
$ nice: cannot set priority: Permission denied
```

注意：只有 root 用户才能设置负的 nice 值。请以 root 身份登录并尝试相同操作。请注意，下面的 nice 命令中 10 前面有两个破折号。

```
# nice -10 ./nice-test.sh &
```

```
[1] 13060
```

```
# ps axl | grep nice-test
```

```
40 13060 13024 10 -10 5388 964 wait
```

```
pts/1 0:00 /bin/bash ./nice-test.sh
```

133

S<

## Linux 技巧

Ajay Kumar Tiwari

[Note: 第 6 列的值为 -10 是 shell 脚本的 nice 值。]

### Hack 101. Renice 命令

Renice 会更改正在运行进程的调度优先级。

如何降低正在运行进程的优先级？（增加 nice）

在下面的示例中，一个现有的 shell 脚本以 nice 值为 10 运行。

（ps 输出中的第 6 列）

```
$ ps axl | grep nice-test
0509 13245 13216 30 10 5244 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
SN
```

要增加 nice 值（从而降低优先级），请按如下所示执行 renice 命令。

```
$ renice 16 -p 13245
13245: old priority 10, new priority 16
$ ps axl | grep nice-test
0509 13245 13216 36 16 5244 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
SN
```

[Note: 现在，nice-test.sh（PID 13245）的第 6 列显示新的 nice 值为 16。]

如何提高正在运行进程的优先级？（降低 nice）

在下面的示例中，一个现有的 shell 脚本以 nice 值为 10 运行。

134

## Linux 技巧

（ps 输出中的第 6 列）

Ajay Kumar Tiwari

```
$ ps axl | grep nice-test
0509 13254 13216 30 10 4412 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
SN
```

要提高优先级，请按如下所示给出较低的 nice 值。但是，只有 root 才能提高正在运行进程的优先级，否则您会收到以下错误消息。

```
$ renice 5 -p 13254
renice: 13254: setpriority: Permission denied
```

以 root 身份登录以提高正在运行进程的优先级

```
$ su -
# renice 5 -p 13254
13254: old priority 10, new priority 5
# ps axl | grep nice-test
0509 13254 13216 255 4412 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
SN
```

[Note: 第 6 列现在显示较低的 nice 值为 5（优先级提高）]

## Linux 技巧

Ajay Kumar Tiwari

## Linux 技巧

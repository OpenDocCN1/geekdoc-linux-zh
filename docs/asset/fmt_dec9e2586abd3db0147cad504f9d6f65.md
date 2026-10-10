
# 3398 | 第 14 章 系统管理工具

```bash
$ cat /etc/init/myapp.sh
function killapp
{
  # 如果我们进入这里，说明应用程序拒绝关闭。
  kill -9 'cat /var/run/myapp.pid'
}
case $1 in
start)
  echo "Starting myapp..."
  /usr/local/bin/myapp &
  echo $! > /var/run/myapp.pid
  ;
stop)
  echo "Stopping myapp..."
  timeout -s 15 -k 10 20 /usr/local/bin/stop.myapp
  res=$?
  echo "myapp returned with exit code $res" > /var/log/myapp.log
  case $res in
    0) echo "NOTE: myapp stopped by itself.";
    124) echo "NOTE: myapp timed out when stopping.";
      killapp;
    137) echo "NOTE: myapp was killed when timing out.";
      killapp;
    *) echo "Note: myapp exited with return code $res";
  esac
  rm -f /var/run/myapp.pid
  )
*)
  echo "Usage: $(basename $0) start | stop"
  exit 2
esac
```

```bash
$ cat /usr/local/bin/stop.myapp
#!/bin/bash
trap may_die 1 3 9 15

function may_die {
  SLEEP=`expr $RANDOM % 20`
  echo "Sleeping for $SLEEP seconds (but you don't know that)"
  sleep $SLEEP && exit 10
}

TIME=`expr $RANDOM % 50`
echo "STOPPING MYAPP. (likely to take $TIME seconds, but you don't know that!)"
for i in `seq 1 $TIME`;
do
  echo -en "."
  sleep 1
done

exit 20
$
```

可在 Wins.com 下载。

18 秒的关闭不受 `timeout` 影响：

```bash
$ ./myapp.sh stop
Stopping myapp...
STOPPING MYAPP. (likely to take 18 seconds, but you don't know that!)
..................Note: myapp exited with return code 20
```

44 秒的关闭注定超时。因为进一步关闭超过了允许的秒数，关闭程序会被杀死：

```bash
$ ./myapp.sh stop
Stopping myapp...
STOPPING MYAPP. (likely to take 44 seconds, but you don't know that!)
..................Terminated
Sleeping for 11 seconds (but you don't know that)
./myapp.sh line 3: 6071 Killed timeout -s 15 -k 10 20 /usr/local/bin/stop.myapp
NOTE: myapp was killed when timing out.
```

超时后较短的退出仍被归类为超时，但它免于被杀死。

```bash
$ ./myapp.sh stop
Stopping myapp...
STOPPING MYAPP. (likely to take 26 seconds, but you don't know that!)
..................Terminated
Sleeping for 2 seconds (but you don't know that)
NOTE: myapp timed out when stopping.
$
```

## 网络超时

上一节给出的示例是一个依赖于完全外部因素的系统或进程，例如从远程服务器下载。如果该服务器或到它的网络出现问题，脚本本身无法处理，但可以使用 `timeout` 来管理解决方案。例如，如果预计传输时间为 10 秒，如果传输在了一分钟后仍未完成，可以使用 `timeout` 来终止该传输。

```bash
$ cat downloader.sh
#!/bin/bash

for file in file1.zip file2.zip file3.zip
do
  timeout -n 9 60 wget http://unreliable.example.com/$file
  if [ $? -ne 0 ]; then
    echo "An error occurred when downloading $file"
  fi
done
```

```bash
$ ./downloader.sh
Resolving unreliable.example.com...192.0.32.10
Connecting to unreliable.example.com[192.0.32.10... connected.
HTTP request sent, awaiting response...200 OK
Length: 84263304 (80M) Saving to 'unreliable.example.com/file1.zip'
100%=84263304 (80M) 0s
Resolving unreliable.example.com...192.0.32.10
Connecting to unreliable.example.com[192.0.32.10... connected.
HTTP request sent, awaiting response...200 OK
Length: 13396910 (39M) Saving to 'unreliable.example.com/file2.zip'
59%=24529715 (36.9M)
Resolving unreliable.example.com...192.0.32.10
Connecting to unreliable.example.com[192.0.32.10... connected.
HTTP request sent, awaiting response...200 OK
Length: 70108444 (669M) Saving to 'unreliable.example.com/file3.zip'
17%=12183142 (22.0M)
downloader.sh: line 3: 348 Killed timeout -s 9 60 http://unreliable.example.com/$file
an error occurred when downloading file.zip
$
```

## uname

`uname` 与 `hostname` 相关，但它更灵活。在 x86 架构上，它发现的信息比其设计的硬件要少；SunFire E25k 报告的 `uname -i` 为 SUNW，Enterprise-142900-02，而 T5240 报告的 `uname -i` 为 Generic。通过选项，它可以报告主机名 (-n)、内核版本 (-r) 和版本 (-v)、CPU 架构 (-m)、处理器 (-i) 以及硬件平台 (-a)。这些结合 `-a` 选项几乎等同于 `uname -all`。

`uname` 是脚本确定其运行环境的有用词。此片段定义了 CPU 的能力并相应报告。本章前面的 `dirname` 也使用 `uname` 来确定运行的操作系统，并对包系统做了大致的假设。

```bash
$ cat uname.sh
#!/bin/sh
case $(uname -m) in
  amd64|x86_64) bits=64 ;;
  i386|i586|i686) bits=32 ;;
  *) bits=unknown ;;
esac
echo "You have a $(bits)-bit machine."
```

```bash
$ ./uname.sh
You have a 64-bit machine.
$
```

了解 `uname` 的预期预期，表 14-1 展示了来自不同操作系统和架构的示例。前三个是 Linux 的不同发行版，接两个是 Solaris SPARC，下一个是 Solaris x，最后一个是 OpenBSD 服务器。

### 表 14-1：不同操作系统的 uname 输出

| OS | UNAME-S | UNAME-N | UNAME-R | UNAME-M |
|---|---|---|---|---|
| RedHat 6 | Linux | hattie | 2.6.32-71.el6.i686 | i686 |
| Debian 5 | Linux | goldie | 2.6.32-5-amd64 | x86_64 |
| Ubuntu 10.10 | Linux | elvis | 2.6.35-25-generic | x86_64 |
| Solaris 10 | SunOS | db9 | Generic_142900-02 | sun4u |

## uu

LibreOffice 文档不可管理的二进制文件被编码为可打印（尽管人类不可读！）的 7 位文本。这被附加到电子邮件正文中，以便方便地传输给接收者。在这里，我通过显示文档消息（“这里”）向自己发送文档。

## 402 | 第 14 章 系统管理工具

这是您需要的文档。此致，Steve") 并且在子 shell 中运行 `uuencode`，其输出将作为单个文本流通过管道传递给 `mailx` 命令。

```bash
$sender$ ( echo "Here is the document you wanted."; \
> echo "Regards, Steve." | \
> uuencode sample.odt mydocument.odt ) | \
> mailx -s "Document attached" steve@steve-parser.org\nsender$
```

![](img/5be99b1df3e454de85e6ef3c64fc3870_437_0.png)

如果本地机器已正确配置以发送电子邮件，则此消息将发送给命令中指定的收件者。由于电子邮件的性质，只要语法正确，`mailx` 命令就会返回成功；它无法检测电子邮件投递过程中的任何问题。您需要自行检查。收到的电子邮件如图 14-6 所示。

![](img/5be99b1df3e454de85e6ef3c64fc3870_437_1.png)

# XARGS

当调用的命令带有许多参数（通常是文件名）时，内核必须将这些数据存放在某处供命令引用。有时（通常当使用 `find` 命令遍历大型文件系统时），此列表的长度超过了内核的限制。这会导致“rm: Argument list too long”（参数列表过长）的消息。许多人使用这种方法并知道解决方法是使用 `xargs`，但并不是每个人都理解它的原理，这可能会产生许多重大影响。

```bash
$ rm `find -name *.core** -print'
bash: /bin/rm: Argument list too long
$ find -name *.core** -print0 | xargs -0 rm
$
```

为了解决这个问题，`xargs` 将读取其标准输入（标准输入没有这种限制），并将这些内容以可管理的分块传递给被要求传递的命令。这个简单的 `listfiles` 脚本展示了这种操作对正在运行命令的影响。在这里，`-L 3` 选项 `xargs` 将输入拆分为每次调用三个文件。这并不是大家认为 `xargs` 的工作方式，结果可能会令人意料。

```bash
$ cat listfiles
#!/bin/bash
echo "$Listfiles (PID $$) was called with $# arguments:"
while [ -a $1 ]
do
  echo "$($i): $((i))"\n    shift
done
```

![](img/5be99b1df3e454de85e6ef3c64fc3870_438_0.png)

```bash
$ find . -print
./etc
./etc/hosts
./etc/config.txt
./bin
./bin/ls
./sh
./listfiles
$ find -print | xargs -L 3 ./listfiles
Listfiles (PID 17088) was called with 3 arguments:
1:
2: ./etc
3: ./etc/hosts
Listfiles (PID 17089) was called with 3 arguments:
1: ./etc/config.txt
2: ./bin
3: ./bin/ls
Listfiles (PID 17090) was called with 2 arguments:
1: ./sh
2: ./listfiles
$
```

`find` 命令产生的前三个结果作为三个参数传递给 `listfiles`：

1. `./etc`
2. `./etc`
3. `./etc/hosts`

然后，接下来的三个传递给了另一个 `listfiles` 实例，这显然是一个不同的实例，因为它的 PID 不同。最后只剩下两个文件，因此它们被传递给 `listfiles` 的最后一次。

这一切都很正常，直到文件名开始包含奇怪字符，比如无无空格符号。在目录中添加 `My Photos` 和 `My Documents` 文件夹会让 `xargs` 感到非常困惑。第一个实例调用时带有三个参数：

1. `/My Photos`
2. `/My Photos\DCIM0001.jpg`
3. 

然而，它将这些解释为五个不同的单词：

1. `/My`
2. `/My`
3. `Photos`
4. `/My`
5. `Photos\DCIM0001.jpg`

在这些中，只有第一个是实际的文件（实际上是一个目录）。其他四个未能通过 `[-a "1"]` 测试，因此完全没有显示它们的输出。困惑一直持续，直到回到完全没有空格的路径。

```bash
$ find -print
/My Photos
/My Photos\DCIM0001.jpg
/My Photos\DCIM0002.jpg
/My Documents
/My Documents/doc1.doc
/My Documents/cv.odt
/etc
/etc/hosts
/etc/config.txt
/bin
/bin/ls
/sh
/listfiles
$ find -print | xargs -L 3 ./listfiles
Listfiles (PID 1706) was called with 5 arguments:
1:
Listfiles (ID 1707) was called with 6 arguments:
Listfiles (ID 1708) was called with 4 arguments:
Listfiles (ID 1709) was called with 3 arguments:
1: /etc/config.txt
2: /bin
3: /bin/ls
Listfiles (PID 1710) was called with 2 arguments:
1: /sh
2: ./listfiles
$
```

为了解决这个问题，`xargs` 将读取其标准输入（标准输入没有这种限制），并将这些以可管理的分块传递给被要求传递的命令。这个简单的 `listfiles` 脚本展示了这种操作对正在运行命令的影响。在这里，`-L 3` 选项 `xargs` 将输入拆分为每次调用三个文件。这并不是大家认为 `xargs` 的工作方式，结果可能会令人意料。

```bash
$ find . -print
./etc
./etc/hosts
./etc/config.txt
./bin
./bin/ls
./sh
./listfiles
$ find -print | xargs -L 3 ./listfiles
Listfiles (PID 17088) was called with 3 arguments:
1:
2: ./etc
3: ./etc/hosts
Listfiles (PID 17089) was called with 3 arguments:
1: ./etc/config.txt
2: ./bin
3: ./bin/ls
Listfiles (PID 17090) was called with 2 arguments:
1: ./sh
2: ./listfiles
$
```

`find` 命令产生的前三个结果作为三个参数传递给 `listfiles`：

1. `./etc`
2. `./etc`
3. `./etc/hosts`

然后，接下来的三个传递给了另一个 `listfiles` 实例，这显然是一个不同的实例，因为它的 PID 不同。最后只剩下两个文件，因此它们被传递给 `listfiles` 的最后一次。

这一切都很正常，直到文件名开始包含奇怪字符，比如无无空格符号。在目录中添加 `My Photos` 和 `My Documents` 文件夹会让 `xargs` 感到非常困惑。第一个实例调用时带有三个参数：

1. `/My Photos`
2. `/My Photos\DCIM0001.jpg`
3. 

然而，它将这些解释为五个不同的单词：



## 6.2.8. key 语句的定义与用法

key 语句定义了用于 TSIG 的共享秘密密钥，详见第 4.4 节。

key 语句可以出现在配置文件的顶层，也可以出现在 view（视图）语句内部。定义在顶层中的密钥可以在所有视图中使用。打算用于 controls（控制）语句（见第 6.2.4 节）的密钥必须在顶层定义。

key_id（也称为密钥名称）是一个唯一标识密钥的域名名。它可以用于“server”语句，使发送到服务器的请求使用此密钥进行签名；或者用于地址匹配列表（address match lists），以验证传入的请求是否已使用该名称、算法和密钥进行了签名。

algorithm_id 是一个指定安全/身份验证算法的字符串。目前 TSIG 认证支持的算法是 hmac-md5。secret_string 是算法使用的密钥，被视为一个 base64 编码字符串。

## 6.2.9. logging 语句的语法

```
logging {
  channel channel_name {
    file path name
    [ versions ( number | unlimited ) ]
    [ size size spec ]
    syslog syslog_facility
    stderr
    null);
    [ severity (critical | error | warning | notice | 
      info | debug [ level ] | dynamic ); ]
    [ print-category yes or no; ]
    [ print-severity yes or no; ]
    [ print-time yes or no; ]
  }
  [ category category_name {
    channel_name ; [ ... ]
  };
}
```

## 6.2.10. logging 语句的定义与用法

logging 语句为命名服务器配置多种日志选项。其 channel（通道）部分将输出方法、格式选项和级别与一个名称关联，然后可以配合 category（类别）部分来选择如何记录不同类的消息。

仅使用 logging 语句即可定义任意数量通道和类别。如果没有 logging 语句，日志配置将如下：

```
logging {
  category "unmatched" { "null"; };
  category "default" { "default_syslog"; "default_debug"; };
}
```

在 BIND 9 中，日志配置只有在整个配置文件解析完成后才会建立。在 BIND 8 中，一旦解析到 logging 语句就会建立。当服务器启动时，所有关于配置文件语法错误的日志消息都将进入默认通道，或者如果指定了 -g 选项，则进入标准错误（stderr）。

### 6.2.10.1. channel 子句

所有日志输出都指向一个或多个通道；你可以根据需要创建任意多个通道。

每个通道定义必须包含一个目标子句（destination clause），说明为该通道选择的消息发送到文件、特定的 syslog 设施、标准错误还是被丢弃。你可以可选地限制通道接受的严重性级别（默认为 info），以及是否包含命名的时间戳、类别名称和/或严重性级别（默认是不包含任何内容）。

null 目标子句会导致发送到该通道的所有消息被丢弃；在这种情况下，该通道的其他选项将毫无意义。

file 目标子句将通道重定向到磁盘文件。它可以限制文件允许增长的大小，以及每次打开文件时将保存多少版本的备份。

如果你使用了 versions log file 选项，named 将在打开文件时通过重命名来保留相应数量的备份版本。例如，如果你选择保留 3 个旧版本的 lamers.log，那么 lamers.log.1 将重命名为 lamers.log.2，lamers.log.0 重命名为 lamers.log.1，而 lamers.log 重命名为 lamers.log.0。你可以指定 unlimited 来限制版本数量。如果日志文件关联了 size 选项，则只有当打开的文件超过指定大小时才会进行重命名。默认不保留备份版本；任何现有的日志文件仅会被追加。

如果文件没有 versions 选项，则除非某些带外机制移除或截断日志使其小于最大大小，否则不会有更多数据写入日志。默认行为是不限制文件大小。

文件的 size 选项用于限制日志增长。如果文件超过了该大小，除非关联了 versions 选项，否则 named 将停止写入该文件。如果保留了备份版本，文件将如上述描述那样进行滚动并开始一个新文件。

size 和 versions 选项的示例用法：

```
channel "an_example_channel" {
    file "example.log" versions 3 20m;
    print-time yes;
    print-category yes;
}
```

syslog 子句将通道重定向到系统日志。其参数是 syslog 页面中描述的 syslog 设施。syslog 如何处理发送给它的消息见 syslog.conf 页面。如果你的系统使用的旧版本 syslog 导致 open() 仅接受两个参数，则此子句将被静默忽略。

severity 子句的作用类似于 syslog 的“优先级（priorities）”，只不过当你直接写入文件而不是使用 syslog 时，也可以使用它们。不符合给定严重性级别的消息将不会被通道选择；较高严重性级别的消息将被接受。

如果你正在使用 syslog，则 syslog.conf 中的优先级将透传。例如，将通道和级别定义为 daemon 和 debug 且仅通过 syslog 记录 daemon 消息，会导致 info 和 notice 消息被丢弃。如果情况反过来，即 named 消息仅为 warning 或更高级别，则 syslog 将打印所有消息。

stderr 子句将通道重定向到标准错误。这在服务器作为前台进程运行时调试配置时非常有用。当全局调试级别大于0时，服务器处于调试模式并提供详细的调试信息。提供特定严重性许多别的通道，例如：

```
channel "specific_level" {
    file "foo";
    severity debug 3;
}
```

将在调试模式下获得级别 3 或以下的调试输出，无论全局调试级别如何。dynamic 严重性的通道使用全局调试级别来确定打印哪些消息。

如果开启了 print-time，将记录日期时间。对于 syslog 通道可以指定 print-time，但这没有意义，因为 syslog 也会打印日期时间。如果请求了 print-category，将记录消息的类别。如果开启了 print-severity，将记录消息的严重性级别。print- 选项可以任意组合，并将始终按以下顺序打印：时间、类别、严重性。这里是开启所有三个 print 选项的示例：

```
28-Feb-2000 15:05:32.863 general: notice: running
```

定义了四个用于 named 默认日志的通道如下。其细节见 6.2.10.2 节。

```
channel "default_syslog" {
    syslog daemon;\                   发送到 syslog 的 daemon 设施
    severity info;\                 // 仅发送 info 及其更高优先级信息
}
```

```
channel "default_debug" {
    file "named.run";            // 写入工作目录下的 named.run
                                // 注意：如果启动服务器时带有 '-d' 选项
                                // 则使用 stderr 代替 "named.run"
    severity dynamic;\            // 当前调试级别
}
```

```
channel "default_stderr" {
    stderr;                        // 写入 stderr
    severity info;\                 // 仅发送 info 及其更高优先级信息
}
```

```
channel "null" {
    null;                          // 丢弃发送到此通道的所有内容
}
```

default_debug 具有特殊属性，当服务器调试级别不为零时它会产生输出。它通常写入名为 named.run 的文件。


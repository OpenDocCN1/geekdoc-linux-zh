
# `spd-say` 命令

`spd-say`向处理语音的`speech-dispatcher`进程发送文本到语音的输出请求，该进程处理请求并在理想情况下将结果输出到音频系统。

## 语法

```
$ spd-say [options] "some text"
```

## 选项

```
-r, --rate
       设置语速（范围：-100 到 +100，默认：0）

-p, --pitch
       设置音调（范围：-100 到 +100，默认：0）

-i, --volume
       设置音量（强度）（范围：-100 到 +100，默认：0）

-o, --output-module
       设置输出模块

-l, --language
       设置语言（ISO 代码）

-t, --voice-type
       设置首选语音类型（male1, male2, male3, female1, female2, female3, child_male, child_female）

-m, --punctuation-mode
       设置标点模式（none, some, all）

-s, --spelling
       拼读消息

-x, --ssml
       开启 SSML 模式（默认：关闭）

-e, --pipe-mode
       从 stdin 管道传输到 stdout，并加上 Speech Dispatcher

-P, --priority
       设置消息优先级（important, message, text, notification, progress；默认：text）

-N, --application-name
       设置用于建立连接的应用程序名称为指定字符串值（默认：spd-say）

-n, --connection-name
       设置用于建立连接的连接名称为指定字符串值（默认：main）

-w, --wait
       等待消息被朗读或丢弃

-S, --stop
       停止朗读 Speech Dispatcher 中正在朗读的消息

-C, --cancel
       取消 Speech Dispatcher 中的所有消息

-v, --version
       打印版本和版权信息

-h, --help
       打印此帮助信息
```

## 示例

1. 播放给定的文本作为声音。

```
$ spd-say "Hello"
```

> 播放“你好”声音。

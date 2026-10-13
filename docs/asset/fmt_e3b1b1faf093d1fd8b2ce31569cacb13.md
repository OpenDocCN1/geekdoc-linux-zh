
默认情况下，`at`任务的结果会通过电子邮件发送给调度任务的人。以下屏幕显示了包含之前示例结果的收件箱。

| Mailbox Message | Subject | Date and Time | Size |
| :--- | :--- | :--- | :--- |
| winsor@castle | Output from "at" job | Fri Aug 28 12:15 | 479 |
| winsor@castle | Output from "at" job | Fri Aug 28 12:30 | 479 |
| winsor@castle | Output from "at" job | Fri Aug 28 12:30 | 548 |

你可以从终端使用以下序列。

```
$ -m 0730 tomorrow

at> sort < file > outfile

at> Control-D <EOT>

commands will be executed using /bin/sh

job 904380100.a at Sat Aug 29 07:30:00 1998

$
```

下面的序列演示了将标准错误重定向到管道。这在命令处理过程中非常有用。注意重定向的输出是有意义的。

```
$ now + 5 min

at> << !! file1 2>&1 > outfile | mailx mygroup!

at> Control-D <EOT>

commands will be executed using /bin/sh

job 904280212.a at Fri Aug 28 12:56:52 1998

$ -1

90437000.a Sat Aug 29 07:30:00 1998

904280100.a Fri Aug 28 12:56:52 1998

$
```

(注：由于提供的待翻译文本存在大量重复和混乱，我已根据逻辑对核心内容部分进行规范翻译)

# 75

904323600.a Sat Aug 29 01:00:00 1998
904460400.a Sun Aug 30 15:00:00 1998

以下示例显示了当以超级用户身份执行 `atq` 命令时的输出。

```
castle% su

Password:

castle# atq

Rank  Execution Date      Owner   Job       Queue   Job Name

1st   Aug 28, 1998 18:00  root    90291200.a  a       tryit

2nd   Aug 28, 1998 17:00  winsor 90294800.a  a       tryit

3rd   Aug 28, 1998 18:00  root    90298400.a  a       tryit

4th   Aug 28, 1998 19:00  ray     904302000.a  a       tryit

5th   Aug 28, 1998 21:00  ray     904309200.a  a       tryit

6th   Aug 29, 1998 01:00  winsor 904323600.a  a       tryit

7th   Aug 29, 1998 07:30  winsor 904347000.a  a       stdin

8th   Aug 30, 1998 15:00  winsor 904460400.a  a       tryit
```

以下示例显示了按时间排序的相同示例。

```
castle# atq -c

Rank  Execution Date      Owner   Job       Queue   Job Name

1st   Aug 29, 1998 07:30  winsor 904347000.a  a       stdin

2nd   Aug 28, 1998 17:00  winsor 904948000.a  a       tryit

3rd   Aug 29, 1998 01:00  winsor 904323600.a  a       tryit

4th   Aug 30, 1998 15:00  winsor 904460400.a  a       tryit

5th   Aug 28, 1998 16:00  root    90291200.a  a       tryit

6th   Aug 28, 1998 18:00  root    902984000.a  a       tryit

7th   Aug 28, 1998 19:00  ray     904302000.a  a       tryit

8th   Aug 28, 1998 21:00  ray     904309200.a  a       tryit
```

以下示例显示了 `atq -n` 命令返回的值。此选项列出了队列中的项目数量。

```
castle# atq -n

castle#nnThe following示例仅列出了由用户 ray 轮队的任务。

castle# atq ray

Rank  Execution Date      Owner   Job       Queue   Job Name

1st   Aug 28, 1998 19:00  ray     904302000.a  a       tryit

2nd   Aug 28, 1998 21:00  ray     904309200.a  a       tryit

castle#
```

## 文件

```
/var/spool/cron/atjobs

任务的池区。
```

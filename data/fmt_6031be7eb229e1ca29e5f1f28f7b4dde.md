
```
1       0          0        OK        120      493K       0       0  *file*

3  225562  11305229K    634958  17348085K     592       0  local

4     219       9772K      2296     12902K       0       0  smtp

5  368708  9017330K    290406  15666563K    3488       0  esmtp

7       1         1K        37       6910K       0       0  relay

T  594490  20332332K    959232  33221188K    4080       0
```

第一行给出统计开始的时间和日期。输出按邮件程序分隔，可用作确定电子邮件负载的辅助手段。

## 别名

别名允许 `Sendmail` 执行以下任务：

- 将邮件发送到程序或 shell 脚本。
- 将邮件追加到文件。
- 分发到列表。
- 允许单个用户名接收多个用户名的邮件。

`/etc/aliases` 文件是一个文本文件，其中包含由本地账户名组成的行，后跟第一个字段中的冒号，第二个字段中的别名。以空格或制表符开头的行被视为其上方行的组成部分。以 `#` 开头的行是注释，空行将被忽略。所有其他行都被视为别名行，必须具有以下结构：

```
AccountName:      alias
```

`AccountName` 必须是本地用户名。第二字段 `alias` 被定义为用户名（本地或远程），除非它具有表 9.5 中描述的特征。出于性能考虑，`/etc/aliases` 文件会被转换为 `aliases.db` 或 `aliases.dir/aliases.pag` 格式。转换在 `Sendmail` 启动时或执行 `newaliases` 命令时进行。

![](img/415c89a1ede71e11e5040a0038b6916c_389_0.png)

| 表 9.5 | 特殊别名情况 |
|---|---|
| 情况 | 解释 |
| `/` | 追加到文件 |
| `|` | 使用 `prog` 代理传递到程序 |
| `\\` | 抑制所有别名并本地投递 |
| `:include:` | 特殊情况，允许外部文件包含收件人列表 |

列表 9.7 包含一个示例 `/etc/aliases` 文件。第一行是本地账户别名为远程账户的示例。第 2 行和第 3 行将本地用户名别名为不同的本地用户名。第 4 行包含 `:include:` 表达式。`:include:` 表达式必须后跟收件人列表的完整路径名。`:include:` 语句引用的列表包含收件人地址行（一行中多个收件人需要在收件人之间用逗号分隔）、程序名、文件名或额外的 `:include:` 列表。第 5 行是一个列表。发送给 `dsw` 的电子邮件将传递给 `dweb`、`dws` 和 `rand`。第 6 行将邮件追加到文件。最后两行将邮件传递给相关程序。需要选项的程序需要使用引号。`Sendmail` 需要两个别名：`MAILER-DAEMON` 和 `postmaster`。

### 列表 9.7 示例 `/etc/aliases` 文件

```
baude:            baude@research.business.com

bob:              bill

bcummings:        cummings

bo_list:          :include:/tools/lists/lists/order_list

dsw:              dweb,dws,rand

joe:              /home/machine/joe/mailalways

rot:              /tools/lists/process_this_mail

spyd:             |"/tools/lists/moreprocess -q -t"

MAILER-DAEMON:    postmaster

Postmaster:       root
```

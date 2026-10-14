
```
while (expression)
  command(s)
end
```

以下示例执行了 HP-UX 9.x 版本的 `netstat`，并打印一次标题和多次 `lan0` 状态：

```csh
#!/usr/bin/csh
# 每隔指定间隔运行 netstat 的程序
# 用法: netcheck interval

set limit=9                # 设置运行 netstat 的次数限制

echo ""
netstat -i | grep Name      # 带标题的 netstat 行
set count=0
while ($count<$limit)      # 如果未达到限制
                             # 则运行 netstat
  netstat -i | grep lan0
  sleep 1                  # 按命令行指定的
                             # 间隔睡眠
  @ count++               # 计数自增
end
echo "count has reached $limit, run netcheck again to see lan0 status"
```

以下是程序的运行示例：

```text
syslog 1: netcheck 2
Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Coll
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
count has reached 9, run netcheck again to see lan0 status
```

该程序通过以下方式增加表达式的值：

```
@count++
```

如果表达式为真，则将执行命令。`@count++` 是如下形式的赋值运算符：

```
@ variable_name operator expression
```

在这种情况下，变量首先被赋值为 `"="`, 随后自动自增 `++`。可以对表 7-7 所示的变量上多种操作。

## 表格 7-7 赋值运算符

| 操作 | 符号 | count = 100 的示例 | 结果 |
| --- | --- | --- | --- |
| 存储值 | = | `@count=100` | 100 |
| 自动自增 | ++ | `@count++` | 101 |
| 自动自减 | -- | `@count--` | 99 |
| 加值 | += | `@count+=50` | 150 |
| 减值 | - | `@count-=50` | 50 |
| 乘法值 | *= | `@count*=2` | 200 |
| 除以值 | /= | `@count/2` | 50 |

如果表达式为真，则将执行命令。`@count++` 赋值运算符的形式为：

```
@ variable_name operator expression
```

在这种情况下，变量首先被赋值为 `"="`, 随后自动自增 `++`。可以对表 7-7 所示的变量执行多种操作。

## 7-7

| 操作 | 符号 | count = 100 的示例 | 结果 |
| --- | --- | --- | --- |
| 存储值 | = | `@count=100` | 100 |
| 自动自增 | ++ | `@count++` | 101 |
| 自动自减 | -- | `@count--` | 99 |
| 加值 | += | `@count+=50` | 150 |
| 减值 | - | `@count-=50` | 50 |
| 乘法值 | *= | `@count*=2` | 200 |
| 除以值 | /= | `@count/2` | 50 |

如果表达式为真，则将执行命令。`@count++` 赋值运算符的形式为：

```
@ variable_name operator expression
```

在这种情况下，变量首先被赋值为 `"="`, 随后自动自增 `++`。可以对表 7-7 所示的变量执行多种操作。

C shell 支持多种实现循环的技术，包括：

- 1) `foreach` 循环，它接收一个项目列表，并对列表中的每个项目执行一次循环中的命令。
- 2) `while` 循环，如果命令执行成功（例如 `test` 命令），则执行循环中的命令。

`foreach` 循环的格式如下：

```
foreach name (list)
command(s)
end
```

以下示例使用 `foreach` 循环来测试 `/etc/hosts` 文件中的系统是否已连接到本地主机：

```csh
#!/usr/bin/csh
#Program name: csh_hostck

#此程序将测试你的 /etc/hosts 文件列出的网络中所有其他主机的连通性。

# 它使用 awk 命令从 hosts 文件获取主机
# 并使用 ping 命令检查连通性。

# 注意我们使用了 /usr/bin/echo，因为 csh echo 不支持
# 像 \t 或 \c 这样的转义字符，这些字符在
# foreach 循环中被使用。

# /etc/hosts 中任何以数字开头的行代表
# 一个主机条目。其他内容都是注释或空行。

# 找到 /etc/hosts 中所有以数字开头的行，
# 并打印第二个字段（主机名）。

set hosts='awk '^[1-9]/ { print $2 }' /etc/hosts'
# 外部反反引号，内部单引号
/usr/bin/echo "Remote host connection status"

foreach sys ($hosts)
  /usr/bin/echo "$sys - \c"
  # 发送一个 64 字节的数据包，并查找
  # 输出中的 "1 packets received" 消息
  # 表示成功。

  ping $sys 64 1 | grep "1 packets received" > /dev/null
  if ($status == 0) then
    echo "OK"
  else
    echo "DID NOT RESPOND"
  endif
end
```

那行看起来奇怪的 `awk` 命令用于从 `/etc/hosts` 文件获取远程主机的名称。`foreach` 循环获取列表中的所有项目（在此例中为 `hosts`）并检查每个的状态。

你可以使用 `while` 循环执行指定次数的命令。`while` 循环的格式如下：

```
while (expression)
  command(s)
end
```

以下示例执行了 HP-UX 9.x 版本的 `netstat`，并打印一次标题和多次 `lan0` 状态：

```csh
#!/usr/bin/csh
# 每隔指定间隔运行 netstat 的程序
# 用法: netcheck interval

set limit=9                # 设置运行 netstat 的次数限制

echo ""
netstat -i | grep Name      # 带标题的 netstat 行
set count=0
while ($count<$limit)      # 如果未达到限制
                             # 则运行 netstat
  netstat -i | grep lan0
  sleep 1                  # 按命令行指定的
                             # 间隔睡眠
  @ count++               # 计数自增
end
echo "count has reached $limit, run netcheck again to see lan0 status"
```

以下是程序的运行示例：

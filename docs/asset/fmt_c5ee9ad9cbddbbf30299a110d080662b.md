
# journalctl

## 示例

`journalctl --boots -head`

-12 eb35cbddda4f84da7bdbc71fb94e61 Sun 2024-08-17 15:33:30 EDT...

-11 534713a5a6c54c1bc5b3d056487a16db Wed 2024-08-20 06:45:15 EDT...

-10 64147da7154b4499a312a88a96c19bd Fri 2014-08-29 23:14:38 EDT...

`journalctl -b eb3cd5dba8f4f8da7bdbc71fb94e6e1l`

`journalctl -k`

在这些示例中，`journalctl` 命令允许你过滤和查看消息。要查看特定启动的消息，请使用带有启动单元 ID 的 `-b` 标志。要仅查看内核消息，使用 `-k`。以下是一些示例：

`journalctl --unit=sshd`

`journalctl --priority=err`

`journalctl -a`

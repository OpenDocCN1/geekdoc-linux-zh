
# 第 8 章：备份与可移动介质

## 使用 growisofs 制作和刻录 DVD

使用 `growisofs` 命令，你可以将收集文件并为 ISO 镜像（`mkisos`）以及将该镜像刻录到 DVD（`cdrecord`）这两个步骤合并为一个。除了节省一个步骤外，`growisofs` 命令还提供了默认保持会话开启直到你将其关闭的优势，因此你不需要对多刻会话进行任何特殊操作。

以下是一个用于多刻会话的 `growisofs` 命令示例：

```bash
# growisofs -Z /dev/dvd -R j /home/chris    主并刻录到 DVD
# growisofs -Z /dev/dvd -R j /home/francois  添加到刻录
# growisofs -M /dev/dvd=/zero                关闭刻录
```

如果你想在创建 ISO 镜像时添加选项，可以简单地在命令行中添加 `mkisos` 选项。（例如，参见上述示例中是如何添加 `-R` 和 `-J` 选项的。）

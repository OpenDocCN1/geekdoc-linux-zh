
以下示例显示了 `convert` 的几种用法：

- `-colors 256 input.jpg output.jpg`
- `-colorspace Gray input.jpg output.jpg`
- `-compress JPEG quality:80 input.jpg output.jpg`
- `-contrast 50% input.jpg output.jpg`
- `-crop 50x50+100+100 input.jpg output.jpg`
- `-filter Box input.jpg output.jpg`
- `-gaussian-blur 0x1 input.jpg output.jpg`
- `-normalize input.jpg output.jpg`
- `-quality 85 input.jpg output.jpg`
- `-resize 800x600 input.jpg output.jpg`
- `-rotate 90 input.jpg output.jpg`
- `-trim input.jpg output.jpg`

使用 `convert` 的示例：

- `-trim input.jpg output.jpg`
- `-rotate 90 input.jpg output.jpg`
- `-quality 90% input.jpg output.jpg`
- `-resize 500x500 input.jpg output.jpg`
- `-normalize input.jpg output.jpg`
- `-gaussian-blur 0x2 input.jpg output.jpg`
- `-filter Box input.jpg output.jpg`
- `-crop 100x100+10+10 input.jpg output.jpg`
- `-contrast 20% input.jpg output.jpg`
- `-compress JPEG quality:75 input.jpg output.jpg`
- `-colorspace Gray input.jpg output.jpg`
- `-colors 16 input.jpg output.jpg`

## 复制目录

如果你想复制一个包含所有文件的整个目录，必须使用 `cp -r source directory`。这也会复制隐藏文件。

以下命令将所有的 `book/*.tex` 文件复制到当前目录（`.` 表示当前目录）：

```bash
cp book/*.tex .
```

第二个命令创建了整个目录的备份：

```bash
cp -a book-bak
```


```
$ ghostscript -device=x11 /usr/share/doc/samba/Samba-HOWTO.pdf
```

>>showpage, press (return) to continue<<

在提示符处，按回车（或 `Return`）逐页查看文件。当你到达文档末尾时，可以输入另一个 Postscript 或 PDF 文件名并翻页该文件。完成后，输入 `quit`。

如果 `ghostscript` 检测到 Postscript 或 PDF 文件存在问题，你可能会看到警告或错误信息。在大多数情况下，如果你能看到文档内容，可以忽略这些信息。

`evince` 命令也可以用于显示 Postscript 或 PDF 文件。只需将 ps 或 pdf 文件作为参数启动 `evince` 命令即可：

```
$ evince /usr/share/doc/gutenprint-doc/gutenprint-users-manual.pdf
```

## 使用 Adobe Reader

便携文档格式（PDF）提供了一种以打印呈现的形式存储文档的方法。通过 Adobe Reader，你可以以非常友好的方式查看 PDF 文件。Adobe Reader 使得在 PDF 文件中移动变得简单。PDF 文件可能包含超链接、目录、图形和各种字体。最近的版本允许你填写表单或标记内容。

你可以从 Adobe 网站（www.adobe.com/acrobat/readstep2.html）获取 Linux 版的 Adobe Reader。如果你需要 PDF 文档的特殊表单或编辑功能，你应该获取此阅读器，而不是使用 `Evince` 等开源 PDF 查看器。

安装 Adobe Reader 后，选择“应用程序-Office-Adobe Reader”来启动它。或者你可以输入以下命令来启动程序：

```
$ accroread
```

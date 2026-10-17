
`Alias` 指令指向一个文件系统位置（不一定在 DocumentRoot 内部）。例如，如果设置了以下行，对 bigjob (`http://www.mybox.com/bigjob/index.html`) 文档的请求将导致检索 `/home/newguy/proj/index.html`。

```
Alias /bigjob /home/newguy/proj/
```

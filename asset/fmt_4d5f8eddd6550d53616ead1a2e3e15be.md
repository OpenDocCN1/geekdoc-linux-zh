
`$ fmt diary.txt | crypt | mail -s Diary confidant@linux.org`

Enter key:

控制终端（我简称为 `/dev/tty`）用于直接与用户发起对话（例如，询问他某些问题）。一个例子是 `crypt` 命令：

```
$ fmt diary.txt | crypt | mail -s Diary confidant@linux.org
Enter key:
```

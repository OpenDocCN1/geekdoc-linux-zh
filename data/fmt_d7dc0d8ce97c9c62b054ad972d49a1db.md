
在其中一个 `scp` 示例中，我们在本地复制了一个远程文件。你可以通过以下会话执行相同的操作：

```
[paul@susannah-$] sftp 10.0.0.1
Connecting to 10.0.0.1...
paul@10.0.0.1's password:
sftp> get remote.txt
Fetching remote.txt 100% 00:00
sftp> quit
paul@susannah-$
```

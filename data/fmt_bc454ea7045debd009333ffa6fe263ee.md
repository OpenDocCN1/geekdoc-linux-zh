
```
echo off
net use m: \server1\shares\admin
net use n: \server1\shares\mktg
net use o: \server2\archives
```

在这里，`server1`的两个共享映射到驱动器 M 和 N，`server2`的一个共享映射到驱动器 O。

如果你愿意，可以使用特殊变量 `%username%` 来获取用户的用户名。如果你为每个用户创建了一个文件夹并想为每个用户的文件夹映射驱动器，这非常有用。例如：

```
net use u: \server1\users\%username%
```

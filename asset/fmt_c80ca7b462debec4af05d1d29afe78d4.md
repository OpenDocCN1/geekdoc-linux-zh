
在使用 `tar` 选项时，你可以使用短名称（如 `-c`）或长名称（如 `--create`）。

![](img/b8a4c65ba2acb99909d8842055c0bdd7_144_2.png)

## 活动 6-1：使用 `tar` 工具

**所需时间：** 10 分钟  
**目标：** 创建、查看和提取归档。  
**描述：** 在此活动中使用 `tar` 工具创建、查看和提取归档。

1. 启动虚拟机。
2. 打开终端。创建一个目录，`mkdir activity61`。进入该目录，`cd activity61`。创建一个文件，`touch apple`。
3. 使用 `tar -cf fruit.tar apple orange` 创建归档。
4. 使用 `ls -l` 查看目录。归档文件的大小。
5. 模拟用户删除文件，`rm apple`。
6. 使用 `ls -l` 查看目录。`apple` 和 `orange` 还在吗？
7. 使用 `tar -tvf fruit.tar` 查看归档的成员。
8. 使用 `ls -l` 查看目录。`apple` 和 `orange` 还在吗？
9. 提取归档，`tar -tvf fruit.tar` 查看归档内容。
10. 使用 `tar -xvf fruit.tar` 提取归档文件。
11. 使用 `ls -l` 查看目录。`apple` 和 `orange` 还在吗？
12. 归档文件还在吗？
13. 移除归档，`rm fruit.tar`。

有时你需要从归档中提取少数成员，例如用户不小心删除了文件。下面的示例显示了使用工具从归档中提取成员：

1. `tar -tvf fruit.tar`
2. `-rw-r--r-- 1 user user 2012-05-01 11:22 apple`
3. `-rw-r--r-- 1 user user 2012-05-01 11:22 banana`
4. `-rw-r--r-- 1 user user 2012-05-01 11:22 orange`
5. `tar -xvf fruit.tar apple`
6. `apple`

第 1 行命令列出了 `fruit.tar` 归档的成员，如 2 到 4 行所示。第 5 行命令包含 `-x` 选项来指定要提取的成员（在这里是 `apple`）。如果你想提取多个成员，可以使用相同的选项。下面的示例显示一次性提取多个成员：

```
tar -xvf fruit.tar apple orange
```

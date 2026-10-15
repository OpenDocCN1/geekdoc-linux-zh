

## 5.3.11 CMS 共享文件系统

z/OS 程序员可能熟悉 z/OS UNIX 系统服务（z/OS UNIX 或 UNIX 系统服务），它允许 z/OS 访问 UNIX 文件。z/OS UNIX 文件系统与 z/OS 数据集之间最明显的区别是，从 UNIX 系统服务内部访问时，z/OS UNIX 是一个分层文件系统。

z/VM 文件系统 CMS 共享文件系统（SFS）允许你以分层方式查看系统：z/OS 程序员可能更习惯这种类型的分层文件系统。

SFS 是随 z/VM 一起提供的额外文件系统，它相对于普通的 CMS 文件系统具有多个优势。表 5-6 列出并比较了这些文件系统。

### 表 5-6 比较和对比 SFS 与普通 CMS 文件系统

| 共享文件系统 | CMS 文件系统 |
|---|---|
| 文件级共享 | 小磁盘级共享 |
| 最小分配：零 4096 字节块 | 最小分配：1 个柱面 |
| 分层文件系统 | 平面文件系统 |
| 分配可以动态更改 | 需要更大的小磁盘 |
| 文件级恢复 | 小磁盘级恢复 |

SFS 本质上是由服务器管理的 minidisk 存储集合。图 5-4 第 273 页所示的以下三个主要区域：

- **控制数据**
  保存文件池及其用户的定义。
- **日志数据**
  保存日志，以便在中断发生时可以回滚文件。
- **用户数据**
  保存用户数据。服务器从此处分配数据以提供给用户。

![](img/b0a4b9056f819dccd4781a5105c92d45_288_0.png)

图 5-4 共享文件系统（SFS）

使用 SFS，你不再使用 minidisk，而是由管理员将你注册到文件池，并从你使用的存储组中分配一定数量的 4096 字节块，类似于 CMS minidisk 的使用方式。

虽然访问空间与访问 CMS minidisk 相似，但你使用文件池名称与用户 ID 拼接，而不是 minidisk 设备号。例如，而不是使用 191 和 ACCESS 命令，你将使用：

```
VMSYSU:USERID
```

访问 SFS 后，用户可以使用命令创建目录和子目录，方式与在工作站上类似，如果需要可以创建分层文件结构。用户然后可以在文件级 GRANT 权限，以允许其他用户读取或写入其文件空间中的数据。

如果你已在文件池中分配了空间，请查看第 274 页表 5-7 中列出的命令。

### 表 5-7 与 SMS 相关的命令

| 命令 | 描述 |
|---|---|
| SET FILEPOOL | 设置（或重置）你的默认文件池；例如：set filepool vmsysu |
| QUERY FILEPOOL | 显示你的当前文件池；例如：query filepool current |
| QUERY LIMITS | 查看你可用的 4-K 块数量；例如：query limits |
| DIRLIST | 列出你的目录。这类似于使用 FILELIST 列出 CMS 文件。 |
| ACCESS | 为你的文件空间分配一个模式字母；例如：access vmsysu:cmsuser a ACCESS 与 minidisk 的访问方式类似。 |
| CREATE | 创建目录；例如：create directory test CREATE 类似于 PC 上的 mkdir。 |
| GRANT | 授予其他用户访问文件或目录的权限。 |

整个文件系统有一个管理员，负责备份以及根据需要将 minidisk 分配给存储组。

z/VM 随附三个文件池服务器：

- VMSERVR 由 z/VM 使用
- VMSERVS 由 z/VM 使用
- VMSERVU，一个示例用户文件系统

有关这些主题的更多信息，请参阅 z/VM: CMS File Pool Planning, Administration, and Operation, SC24-6074，以及 z/VM: CMS Commands and Utility Reference, SC24-6073。

## 5.4 作业调度和运行批处理作业

z/VM 和 Linux 提供了在一天/一月/一年的特定时间调度作业运行以及使其定期运行的方法。这对于安排非中断性系统维护任务很有用；运行这些任务时，你不必停止用户在给定时间可能正在进行的工作。任务可以包括：压缩系统日志以节省空间、更新备份等。


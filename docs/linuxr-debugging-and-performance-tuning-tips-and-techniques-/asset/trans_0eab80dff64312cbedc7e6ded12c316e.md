

## 8.2 文件系统管理文件

```
usbdevfs /proc/bus/usb usbdevfs rw 0 0
/dev/hda5 /d ext3 rw 0 0
none /dev/pts devpts rw 0 0
none /dev/shm tmpfs rw 0 0
none /proc/sys/fs/binfmt_misc binfmt_misc rw 0 0
/dev/hda1 /win vfat rw,nosuid,nodev,noexec 0 0
```

请注意，`/etc/mtab` 包含一些 `/proc/mounts` 中没有的信息（例如，查看 `/win` 挂载点的那一行）。反过来说，使用 `mount -f` 也可以向 `/etc/mtab` 中写入并非真实存在的条目（这种做法有其用途，参见 `mount(8)`）。总之，`/proc/mounts` 始终描述实际挂载的内容；然而，`/etc/mtab` 包含了 `/proc/mounts` 中没有的挂载选项信息。因此，为了获得完整的情况，您可能需要读取这两个文件。

### 8.2.1 使用挂载选项

mount 命令支持控制内核允许或禁止对文件系统执行哪些操作的选项。这些选项有很多。只有两个在命令行中真正有用：

- **ro**
  以只读方式挂载文件系统。这对于 CD-ROM 和 DVD 等只读介质是必需的。
- **loop**
  使用回环设备将普通文件作为文件系统处理。我们在前面已经展示过此操作的示例（参见第 8.1.3 节“挂载文件系统：mount”，第 236 页）。

选项通过 `-o` 命令行选项传递，并且可以组合使用，以逗号分隔。例如，以下是之前使用的命令行：

```
mount -t iso9660 -o ro,loop shrink6-1386-disc1.iso /mnt/cdrom
```

其余选项旨在用于 `/etc/fstab`（尽管也可以在命令行上使用）。以下列表列出了我们认为在日常使用中最重要的选项。

- **auto, noauto**
  标记为 auto 的文件系统将在系统启动时通过 `mount -a`（挂载所有文件系统）进行挂载。noauto 文件系统必须手动挂载。

  这些文件系统仍然会出现在 `/etc/fstab` 中，与其他文件系统并列。（例如，参见我们 `/etc/fstab` 文件中之前显示的 `/win` 条目。）
- **defaults**
  使用默认选项 rw, suid, dev, exec, auto, nouser 和 async。（async 是一个高级选项，可增加 I/O 吞吐量。）
- **dev, nodev**
  允许（或禁止）在文件系统上使用字符设备或块设备文件。
- **exec, noexec**
  允许（或禁止）执行文件系统上的二进制可执行文件。
- **user, nouser**
  允许（或禁止）任何用户挂载此文件系统。这对 CD-ROM 很有用；即使在单用户工作站上，不切换到 root 用户就能挂载 CD 也是方便的。只有挂载文件系统的用户才能卸载它。user 隐含 noexec, nosuid 和 nodev 选项。
- **suid, nosuid**
  支持（或不支持）文件系统上可执行文件中的 setuid 和 setgid 位。
- **rw**
  以读写方式挂载文件系统。

nodev, noexec 和 nosuid 选项对于软盘和 CD-ROM 文件系统的安全性特别有价值。考虑一种学生环境，其中允许学生挂载自己的软盘或 CD。制作一个包含 setuid-root shell 或具有全系统写权限的硬盘设备文件的文件系统是很简单的，这可能会让一些精明的用户修改系统文件的权限。

每个文件系统都有特定的额外选项。对于 ext2 和 ext3，一个重要的选项是 grpid。我们将对该选项的讨论推迟到第 11.5.1 节“新文件和目录的默认组”，第 412 页。所有受支持文件系统的详细信息可在 mount(8) 手册页中找到。

作为一个具体的例子，让我们重新考虑我们系统中 Windows 分区的那一行：

```
# device mount-point type options freq
/dev/hda1 /win vfat noauto,defaults,user,uid=2076,gid=10 0 0
```

noauto 选项防止 Windows 分区在启动时挂载。defaults 选项等同于 rw, suid, dev, exec, async。user 选项允许我们在不是 root 的情况下挂载文件系统。uid= 和 gid= 选项强制 /win 中的文件属于我们普通用户，这样我们在处理该分区时就不需要 root 权限。

### 8.2.2 处理已挂载的文件系统：getmntent()

可以通过 getmntent() 例程组以编程方式读取 `/etc/fstab`、`/etc/mtab` 和 `/proc/mounts` 中的任何一个：

```c
#include <stdio.h>
#include <mntent.h>
```
*(Glibc)*

```c
FILE *setmntent(const char *filename, const char *type);
struct mntent *getmntent(FILE *filep);
int addmntent(FILE *filep, const struct mntent *mnt);
int endmntent(FILE *filep);
char *hasmntopt(const struct mntent *mnt, const char *opt);
```

setmntent() 打开包含挂载点条目的文件。filename 参数是要打开的文件名。type 参数类似于 fopen() 的第二个参数，指示读、写或读写访问。（考虑到 mount 命令，它必须为每个挂载的文件系统向 /etc/mtab 添加一个条目，而 umount 必须删除一个。）返回的 FILE * 类型值随后用于其他例程。

getmntent() 遍历文件，返回指向静态 struct mntent 的指针，该结构被填充了相应的值。这个静态存储每次调用时都会被覆盖。当没有更多条目时，它返回 NULL。（这与读取密码文件和组文件的例程类似；参见第 6.3 节“用户和组名”，第 195 页。）

调用 addmntent() 向打开的文件末尾添加更多信息；它旨在供 mount 使用。

endmntent() 关闭打开的文件；在处理完成后调用它。不要只调用 fclose()；与 FILE * 变量关联的其他内部数据结构可能需要清理。

hasmntopt() 是一个更专业的函数。它扫描作为第一个参数传入的 struct mntent，查找与第二个参数匹配的挂载选项。如果找到该选项，它返回匹配子字符串的地址。否则，它返回 NULL。

struct `mntent` 中的字段直接对应于 `/etc/fstab` 文件中的字段。其结构如下：

```c
struct mntent {
    char *mnt_fname;  /* 文件系统设备或服务器。 */
    char *mnt_dir;    /* 挂载的目录。 */
    char *mnt_type;   /* 文件系统类型：ufs, nfs 等。 */
    char *mnt_opts;   /* 文件的逗号分隔选项。 */
    int mnt_freq;     /* 转储频率（以天为单位）。 */
    int mnt_passno;   /* 'fsck' 的传递编号。 */
};
```

处理已挂载文件系统的正常范式是编写一个外部循环，读取 `/etc/mtab`，一次处理一个 struct `mntent`。我们的第一个示例 ch08-mounted.c 正是这样做的：

```c
1 /* ch08-mounted.c --- 打印已挂载文件系统列表 */
2
3 /* 注意：特定于 GNU/Linux！ */
4
5 #include <stdio.h>
6 #include <errno.h>
7 #include <mntent.h> /* 用于 getmntent() 等 */
8 #include <unistd.h> /* 用于 getopt() */
9
10 void process(const char *filename);
11 void print_mount(const struct mntent *fs);
12
13 char *myname;
14
15 /* main --- 处理选项 */
16
17 int main(int argc, char **argv)
18 {
19     int c;
20     char *file = "/etc/mtab"; /* 默认读取的文件 */
21
22     myname = argv[0];
23     while ((c = getopt(argc, argv, "f:")) != -1) {
24         switch (c) {
25         case 'f':
26             file = optarg;
27             break;
28         default:
29             fprintf(stderr, "usage: %s [-f fstab-file]\n", argv[0]);
30             exit(1);
31         }
32     }
33
34     process(file);
35     return 0;
36 }
37
38 /* process --- 从文件读取 struct mntent 结构 */
39
40 void process(const char *filename)
41 {
42     FILE *fp;
43     struct mntent *fs;
44
45     fp = setmntent(filename, "r");  /* 只读 */
46     if (fp == NULL) {
47         fprintf(stderr, "%s: %s: could not open: %s\n",
48                  myname, filename, strerror(errno));
49         exit(1);
50     }
51
52     while ((fs = getmntent(fp)) != NULL)
53         print_mount(fs);
54
55     endmntent(fp);
56 }
57
58 /* print_mount --- 打印单个挂载条目 */
59
60 void print_mount(const struct mntent *fs)
61 {
62     printf("%s %s %s %d %d %d\n",
63            fs->mnt_fname,
64            fs->mnt_dir,
65            fs->mnt_type,
66            fs->mnt_opts,
67            fs->mnt_freq,
68            fs->mnt_passno);
69 }
```

与我们之前见过的大多数程序不同，这个程序是特定于 Linux 的。许多 Unix 系统都有类似的例程，但不保证它们完全相同。默认情况下，ch08_mounted 读取 /etc/mtab，打印每个已挂载文件系统的相关信息。-f 选项允许您指定读取不同的文件，例如 /proc/mounts 甚至 /etc/fstab。

main() 函数处理命令行（第 23–32 行）并对指定文件调用 process()。（此程序遵循我们的标准样板代码。）

process() 进而打开文件（第 45 行），并遍历返回的每个文件系统（第 52–53 行）。完成后，它关闭文件（第 55 行）。


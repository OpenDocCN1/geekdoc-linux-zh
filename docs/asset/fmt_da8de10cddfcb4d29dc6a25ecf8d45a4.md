
`hosts.allow` 和 `hosts.deny` 文件中的每一行都具有以下格式：
`daemon_list : client_list; [command];`

当 `daemon_list` 是由一个或多个服务器守护进程组成的逗号分隔列表（例如 `postfix`、`vsippd` 和 `sshd`）时，`client_list` 是由一个或多个客户端组成的逗号分隔列表（参见第 461 页的表 11-2），可选的 `command` 是当 `client_list` 尝试访问 `daemon_list` 中的服务器守护进程时执行的命令。

当客户端请求连接到服务器时，将按照以下顺序查询服务器系统上的 `hosts.allow` 和 `hosts.deny` 文件，直到找到匹配项为止：

- 1. 如果守护进程/客户端对匹配 `hosts.allow` 中的某行，则允许访问。
- 2. 如果守护进程/客户端对匹配 `hosts.deny` 中的某行，则拒绝访问。
- 3. 如果 `hosts.allow` 或 `hosts.deny` 文件中没有匹配项，则允许访问。

第一个匹配项决定了是否允许客户端访问服务器。当 `hosts.allow` 或 `hosts.deny` 为空时，就相当于该文件为空。

尽管不建议，但你可以通过删除文件来允许所有客户端访问所有守护进程。

示例：为了获得更安全的系统，请将以下行放入 `hosts.deny` 中以阻止所有访问：

```
$ cat /etc/hosts.deny

ALL : ALL : echo "%s tried to connect to %d and was blocked " >> /var/log/tcpwrappers.log
```

此行防止任何客户端连接到任何服务，除非在 `hosts.allow` 中明确允许此类操作。当匹配到此项时，它会向向名为 `/var/log/tcpwrappers.log` 的文件添加一行。`%s` 扩展为客户端信息，`%d` 扩展为尝试连接的守护进程名称。

在配置了上述 `hosts.deny` 文件后，你可以在 `hosts.allow` 中包含某些行，以显式允许访问某些服务和系统。例如，`hosts.allow` 文件允许任何人连接到 OpenSSH 守护进程（`ssh`, `scp`, `sftp`），但仅允许来自与本地系统相同网络的连接以及 `192.168.subnet` 用户：

```
$ cat /etc/hosts.allow

sshd: ALL

inet: ALL LOCAL

inet: 192.168.* 127.0.0.1
```

第一行允许从任何系统（`ALL`）连接到 `sshd`。第二行允许从与服务器相同局域内的任何系统（`LOCAL`）连接。第三行匹配任何 IP 地址以 `192.168` 开头的系统以及本地系统。

## 设置 chroot 监狱

在早期的 UNIX 系统中，根目录是文件系统中的固定点。在现代 UNIX 变体（包括 Linux）中，你可以根据进程定义根目录。`chroot` 工具允许你使用非 `/` 的根目录来运行进程。

根目录出现在目录层次结构的最顶端，没有父目录。此进程无法访问根目录以上的文件，因为那里不存在这些文件。例如，如果你运行一个程序（进程）并指定其根目录为 `/imp/jail`，该程序在 `/imp` 或更高处将没有任何文件的副本：`jail` 是程序的根目录，并被标记为根（而不是 `jail`）。

通过创建一个虚拟根目录（通常称为 `chroot` 监狱），你可以防止程序访问、执行或修改从其根开始的目录层次结构之外的（可能是恶的）。你必须正确设置 `chroot` 监狱以增加安全性：如果你没有正确设置 `chroot` 监狱，那么在没有 `chroot` 监狱的情况下，恶意用户更容易获得系统的访问。

## 设置服务器

### 使用 chroot

创建 `chroot` 监狱非常简单：以 `root` 权限运行，将 `jail` 给命令 `/usr/bin/chroot`。下面的示例显示了以 `root` 权限运行 `chroot` 的结果：

```
/usr/bin/chroot /tmp/jail
```

除非以 `root` 权限运行，否则 `chroot` 工具将失败。因为具有 `root` 权限的用户可以跳出 `chroot` 监狱，所以务必在 `chroot` 监狱中使用降低后的权限（即除 `root` 以外的权限）运行程序。

```
$ sudo /usr/bin/chroot /tmp/jail /bin/bash
```

有几种方法可以降低用户的权限。例如，你可以将 `su` 或 `sudo` 放入监狱并在监狱内部启动 shell 或守护进程，使用这些程序之一来降低在监狱中工作的用户的权限。如下命令会在监狱内启动一个具有降低权限的 shell：

其中 `jailpath` 是监狱的路径，`user` 是 shell 具有相应权限的用户。这种场景的问题是，为 Ubuntu 编译的 `sudo` 和 `su` 会调用 PAM。要运行这些工具之一，你需要将所有的 PAM（包括其库文件和配置文件）复制到监狱中，并使用 `sudo`（或 `su`）以及 `/etc/passwd` 文件。然而，源代码调用了 PAM，因此你将修改源代码使其不再调用 PAM。这两种技术都是耗耗时的，并且引入了可能导致监狱不安全的复杂性。

接下来的 C 程序¹ 在 `chroot` 监狱中使用降低的权限运行程序。由于此程序在调用 `chroot()` 之前获取了你在命令行上指定的用者的 UID 和 GID，因此你不需要将 `/etc/passwd` 放入监狱中。

¹ 感谢 David Chisnall 和 l'Étoile Project (`etoiles.com`) 提供的 `uchroot` c 程序。

### 设置服务器

该程序将指定程序的权限降低到指定用户的权限。此程序作为解决上述问题的简单解决方案，以便你可以尝试 `chroot` 监狱（`chroot jail`）并更好地理解它的工作原理。

`# cat uchroot.c`

```c
/*  svn.gna.org/viewcs/etotile/trunk/etotile/Live/uchroot.c 查看使用条款。 */

#include <stdio.h>

#include <stdlib.h>

#include <pwd.h>
int main(int argc, char *argv[]) {
    if(argc < 4) {
        printf("Usage: %s (username) {directory} [program] [arguments]\n", argv[0]);
        return 1;
    }
    /* 解析参数 */
    struct passwd *pass = getpwnam(argv[1]);
    if(pass == NULL) {
        printf("Unknown user %s\n", argv[1]);
        return 2;
    }
    /* 设置所需的 UID */
    if(chroot(argv[2]) || setgid(pass->pw_gid) || setuid(pass->pw_uid)) {
        printf("%s must be run as root. Current uid-%d, eid-%d\n", argv[0], (int)getuid(), (int)geteuid());
        return 3;
    }
    char buf[100];
    return execv(argv[3], argv + 3);
}
```

以下第一个命令 `uchroot.c` 会创建一个名为 `uchroot` 的可执行文件。随后的命令将 `uchroot` 移动到 `/usr/local/bin` 并赋予其恰当的所有权。

```bash
$ gcc uchroot.c -o uchroot
$ sudo mv uchroot /usr/local/bin
$ sudo chroot root /usr/local/bin/uchroot
$ ls -l /usr/local/bin/uchroot
-rwxr-xr-x 1 root root 1922 2010-07-17 08:26 /usr/local/bin/uchroot
```

## 第 11 章 系统管理：核心概念

使用本节之前的设置，执行以下命令以用户 `sam` 的权限在 `chroot` 监狱中运行 shell：

```bash
$ sudo /usr/local/bin/chroot sam /tmp/jail/bin/bash
```

## 维护多个 chroot 监狱

提示：如果你计划部署多个 `chroot` 监狱，最好在活动监狱之外的其他地方保留一份 `bin` 和 `lib` 目录的干净副本。

## 在 chroot 监狱中运行服务

在监狱内运行 shell 的作用有限。实际上，你可能更想在监狱内运行特定的服务。若要在监狱内运行服务，请确保所需的所有文件都在监狱内。使用 `uchroot`，在 `chroot` 监狱中启动服务的命令格式如下：

```bash
```

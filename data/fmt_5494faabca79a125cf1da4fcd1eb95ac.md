
```
# Customize CPP to point to your system's C preprocessor.
# if cpp is on your path:
#CPP=cpp

# if cpp is not on your path, try one of these:
CPP=/lib/cpp               # traditional
# CPP=/usr/lib/cpp          # also traditional
# CPP=/usr/ccs/lib/cpp     # Solaris 2.x
```

接下来，我们需要查看 `config/` 目录并创建两个文件：

- `config.h`，其中将包含特定于平台的配置信息
- `options.h`，其中将包含特定于站点的配置信息

有许多针对不同平台的示例 `config.h` 文件。有一个针对 Linux 的特定版本，因此我们将该文件复制为 `config.h` 并进行审查。在对反映我们的 Red Hat Linux 环境的几个更改之后，它就准备就绪了。现在让我们把注意力转向 `options.h`。对于 `options.h`，只有一个示例文件：`options.h-vanilla`。顾名思义，这是一个基本文件，包含一系列 `#define`，用于为典型环境配置 amanda。我们需要进行一些更改：

- 定义通用实用程序的路径。
- 防止程序名称带有后缀 `-2.3.0`。
- 定义程序应安装的目录。

虽然第一项更改对于习惯构建软件的人来说相当标准，但最后两项更改实际上是由于 RPM 的原因。使用 RPM 时，没有必要使用特定版本的名称来命名程序，因为 RPM 可以轻松地升级到新版本，甚至在新版本表现不佳时降级回去。amanda 使用的默认路径将文件隔离，以便于维护。使用 RPM 时，不需要这样做，因为 RPM 安装的每个文件都会写入数据库。此外，Red Hat Linux 系统遵循文件系统标准（FSTND），因此任何旨在用于 Red Hat 系统的软件包也应该遵循 FSTND。幸运的是，amanda 的编写使得进行此类更改变得容易。即使我们需要修改安装脚本，RPM 也会作为其补丁处理的一部分接收这些更改。

我们将省略通常的拼写错误、不兼容性及由此导致的重新构建过程。在经过未透露具体次数的迭代后，我们的 `config.h` 和 `options.h` 文件已经完美。Amanda 现在可以构建：

```
# make
Making all in common-src
make[1]: Entering directory '/usr/src/redhat/SOURCES/amanda-2.3.0/common-src'
...
make[1]: Leaving directory '/usr/src/redhat/SOURCES/amanda-2.3.0/man'
# make install
```

如前所述，amanda 的结构使得大多数情况下只需在 `tools/munge` 和 `config` 中的两个文件中进行更改。我们的情况也不例外——最终，我们只需要修改这些部分。

## 20.2.3. 安装和测试

众所周知，软件能够构建并不意味着它已准备好投入使用。首先需要对其进行测试。为了测试 amanda，我们需要安装它。Amanda 的 `makefile` 有一个 `install` 目标，因此我们使用它作为起点。我们还将获取输出的副本，因为我们稍后会用到它。

```
# make install
Making install in common-src

make[1]: Entering directory '/usr/src/redhat/SOURCES/amanda-2.3.0/client-src'
Installing Amanda client-side programs:
install -c -o bin amandad /usr/lib/amanda
install -c -o bin sendsize /usr/lib/amanda
install -c -o bin calcsiz /usr/lib/amanda
install -c -o bin sendbackup-dump /usr/lib/amanda
install -c -o bin sendbackup-gnutar /usr/lib/amanda
install -c -o bin rantar /usr/lib/amanda
install -c -o bin selfcheck /usr/lib/amanda
Setting permissions for setuid-root client programs:
(cd /usr/lib/amanda ; chown root calcsiz ; chmod u+s calcsiz)
(cd /usr/lib/amanda ; chown root runar ; chmod u+s runar)
...
Making install in server-src
Installing Amanda libexec programs:
install -c -o bin taper /usr/lib/amanda
install -c -o bin dumper /usr/lib/amanda
install -c -o bin driver /usr/lib/amanda
install -c -o bin planner /usr/lib/amanda
install -c -o bin reporter /usr/lib/amanda
install -c -o bin getconf /usr/lib/amanda
Setting permissions for setuid-root libexec programs:
(cd /usr/lib/amanda ; chown root dumper; chmod u+s dumper)
(cd /usr/lib/amanda ; chown root planner; chmod u+s planner)

Installing Amanda user programs:
install -c -o bin amrestore /usr/sbin
install -c -o bin amadmin /usr/sbin
install -c -o bin amflush /usr/sbin
install -c -o bin amlabel /usr/sbin
install -c -o bin amcheck /usr/sbin
install -c -o bin amdum /usr/sbin
install -c -o bin amcleanup /usr/sbin
install -c -o bin amtape /usr/sbin
Setting permissions for setuid-root user programs:
(cd /usr/sbin ; chown root amcheck; chmod u+s amcheck)

Installing Amanda changer libexec programs:
install -c -o bin chg-generic /usr/lib/amanda

Installing Amanda man pages:
install -c -o bin amanda.8 /usr/man/man8
install -c -o bin amadmin.8 /usr/man/man8
install -c -o bin amcheck.8 /usr/man/man8
install -c -o bin amcleanup.8 /usr/man/man8
install -c -o bin amdum.8 /usr/man/man8
install -c -o bin amflush.8 /usr/man/man8
install -c -o bin amlabel.8 /usr/man/man8
install -c -o bin amrestore.8 /usr/man/man8
install -c -o bin amtape.8 /usr/man/man8
```

好的，没有大问题。不过，Amanda 确实需要额外的努力才能让一切正常运行。查看 `docs/INSTALL`，我们按照步骤让 amanda 在测试系统上同时作为客户端和服务器运行。在执行每个步骤时，我们会记录以便将来参考。

对于客户端：

1. 设置 `~/.rhosts` 文件，允许服务器连接。
2. 使磁盘设备文件对客户端可读。
3. 使 `/etc/dumpdates` 对客户端可读且可写。
4. 在 `/etc/services` 中添加 `amanda` 条目。
5. 在 `/etc/inetd.conf` 中添加 `amanda` 条目。
6. 对 `inetd` 执行 `kill -HUP` 命令。

对于服务器：

1. 创建一个目录用于存放服务器配置文件。
2. 修改提供的示例配置文件以适应我们的站点。
3. 添加 `crontab` 条目以每晚运行 `amanda`。

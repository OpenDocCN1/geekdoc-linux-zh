

某物是专属存在，那么默认值必须是禁用。在其他情况下，例如两个选项 `--disable-user-locking` 和 `--enable-user-locking(t=DIR)`，不清楚会发生什么。确定默认值的最简单方法是不带任何选项运行 `configure`。这将创建一系列文件，包括示例 6-17 中显示的文件。文件 `config.log` 和 `config.status` 包含用于 `configure` 的调试信息。如果您在让 `configure` 正常运行时遇到问题，或者 `configure` 未能识别系统的某个组件，请查看这些文件。`config.cache` 文件包含用于构建 `Makefile` 的信息。如果您发现 `configure` 找到了它将在链接过程中使用的库（例如），并且您希望使用其他库，您可以对 `config.cache` 进行更正，然后执行 `configure --recheck` 以重新构建 `Makefile`。`config.h` 文件包含各种变量的定义，这些变量随后用于编译过程。在这里，您可以找到示例 6-16 中显示的各种选项的默认值。您可以直接对 `config.h` 文件进行更正，但为了避免错误，您最好执行 `make realclean`，这会删除由 `configure` 生成的所有文件；然后使用所需的参数重新运行 `configure`。起初，这可能看起来是一个繁琐的过程，但经过练习，您将更加熟练地处理 `configure`。这绝对值得付出努力，因为许多公开可用的工具都是使用 `configure` 构建的。

## 示例 6-17 由 `configure` 创建的文件

```text
Makefile
config.cache
config.h
config.log
config.status
```

表 6.2 描述了与 OPIE 的 `configure` 相关的几个重要参数。这显然不是一个详尽的列表，您应该检查所有参数以确定您的需求。首先在一个测试环境中配置和编译 OPIE 是一个好主意，然后重新配置并重新编译，直到您获得一个适合您的实现。

在确定您希望与 OPIE `configure` 工具一起使用的选项后，您就可以准备执行它了。示例 6-18 显示了此类执行的输出（由于格式限制导致换行）。在我们的例子中，我们将使用 `--enable-access-file`，以便我们可以探索相关功能。除非绝对必要，否则我们不推荐使用 `--enable-access-file` 选项。

`configure` 的完整输出将在 `config.log` 中找到。请注意，`configure` 警告我们关于访问文件 `/etc/opieaccess` 的使用，这将在第 142 页的*使用 /etc/opieaccess*中讨论。它还告诉我们二进制文件将安装在 `/usr/local/bin`。这将发生在我们运行 `make install`（或其变体）时；这将在本节稍后讨论。请注意，二进制文件的此位置不适用于替换程序 `su`、`login` 和 `ftpd`。

### 表 6.2 重要 OPIE 配置选项说明

| OPIE configure 选项 | 说明 |
| :--- | :--- |
| --enable-user-locking=[DIR] | 允许指定锁文件目录的备用位置。默认值是 /etc/opielocks。这些锁文件的目的是缓解竞争攻击，并且是根据 RFC2289 的要求实现的。 |
| --disable-user-locking | 禁用锁文件的使用。 |
| --enable-access-file=FILENAME | 启用访问控制列表的使用。FILENAME 将被替换为该文件的绝对路径名。默认情况下，此选项被禁用且不推荐。 |
| --enable-su-star-check | 导致所有密码无效（密码字段为 *）的用户尝试 su 时失败。这适用于 root。仅在使用替换的 su 程序时才有意义。 |
| --enable-insecure-override | 通常，OPIE 将禁止通过网络披露秘密密码。设置此配置选项允许使用 opie-passwd 和 opiekey 的 -f 标志来覆盖安全检查。不推荐使用此选项。 |
| --enable-server-md4 | 导致服务器端应用程序使用 MD4 而不是 MD5。MD5 是默认且推荐的。 |

## 示例 6-18 为 OPIE 运行 configure

```text
# ./configure --enable-access-file=/etc/opieaccess
creating cache ./config.cache
Using the access file in /etc/opieaccess -- don't say we didn't warn you!
checking for gcc... gcc
checking whether the C compiler (gcc ) works... yes
checking whether the C compiler (gcc ) is a cross-compiler... no
checking whether we are using GNU C... yes
....
<lots of output snipped>
...
checking for nonstandard gettimeofday... no
updating cache ./config.cache
creating ./config.status
creating configure.munger
creating libmissing/Makefile
creating libopie/Makefile
creating Makefile.munge
creating config.h

Binaries are going to be installed into /usr/local/bin,
Manual pages are going to be installed into /usr/local/man.
creating Makefile

Have you read the README file?
#
```

### 表 6.3 OPIE Makefile 支持的参数

| 参数 | 说明 |
| --- | --- |
| client | 编译和链接客户端程序 opikeyey 和 opigen。¹ |
| server | 编译和链接服务器程序 opiespssd, opieserv,¹ su, login, 和 ftpd。 |
| client-install | 安装客户端程序。 |
| server-install | 安装服务器程序。 |
| install | 安装所有程序（客户端和服务器）。 |
| clean | 删除所有二进制文件和对象文件。 |
| realclean | 删除所有二进制文件、对象文件以及由 configure 创建的文件（包括所有 make 文件）。 |
| no arguments | 编译和链接所有程序（客户端和服务器）。 |

¹opikeyen 是提供给开发者的程序示例；它在功能上类似于 opikeyey。  
¹opieserv 是提供给开发者的程序示例；它在功能上类似于 opiespssd。

由 `configure` 生成的 OPIE Makefile 为我们提供了一些选项。它将接受表 6.3 中描述的参数。

为了我们的示例目的，我们将使用不带参数的 `make` 来编译 OPIE，然后使用 `make install` 来安装 OPIE。如表 6.3 所述，这将创建客户端和服务器活动所需的二进制文件，然后将所有编译的二进制文件安装到适当的位置。示例 6-19 显示了执行 `make` 的部分输出。请注意，OPIE 在编译完实用程序后执行一系列测试。如果您的 Makefile 存在问题，这几乎肯定是问题会出现的地方。

## 示例 6-19 OPIE make

```text
# make
(cd libopie ; make libopie.a CFLAGS='-O -DKKEY_FILE="/etc/opiekeys"')
make[1]: Entering directory '/usr/src/opie/opie-2.32/libopie'
gcc -O -DKKEY_FILE='/etc/opiekeys' -I. -c md4c.c -o md4c.o
gcc -O -DKKEY_FILE='/etc/opiekeys' -I. -c md5c.c -o md5c.o
gcc -O -DKKEY_FILE='/etc/opiekeys' -I. -c atob8.c -o atob8.o
gcc -O -DKKEY_FILE='/etc/opiekeys' -I. -c bto8.c -o bto8.o
...
<lots of output snipped>
...
opiestest: executing 13 tests
( 1/13) testing opieatob8... passed
( 2/13) testing opieatob8... passed
( 3/13) testing opiebtoa8... passed
( 4/13) testing opiebtob8... passed
( 5/13) testing opiegenerator... passed
( 6/13) testing opiegtsequence... passed
( 7/13) testing opiehesh (MD4)... passed
( 8/13) testing opiehash(MD5)... passed
( 9/13) testing opieinsecure...  passed
(10/13) testing opiekeycrunch...  passed
(11/13) testing opielock...        passed
(12/13) testing opieandchallenge...  passed
(13/13) testing opieunlock...      passed
opietest: completed 13 tests. 13 tests passed, 0 tests skipped, 0 tests failed.
...
<lots more output snipped>
gcc -o opiefp.d.o glob.o popen.o y.tab.o -Llibopie -Llibmssing -lopie -lposix -lnsl -lbcrypt -lmssing -lopie -o opiefpd
gcc -O   -c opieserv.c -o opieserv.o
gcc -o opieserv.o -Llibopie -Llibmssing -lopie -lposix -lnsl -lbcrypt -lmssing -lopie -o opieserv
#
```

现在 OPIE 已编译完成，您准备好安装并开始使用它了。但在这样做之前，请阅读以下警告。

# 警告！

> 当您为 OPIE 运行 `make install` 或 `make server-install` 时，替换程序 su, login, 和 `ftpd` 将自动复制到相应位置。幸运的是，此 Makefile 会将您现有的二进制文件复制到 `name.opie.old`（例如，`/bin/login` 变为 `/bin/login.opie.old`）。它还会清除所有 `*.opie.old` 文件的权限。
> 
> 您可能有很多理由不希望使用这些替换程序，特别是如果您正在使用如第 143 页“OPIE 和 PAM”中讨论的 PAM 与 OPIE。为了克服安装 OPIE 的这方面问题，您可以修改 Makefile 以满足您的需求，或者在 OPIE 安装完成后将原始文件复制回来。如果您选择后者方法，请务必在安装 OPIE *之前*记录 su, login, 和 ftpd 的文件权限和所有权。
> 
> 另一个问题是，由于替换程序是自动安装的，任何在安装后尝试登录的用户都将无法登录，直到为他们使用 `opiepass` 和 `opiekey` 生成 OPIE OTP 列表。如果管理员在为 root 生成 OTP 列表之前注销，这会是一个特别的问题。您可能会将自己锁定在系统之外！
> 
> 此外，替换的 `ftpd` 不使用与原始版本相同的标志；因此，如果您使用替换的 `ftpd`，您需要相应地修改 `/etc/inetd.conf`。修改 `/etc/inetd.conf` 后，确保执行 `killall -HUP inetd`。

示例 6-20 显示了 `make install` 的输出。我们现在准备实施并使用 OPIE。


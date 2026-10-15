
```
include /usr/share/openldap/schema/core.schema
include /usr/share/openldap/schema/cosine.schema
include /usr/share/openldap/schema/corba.schema
include /usr/share/openldap/schema/inetorgperson.schema
include /usr/share/openldap/schema/java.schema
include /usr/share/openldap/schema/krb5-kdc.schema
include /usr/share/openldap/schema/kerbersobject.schema
include /usr/share/openldap/schema/misc.schema
include /usr/share/openldap/schema/nis.schema
include /usr/share/openldap/schema/openldap.schema
include /usr/share/openldap/schema/autofs.schema
include /usr/share/openldap/schema/samba.schema
include /usr/share/openldap/schema/kolab.schema
```

## 第 16 章 LDAP

```
objectClass: organizationalPerson
objectClass: inetOrgPerson
mail: ggallei@salmar.com
telephoneNumber: 555-8708
givenname: Galileo
```

让我们来看一些替代方案，好吗？那里有一些非常棒的图形化工具，我稍后会介绍，但开始，你可能已经在 Windows 邮件客户端中有某个地址簿了。也许你或你的办公室正在运行 Outlook，其中有大量的电子邮件地址。你可以将该通讯录导出为 `CSV` 文件（逗号分隔的 ASCII 文件），并从该文件创建一个单一的 `LDIF` 文件进行导入。当然，缺失的步骤是如何轻松地将该 `CSV` 文件转换为 `LDIF` 文件。

我编写了这个简小的 Perl 脚本来解决这个问题。（在附录 B“自动化与脚本”中有更多脚本内容）你可以使用 `Kate` 或 `vi` 来创建它（这两者在第 10 章“与 Shell 合一”中都介绍过）。

```perl
#!/usr/bin/perl
## importcsv.pl : 从 CSV 通讯录创建 LDIF 文件
# Marcel Gagné

open (LDIF_FILE,">>/tmp/loadfile.ldif);
## 这是我们的临时 LDIF 文件。

$csv_file = @ARGV[0];
open (CSVFILE, "$csv_file");
## 打开 CSV 文件。

while ($line = <CSVFILE>) {
	chomp $line;
	($full_name,$email,$street,$city,$poscode)
	= split(",", $line, 5);
	## 在示例中我只关注前两个属性
	($first_name,$last_name) = split(" ", $full_name, 2);
}

printf LDIF_File("%s,dn:\n", cn=$full_name,ou=people,dc=domain,dc=com");
```

## 迈向 Linux 商务桌面

```perl
printf LDIF_FILE("%s"
```

close CSVFILE;

exit (0);

```

确保在脚本中替换你自己的域名。将文件保存为 `importcsv.pl`，然后赋予脚本可执行权限并运行它。

```bash
chmod +x importcsv.pl
./importcsv.pl myfile.csv
```

该脚本接受一个参数，即你的 `CSV` 文件的路径。你可以修改它以接受第二个参数（作为 `LDIF` 文件的路径），但我选择在 `/tmp/loadfile.ldif` 中使用默认名称。

太棒了。你现在可以使用以下命令导入所有数据：

```bash
ldapadd -c -f loadfile.ldif -XV -D "cn=Manager,dc=salmar,dc=com" -W
```

`-W` 标志告诉 `ldapadd` 命令在命令行提示密码，但真正有趣的标志是 `-c` 选项。因为这个 Perl 脚本可能会生成大量的 LDAP 条目，我们不希望 LDAP 命令在每次遇到错误时都崩溃。`-c` 告诉命令无论遇到任何错误都继续执行。

## GQ，一个图形化 LDAP 工具

突然，我们有了一个填充了企业通讯录（或者对于你们中更常用的用户来说，是个人通讯录）所有数据的 LDAP 数据库。这对于初始加载是一个很棒的方法，但当你想要随手向此目录添加数据时，该怎么办？不断创建 `LDIF` 文件可能会有些无聊。如果你检查你的 Linux 发行版光盘，可能会发现一个名为 `GQ` 的基于 `Gtk` 的小包，对于一个提供 LDAP 目录浏览器、架构浏览器以及导入/导出实用程序的精彩工具来说，这个名字相当平和。最棒的是，它让你可以使用友好的图形化界面（图 16-5）在你的 LDAP 目录中添加、删除或修改单个条目。

![](img/c69138fb82b7e78233ca21acbdb2739f_356_0.png)

图 16-5 `GQ` 是一个图形化 LDAP 浏览器/编辑器。

你可以从 Biot.com (`http://biot.com/qq`) 的 Bert Vermeulen 和 Peter Stamfest 获取最新版本的 `GQ`。根据我的描述，构建 `GQ` 需要安装 `Gtk`（版本 1.2 或更高版本）。除此之外，安装过程遵循标准的解压和构建五步法。

```bash
tar -xzvf gq-1.0betal.tar.gz
cd gq-1.0betal
./configure
make
su -c "make install"
```

## 迈向 Linux 商务桌面

当然，我知道你们都懂这些，但没有什么比看到一个程序在你自己的系统上从零开始构建更让我感到满足了。不是吗？我跑题了。
只需在 shell 提示符处输入命令名称即可启动程序：

```bash
gq
```

如果你在该主机上配置并运行了 LDAP 服务器，`gq` 会自动记录它并将其作为默认值。注意程序窗口有三个标签页：搜索（Search）、浏览（Browse）和架构（Schema）。从搜索 标签页，你可以输入 LDAP 目录中的全部或部分名称并找到它。这里有三个字段：第一个是你的名称搜索字段，第二个是你的 LDAP 服务器，第三个允许你指定在目录何进行搜索，例如我示例组织中的 `dc=salmar,dc=com`。如果你留空字段，`gq` 将返回所有名称。从浏览 标签页，你可以添加或修改条目。点击右侧可以删除。（要删除条目，请右键点击条目并选择 Delete）。

要修改条目，右键点击条目并选择 Modify。这会打开一个窗口，你可以更改任何属性。要添加新条目，点击 New。这会打开一个窗口，你可以指定新条目的属性。

Schema 标签页允许你查看 LDAP 目录的架构。如果你想知道目录中可以使用哪些属性，这非常有用。你还可以将架构导出到文件。

从那里开始，下载源代码并将其保存到临时目录。在本示例中，我将使用 2.0 版本。我所做的第一件事是将源代码提取到我的目录中，如下：

```
tar -xzvf httpd-2.0.49.tar.gz
cd httpd-2.0.49
./configure --with-apxs2 --enable-modules=most --enable-modules-shared=all --enable-ssl
```

这会将 Apache 配置为安装到 `/usr/local/apache` 的默认目录结构中。在 Red Hat 安装（以及其他一些系统）案例中，默认目录是 `/home/httpd`。如果你想使用不同的安装位置，请使用 `--prefix` 选项：

```
./configure --prefix=/home/httpd (后续后续选项)
```

`configure` 脚本有许多可以设置的额外标志或选项。在开始安装之前，你可能想运行 `./configure --help`。目前，我将保持简单，并使用我第一个示例中的默认值。当 `configure` 脚本完成创建 `Makefile` 后，输入 `make` 然后跟上 `make install` 即可完成安装。

```
make
make install
```

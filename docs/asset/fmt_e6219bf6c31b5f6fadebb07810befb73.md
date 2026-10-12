
```
% chmod 755 /usr/local/mysql/bin
% chmod u=rwx,go=rx /usr/local/mysql/bin
```

### 4. 客户端不需要访问的目录可以设置为仅 `mysql` 可访问
包含服务器的 `libexec` 目录就是一个例子。以下任一命令都会适当设置其模式：

```
% chmod 700 /usr/local/mysql/libexec
% chmod u=rwx,go=rw /usr/local/mysql/libexec
```

### 5. 更改数据目录及其下所有文件和目录的模式，使它们仅对 `mysql` 可见

```
% chmod -R go-rwx /usr/local/mysql/data
```

这可以防止除用于运行服务器的登录账户之外的其他登录账户直接访问数据目录的内容。

在使用上述说明后，你的 MySQL 安装基础目录的所有权和权限看起来像这样：

```
% ls -la /usr/local/mysql
total 44
drwxr-xr-x  13 mysql  mysql   1024 May  7 10:45 .
drwxr-xr-x  24 root   wheel   1024 May  1 12:54 ..
drwxr-xr-x   2 mysql  mysql   1024 Jul 16 20:58 bin
drwxr-----	12 mysql mysql		1024 May 8 12:20 data
drwxr-xr-x	3 mysql mysql		512 May 7 10:45 include
drwxr-xr-x	2 mysql mysql		512 May 7 10:45 info
drwxr-xr-x	3 mysql mysql		512 May 7 10:45 lib
drwxr-----	2 mysql mysql		512 Jul 16 20:58 libexec
drwxr-xr-x	3 mysql mysql		512 May 7 10:45 man
drwxr-xr-x	6 mysql mysql		1024 May 7 10:45 mysql-test
drwxr-xr-x	3 mysql mysql		512 May 7 10:45 share
drwxr-xr-x	7 mysql mysql		1024 May 7 10:45 sql-bench
```

如图所示，现在所有内容的属主都是 `mysql`，组属主也是 `mysql`。唯一的例外是 `..`，它指的是 `/usr/local/mysql` 的父目录。该目录仅由 `root` 拥有并可被 `root` 修改，这是好事。你不想让未授权用户能够干涉包含你安装目录的目录。

基础目录下的数据目录具有更严格的权限：

```
% ls -la /usr/local/mysql/data
total 10148
drwxr-----	11 mysql mysql		1024 May 8 12:20 .
drwxr-xr-x	22 mysql mysql		512 May 8 13:31 ..
drwxr-----	2 mysql mysql		512 Apr 16 15:57 managerie
drwxr-----	2 mysql mysql		512 Jun 25 1998 mysql
drwxr-----	7 mysql mysql		1024 May 7 10:49 ambpd
drwxr-----	2 mysql mysql		1536 Jun 25 1998 test
drwxr-----	2 mysql mysql		1024 May 8 18:43 tmp
```

在这里，`..` 行指的是数据目录的父目录，即 MySQL 基础目录。

对于数据目录的 `mysql` 独占访问策略，某些文件可能需要例外。例如，如果你使用数据目录作为 Unix 套接字文件的位置，就需要稍微开放对目录的访问权限。否则，客户端程序将无法通过套接字连接到服务器。为了让客户端程序能够访问套接字文件，同时不授予数据目录的完整读取权限，请使用此命令：

```
% chmod go+x /usr/local/mysql/data
```

为了避免以这种方式开放数据目录，请使用不同的位置来存放 Unix 套接字文件，例如基础目录。同样的原则也适用于其他非 `mysqld` 程序有合法需求访问的文件，例如包含全局客户端参数的选项文件。

如前所述，前面的过程假设所有与 MySQL 相关的文件都位于单个基础目录下。如果不是这样，你需要定位每个与 MySQL 相关的目录，并对每个目录执行相应的操作。例如，如果你的数据目录位于 `/var/mysql/data` 而不是 `/usr/local/mysql` 下，你需要发出这些命令来正确更改安装的所有权：

```
# chown -R mysql /usr/local/mysql
# chgrp -R mysql /usr/local/mysql
# chown -R mysql /var/mysql/data
# chgrp -R mysql /var/mysql/data
```

或者，假设你在 MySQL 安装目录下创建一个 `innodb` 目录，用于存放所有与 InnoDB 相关的文件。默认情况下，这些文件放在数据目录中。如果你将它们放在你的 `innodb` 目录中，请设置该目录具有与数据目录相同的访问模式。如果你重新定位通常会放在数据目录中的其他文件（例如日志文件），此原则也适用。

安装根目录下的一些目录实际上是符号链接，指向其他位置时，会出现另一种复杂情况。如果你的 `chown` 和 `chgrp` 版本不跟随符号链接，你需要追踪链接并在链接指向的位置应用所有权更改。一种方法是使用 `find`：

```
# find /usr/local/mysql -follow -print | xargs chown mysql
# find /usr/local/mysql -follow -print | xargs chgrp mysql
```

更改访问模式时也有类似的考虑。例如，如果你的数据目录下有符号链接，且 `chmod` 不跟随它们，请使用此命令代替：

```
# find /usr/local/mysql/data -follow -print | xargs chmod go-rwx
```

由于此时数据目录内容的所有权和权限设置为仅允许 `mysql` 登录用户访问，因此应确保服务器从现在开始始终以 `mysql` 身份运行。确保此点的简单方法是在服务器启动时读取的 `/etc/my.cnf` 文件或任何其他 `my.cnf` 文件的 `[mysqld]` 部分中指定用户：

```
[mysqld]
user=mysql
```

这样，无论你是以 `root` 还是 `mysql` 身份登录启动服务器，服务器都将作为 `mysql` 运行。有关使用特定登录账户运行服务器的更多信息，请参见第 12.2.1.1 节，“使用非特权登录账户运行服务器”。

在保护你的 MySQL 安装后，你可以重新启动服务器。

#### 13.1.2.1 保护 Unix 套接字文件

服务器使用 Unix 域套接字文件进行来自本地主机的客户端连接。套接字文件通常公开可访问，以便客户端程序可以使用它。但是，它不应位于任意客户端具有删除权限的目录中。例如，通常会在 `/tmp` 目录中创建套接字文件，但在某些 Unix 系统上，该目录的权限允许用户删除除自己文件外的其他文件。这意味着任何用户都可以删除套接字文件，从而导致在服务器重启以重新创建套接字文件之前，客户端程序无法建立到服务器的本地主机连接。最好将 `/tmp` 目录的“粘滞位”设置好，这样即使任何人都可以创建目录中的文件，用户也只能删除自己的文件。你可以通过执行以下命令作为 `root` 来设置目录的粘滞位：

```
# chmod +t /tmp
```

某些安装将套接字文件放在数据目录中，如果你使数据目录对 `mysql` 私有，这会导致一个问题。除非由 `root` 或 `mysql` 运行，否则没有任何客户端程序可以访问套接字文件。在这种情况下，一个选项是稍微开放数据目录，使客户端可以看到套接字文件：

```
% chmod go+x /usr/local/mysql/data
```

另一种方法是更改服务器创建套接字文件的位置。例如，你可能通过指定 `/usr/local/mysql/mysql.sock` 作为位置来配置 MySQL 在基础目录中创建文件。要么在全局选项文件中指定位置，要么从源代码重新编译以将该位置构建为默认值。如果你选择使用选项文件，请确保为服务器和客户端都指定位置：

```
[mysqld]
socket=/usr/local/mysql/mysql.sock

[client]
socket=/usr/local/mysql/mysql.sock
```

重新编译的工作量更大，但是一个更完整的解决方案，因为使用选项文件对于不检查选项文件的客户端程序不起作用。（所有标准 MySQL 客户端都会检查，但第三方程序可能不会。）通过重新编译，新的套接字位置将成为客户端库已知的默认值；因此，任何使用客户端库的程序都会将新位置作为其自己的默认值，无论是否使用选项文件。

#### 13.1.2.2 保护选项文件


空括号禁用了模块变量的默认导入，直到需要时才导入。这节省了内存空间，因为你可能不需要预加载的所有模块的所有功能。现在，可以使用 `PerlRequire /path/to/startup.pl` 指令在服务器启动时预加载此脚本。

当你使用诸如 `startup.pl` 这样的脚本预加载模块时，子进程至少可以共享这些模块使用的许多代码页，从而节省 `RAM`，有助于你的系统健康。

### 缓存数据库连接

如果你使用 `Perl DBI` 从 `mod_perl` 脚本中访问关系数据库，你可以通过更改一行代码来显著提高数据库连接的性能。如果你的 `mod_perl` 脚本当前使用 `use DBI;` 调用来直接使用 `DBI` 模块，请将其更改为 `use Apache::DBI;`，这将缓存你应用程序的数据库连接并显著提高性能。还有一些其他你应该考虑的编程技巧：

- 如果你对每个请求都连接到同一个数据库，请考虑在请求处理器外部打开数据库连接。例如：

```perl
sub handle {
    my $r = shift;
    my $q = new CGI;
    my $id = $q->param('id');

    # Connect to database
    my $dbh;
    eval {
        $dbh = DBI->connect($dataSource,
                            $dbUser,
                            $dbPassword, { AutoCommit => 1 })
            or die;
    };

    if ($@) {
        # die "Can't connect to database $DBI::errstr";
        # connect failed do something
        print STDERR "Can not connect to $dataSource \n";
        print STDERR "DB2 Server Error: $DBI::errstr \n";
    }

    my $statement = "SELECT myfield from mytable where ID = $id";
    my $sth = $dbh->prepare($statement);
    my $rv             = $sth->execute;
    if(! $rv ){
        # No record found. Do something
    }

    while ( my @fields = $sth->fetchrow_array){
        print STDOUT "ID $id shows: ", join(', ', @fields),
        "<br>";
    }

    $sth->finish;
}
```

请注意，数据库连接是在 `handle` 中执行的，但由于连接使用的是相同的数据库和用户凭证，因此可以在处理器外部执行。

- 如果可能，请准备一次 `SQL` 语句并复用已准备的语句以节省时间。之前的示例可以更高效地编写如下：

```perl
my $APP_RUN_COUNT = 0;
my ($dbh, $sth);

sub init {
    eval {
        $dbh = DBI->connect($dataSource,
                             $dbUser,
                             $dbPassword, { AutoCommit => 1 }) ||
            die;
    };
    if ($@) {
        # die "Can't connect to database $DBI::errstr";
        # connect failed do something
        print STDERR "Can not connect to $dataSource \n";
        print STDERR "DB2 Server Error: $DBI::errstr \n";
    }
}

sub prepare_statement {
    my $dbh = shift;
    my $statement = "SELECT myfield from mytable where ID = ?";
    $sth = $dbh->prepare($statement);
}

sub handle {
    my $r = shift;
    if ($APP_RUN_COUNT++ == 0) {
        init();
        prepare_statement($dbh);
    }

    my $q = new CGI;
    my $id = $q->param('id');
    my $rv = $sth->execute($id);
    if (! $rv ) {
        # No record found. Do something
    }

    while ( my @fields = $sth->fetchrow_array){
        print STDOUT "ID $id shows: ", join(',', @fields), "<br>";
    }
    $sth->finish;
}
```

在此，`handler` 方法调用 `init()` 和 `prepare_statement()` 例程，为子服务器进程的整个生命周期创建一次全局数据库和语句句柄。这使得脚本比之前的版本高效得多。

### 在部分 Apache 子进程上运行 mod_perl 应用程序

当你开始使用许多 `mod_perl` 脚本时，你会注意到你的 `Apache` 子服务器进程体积变大。你可以使用 `top` 命令来见证这种现象。只要你有足够的 `RAM`，就应该没问题。然而，没有人拥有足够的 `RAM`，因此不依赖大量内存作为解决方案，而是考虑如何更有效地解决此问题，这是一个好主意。

如果你发现由于加载了许多 `mod_perl` 脚本导致 `Apache` 子进程越来越大，请考虑拥有一个专门服务于动态内容的脚本服务器。图 22-6 展示了这是如何运作的。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_661_0.png)

当用户请求名为 `www.domain.com` 的站点的主页时，负责静态页面的 `Apache` 服务器将 `index.html` 页面返回给客户端。该页面包含嵌入的静态和动态内容链接。图中显示了两个这样的链接：`login` 和 `privacy`。当最终用户点击 `login` 链接时，它请求 `http://myapps.domain.com/login`，这是一个不同于 `www.domain.com` 服务器的 `Apache` 服务器。事实上，在理想世界中，这两个应该是两个不同的 `Linux` 系统。然而，并非每个人都有能力像这样拆分动态和静态内容，因此此解决方案并不适用于所有人。

如果你必须在运行 `Apache` 的同一 `Linux` 系统上保留 `mod_perl` 和静态内容，你仍然可以确保肥大的 `Apache` 子进程不提供静态页面。这里是一个我喜欢的解决方案：

1. 为你的 `Apache Web` 服务器编译并安装 `mod_proxy` 模块。
2. 将现有的 `httpd.conf` 文件复制为 `httpd-8080.conf`，并将 `Port` 指令修改为 `Port 8080` 而不是 `Port 80`。从 `httpd.conf` 中移除所有 `mod_perl` 特定的配置，以便所有 `mod_perl` 配置都在 `httpd-8080.conf` 文件中。
3. 修改 `httpd.conf` 文件以包含以下代理指令：

   ```
   ProxyPass /myapps http://127.0.0.1:8080/myapps
   ```

   你可以将 `myapps` 更改为你喜欢的任何内容。如果你更改了这一点，请确保在此讨论中提到的其他位置也进行更改。这里，提供静态页面的 `Apache` 服务器被告知所有到 `/myapps` `URL` 的请求都应通过代理模块提供服务，该模块应从运行在同一 `Linux` 系统（`127.0.0.1` 是本机）但端口为 `8080` 的 `Apache` 服务器获取响应。
4. 在 `httpd-8080.conf` 中添加以下配置以创建 `mod_perl` 脚本位置。

   ```
   <Location /myapps>
   SetHandler perl-script
   PerlHandler MyApp!
   </Location>
   ```

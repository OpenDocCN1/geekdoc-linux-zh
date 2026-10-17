
```perl
#!/usr/bin/perl -w
use strict;

# 检查传递的参数数量，如果错误则退出
if ($ARGV < 0) {
    print "Usage: FileIO <outputfile>\n";
    exit;
}

# 获取第一个参数作为输出文件名
my $output_filename = $ARGV[0];

# 打开文件读取
open (READ_FILE, "/etc/passwd") || die "Cannot open the password file!\n";

# 打开文件写入
open (WRITE_FILE, $output_filename) || die "Cannot open the write file\n";

# 读取输入文件
while (<READ_FILE>) {
    my $line_read = _;
    chomp $line_read;

    # 调用我们的解析程序
    my $username_parsed = Parse_Username($line_read);
    if (length($username_parsed) > 0) {
        print "Parsed username as: [$username_parsed]\n";
        print "Writing to file...\n";
        print WRITE_FILE, "$username_parsed\n";
    }
}

# 关闭句柄
close (WRITE_FILE);
close (READ_FILE);

# 如果不是 /sbin/nologin，从行解析用户名的子程序
sub Parse_Username {
    # 获取传递的参数
    my ($received) = @_;

    # 按 ":"分割行到 @parts 数组
    my @parts = split (/:/, $received);

    # 第一项是用户名，最后一部分是 shell
    if ($parts[0] != /\/sbin\/nologin/) {
        return $parts[0];
    } else {
        return "";
    }
}
```

在这个脚本中有几个值得注意的有趣点——`@ARGV`数组始终从命令行输入中填充，每个参数都是数组中的一个元素。特殊变量`$#[ArrayName]`始终指向数组中最后一个元素的索引；换句话说，它提供了数组的长度。`while <READ_FILE>`行基本上是说“读取文件直到遇到文件结束（EOF）标记”。特殊变量`$_`是PERL处理过的最后一个变量；在这种情况下，是行文本。写入文件非常简单，只需将文件句柄作为第一个参数进行`print`。

# 第 7 章 编写开源安全工具

## 图 7.34 MySQL 数据库设置与填充

```
root@Fedora-wips:/home/roeof - Shell - Konsole
Session Edit View Bookmarks Settings Help
mysql> insert into HTTPPR values ('GET / HTTP/1.0','200 OK');
Query OK, 1 row affected (0.00 sec)
mysql> insert into HTTPPR values ('GET /notthereall HTTP/1.0','404 Not Found')
Query OK, 1 row affected (0.00 sec)
mysql> select * from HTTPPR;
request                 response
----------------------+-----------------
GET /HTTP/1.0          | 200 OK           
GET /notthereall HTTP/1.0 | 404 Not Found 
----------------------+-----------------
2 rows in set (0.00 sec)
mysql>
Shell
```

接下来，我们需要编写PERL脚本。我们需要使用套接字（`sockets`）和某种形式的数据库访问引擎。CPAN模块提供了与数据库通信的功能。要从CPAN安装此库：

1. 输入 `perl -shell -MCPAN`。
2. 如果你是第一次使用CPAN，你需要先配置它——大多数默认设置都是可以。
3. 接下来，在CPAN接口中安装 `DBI`。
4. CPAN接口现在将为你获取必要的文件、进行编译并安装。

PERL安装时已自带了socket库。我们现在拥有了编写程序所需的所有工具。几分钟后，我们最终得到了：

```perl
#!/usr/bin/perl -w
$|=1;
use strict;
use DBI;
use Socket;

##### 参数检查部分
## 检查参数是否正确
```

```perl
if ($ARGV < 0) { print "Usage: SqlSocket <target>\n"; exit; }
```

```perl
# 从命令行获取 Web 服务器目标
$target=$ARGV[0];
```

```perl
##### 数据库部分
print "Connecting to MySQL database...\n";
# 连接到本地 MySQL 数据库 - 不需要认证。
my $connection_string="dbi:mysql:database=HTTP_requests;host=localhost:3306";
$db_handle = DBI->connect($connection_string) || print "Couldn't connect to database: $DBI::errstr\n";
```

```perl
# 构建我们的 SQL 语句
$sql = "SELECT request, response FROM HTTPPR";
```

```perl
# 准备查询
$statement = $db_handle->prepare($sql) || die "Couldn't prepare query '$sql': $DBI::errstr\n";
```

```perl
# 然后执行它！
$statement->execute() || die "Couldn't execute query '$sql': $DBI::errstr\n";
```

```perl
print "Received data from DB OK...\n";
##### 程序主逻辑从开始
# 现在获取数据
my @row;
while (@row = $statement->fetchrow_array()) {
    $DB_request=$row[0];
    $DB_response=$row[1];
    print "Sending request [$DB_request] to $target...\n";
```

```perl
# 连接到目标，发送请求并获取响应
my @response_from_server = sendraw($DB_request,"\r\n\r\n",target,"80");
```

```perl
# 获取第一行，因为它包含状态码
my $HTTP_code_line = $response_from_server[0];
chop $HTTP_code_line; chop $HTTP_code_line;
print "Response is received [$HTTP_code_line]\n";
# ## 检查响应的第一行是否包含数据库响应
if ($response_from_server[0]) =~ /\Q$DB_response\E/ {
    print "Response matches [$DB_response] from DB!";
} else {
    print "Response does NOT match [$DB_response] from DB...";
}
print "\n";
```

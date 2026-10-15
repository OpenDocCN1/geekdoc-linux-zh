
```perl
&print_header;
dbmopen (%users,"users",0666);
if (!defined($users($fields{'email'}))) {
    print "您输入的电子邮件地址在我们的数据库中不存在。请点击浏览器的后退按钮，修正您的输入并重新提交表单。";
}
else {
    $temp=$users($fields{'email'});

    dbmclose($users);
    $temp=/([a-zA-Z0-9]{5,10})$/;;
    $actualpass=$1;

    if ($actualpass eq '') {
        print "此电子邮箱地址没有输入密码。在输入数据之前，请在此<a href=\"userpassword.html\">这里</a>输入一个。";
    }
}
elsif ($fields{'pass'} ne $actualpass) {
    print "您输入的密码错误。请返回上一个页面并重试。";
}
else {
    &post_data;
}
```

第一个 `if` 语句看起来很熟悉：它是你在列表 3.7 和 3.8 中使用的代码，用于检查用户是否存在于数据库中。如果用户存在，脚本将进入该构造的 `else` 部分。在这里，你想从用户数据中获取密码，而你不需要任何正则表达式即可做到。我们设置了数据，使得密码（如果存在）始终是最后一段数据，你只需要检查字符串末尾是否有 5 到 10 个字母数字字符。此模式被包含在括号中，Perl 赋值 `$1=$actualpass`，然后测试确保没有...

这可以告诉你用户是否输入了密码，或者如果用户没有输入密码，数据字符串将以 "yes" 或 "no" 结尾。由于这两个元素都不匹配你的密码模式，因此，如果 USERS DBM 中没有该电子邮箱的密码，`$1` —— 说 `$actualpass` —— 将为空。

最后，脚本会检查与数据一起输入的密码是否与你存储的密码匹配；如果是，你就可以将数据输入到你的数据库了。

## 绕过 DBM 文件的局限性

尽管 DBM 文件非常强大，但在 Perl 的许多实现中，它们存在一个局限性：每个程序只能调用一次 `dbmopen()`。对于你现在运行的这个应用程序，这个局限性导致了一个问题，因为你倾向于将数据存储在 DBM 文件中

> 提示：你的 Perl 实现允许每个程序进行多次 `dbmopen`。该局限性取决于你的系统使用的 DBM 库版本。如果你的系统拥有 NDBM 库（而不是 GDBM），那你就幸运。如果你的 Perl 解释器是使用这些库编译的，你可以使用多个 `dbmopen` 命令；否则，你就没办法了。要确定你系统使用的 DBM 版本，你需要找到计算机的库并寻找类似于 `LIBDBM.a` 或 `LIBDBGM.a` 的文件。

幸运的是，为了绕过这个局限性：你可以让系统调用另一个 Perl 程序处理这些数据。首先，从临时文件中保存数据，如列表 3.11 所示。

### 列表 3.11 来自 POSTPERIODDATA.PL 的 `post_data` 子程序

```perl
sub post_data {
  $filename=$time.".txt";

  open (f, "scratch/\$filename") || die "could't open file $!";

  print f "email:\$fields{'email'}\n";

  print f "period:\$fields{'period'}\n";

  print f "hours:\$fields{'hours'}\n";

  print f "webhours:\$fields{'webhours'}\n";

  print f "phonehours:\$fields{'phonehours'}\n";

  print f "send:\$fields{'send'}\n";

  print f "receive:\$fields{'receive'}\n";

  print f "uses:\n";
  foreach $use(split(/\/\0/,$fields{'users'})) {
    print f ":\$use\n";
  }

  print f "\n";
  close f;
```

## 第3章 -- 高级处理与数据存储

```perl
system "postdatasup scratch/$filename >> /dev/null";
system("rm scratch/$filename");

print "感谢提交您的数据。";

}
```

该子程序的第一行创建了一个作为文件名的字符串。这个字符串看起来很奇怪，但它具有重要作用。`$$` 是一个特殊的 Perl 变量，代表标识该脚本运行时的进程 ID（process ID-name）。每个运行的进程都有一个进程 ID，且进程 ID 在任何时候都是唯一的。在进程结束后，ID 可以被重用。最后这一事实意味着，为了确保你创建的文件的唯一性，你需要给它盖一个戳。为此，请使用 `time` 函数，它返回自 1970 年 1 月 1 日以来的秒数。

有了唯一的文件名，你需要打开文件。列表 3.1 的第 3 行执行了此任务，在 `SCRATCH` 目录下打开一个具有指定名称的新文件。我创建这个目录是为了使其全局可写：写入供立即使用的临时文件。有一个 `SCRATCH` 目录会非常方便。

打开文件后，脚本将数据打印到文件中，每行一个项目。由于 `uses` 项可能有多个值，它需要更多的处理过程……（注：原文此处存在大量重复的 "it takes a little more processing" 句式，翻译时已根据逻辑精简冗余部分以保持语义流畅）。

```perl
# 这里的逻辑将数据处理为：
```
```perl

($trash,period)=split(/,$file[0]);

($trash,date)=split(/,$file[1]);

($trash,hours)=split(/,$file[2]);

($trash,webhours)=split(/,$file[3]);

```

## 3 -- 高级与数据存储

```perl

($trash, $phonephones)=split(/,$file[4]);

($trash, $send)=split(/,$file[5]);

($trash, $receive)=split(/,$file[6]);

($trash, @uses)=split(/,$file[7]);

$dbfile="$period";

dbmopen (%data, $dbfile, 0666);

$data{email}=join(':', $ours, $webhours, $phonephones, $send, $receive);

$data{email}=".":join(',', @uses);
```

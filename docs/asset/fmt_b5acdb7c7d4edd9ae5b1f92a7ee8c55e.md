
```perl
# 删除注释...
$line = ~ s/\#.*$\//;
# 并跳过空行，包括删除注释后变为空的行
if ($line = ~ /^\s*$/) {
  next;
}
# 开始一个新的标签章节
if ($line = ~ /\([\w\s.\-\]+\)\/) {
  $label = $1;
  $label = ~ tr/A-Z/a-z/;
}
my ($name, $val) = split(/\=/, $line, 2);
$name = ~ s/^\s+//;
$name = ~ s/\s+$/;
$name = ~ tr/A-Z/a-z/;
$val = ~ s/^\s+//;
$val = ~ s/\s+$/;
if ($label eq "") {
  die '所有选项都必须出现在一个章节内，你是否忘记了 [global]？';
}
push @{\$options[$label]}, $val;
}
close(IN);
my $domain = @{$options['global']['domain']}[0];

my @serverTypeNames = keys(%options);

my @serverTypes;
my @required = (
  "name",
  "base",
  "filter",
  "addr",
  "smtpserver",
  "uri",
);
```

# 统一的 Linux 和 Exchange 递送（带反垃圾邮件和反病毒）343

```perl
my %required;

my $r;
for $r (@required) {
  $required($s) = 1;
}

my @scalar = (
  "name",
  "base",
  "binddn",
  "bindpw",
  "filter",
  "attr",
  "smtpserver"
);

my @list = (
  "uri"
);

my $sn;

for $sn (@serverNames) {
  if ($sn eq 'global') {
    next;
  }
  my $s = { };
  my $item;
  for $item (@scalar) {
    if (defined($options($sn){$item})) {
      $$s($item) = @($options($sn){$item})[0];
    }
    if ($Required($item) && defined($s($item))) {
      die "Required option $item missing for $sn";
    }
  }
  for $item (@list) {
    $$s($item) = $options($sn)($item);
    if ($required($item) && !defined($s($item))))
```

# 344 第 6 章 • 实用的 Windows Exchange 和 Linux Postfix 邮件集成

```perl
die "Required option $item missing for $sn";
}
push @serverTypes, $s;
```

# 同时连接 OpenLDAP 和 Active Directory 以创建

# 传输映射，将 Linux 用户的邮件转发到

# 一个目的地，并将 Exchange 用户的邮件转发到另一个。

# 同时构建一个所有有效接收者的组合列表，

# 以于过滤未经请求的垃圾邮件，而无需

# 打扰内部服务器。

```perl
use Net::LDAP;
my $s;
```

```perl
open(RECIPIENTS, '/etc/postfix/recipients.new');
open(TRANSPORT, '/etc/postfix/transport.new');
for $s (@serverTypes) {
  my $ldap;
  my $uri;
  for ($uri (@$$s{'uri'})) {
    $ldap = Net::LDAP->new($uri);
    if ($ldap) {
      last;
    }
  }
  if (!$ldap) {
    die "Could not contact any LDAP URIs for \
$$s{'name'}, \n",
      "为了避免不一致，将不会更新任何映射";
  }
  my $bind;
  if ($$s{'binddn'}) {
    # 以特定用户绑定（简单身份验证）
    $bind = $ldap->bind(
      dn => $$s{'binddn'},
      password => $$s{'bindpw}');
```

# 统一的 Linux 和 Exchange 递送（带反垃圾邮件和反病毒）345

```perl
) else {

  # 匿名绑定

  $bind = $ldap->bind(code);

  if ($bind->code()) {

    die "Bind error:", $bind->code(), "\n",

      "此路径将不会更新映射。";

  }

  my $search = $ldap->search(base = $$s['base'],

    filter = $$s['filter'],

    attrs = $$s['attr']);

  my $entries = $search->count;

  if ($entries < '1') {

    print STDERR "Warning: zero accounts found for $$s['uri'], "\n";

  }

  my $entries = $search->entries;

  my $se;

  for $se (@entries) {

    my $m = $se->get_value($s['attr']);

    # 忽略 Exchange 邮箱

    # 使用 SID 而不是用户名

    if ($m =~ /\/) {

      next;

    }

    my $smtpServer = $$s['smtpserver'];

    print RECIPIENTS "$$$m@domain\n";

    print TRANSPORT "$$$m@domain\tsmtp:$$smtpServer\n";

  }

  # 解绑定

  $ldap->unbind();

}

close(RECIPIENTS);

close(TRANSPORT);

unlink('/etc/postfix/recipients');

rename('/etc/postfix/recipients.new', "/etc/postfix/recipients");

system('/usr/sbin/postmap /etc/postfix/recipients');

unlink('/etc/postfix/transport');

rename('/etc/postfix/transport.new', "/etc/postfix/transport");

system('/usr/sbin/postmap /etc/postfix/transport');
```

# 配置 MailScanner：您的前端反垃圾邮件和病毒能力

`MailScanner` 的工作是使用 `SpamAssassin` 和 `ClamAV` 等程序扫描邮件。当我们配置 `Postfix` 时，我们添加了一条规则将所有入邮件移动到等待队列（hold queue）。我们需要配置 `MailScanner` 提取队列中的邮件，进行病毒扫描，并将干净的邮件返回 `Postfix` 接收队列以递送到 `Exchange` 服务器。

# 为什么我们没有对 MailScanner 使用 Webmin

`MailScanner` `Webmin` 模块目前处于测试阶段，可以在 `http://www.webmin.com` 找到。参考 `MailScanner` 文档 `http://www.debian.org/MailScanner/` 获取更多信息。所有的 `MailScanner` 配置文件都位于 `/etc/MailScanner/` 目录。`MailScanner` 的主配置文件是 `/etc/MailScanner/MailScanner.conf`。我们需要更改的所有设置都可以在这里找到。与其他配置文件类似，`MailScanner.conf` 具有简单的格式：空行和以 `#` 开头的行会被忽略，所有其他行如下：

```
option = value
```

现在我们将检查必须更改的选项。

### 运行用户 (Run As User)

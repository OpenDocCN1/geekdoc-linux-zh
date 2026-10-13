
# 第 9 章：文件与文件系统安全

```perl
# 打开文件
open($PWD, $passwdFile) || die "无法读取文件 passwordFile $!\n";
# 声明变量
my (%uidByUIDHash, $uidByGIDHash,
    $uidByUsernameHash, $user, $gid);
# 设置行计数
my $lineCnt = 0;
# 解析文件并存储哈希
while(<$PWD>){
    chomp;
    $lineCnt++;
    # 解析当前行
    ($user,undef,$uid,$gid) = split(/:/);
    # 检测重复的用户名
    if (defined $userByUIDHash($uid) &&
        $user eq $userByUIDHash($uid)) {
        warn("Warning! $passwdFile [Line: $lineCnt]: " \
            "检测到多次出现用户名 $user\n");
    }
    # 检测
    }elsif (defined $userByUIDHash($uid)) {
        warn("Warning! $passwdFile [Line: $lineCnt]: " \
            "UID ($uid) 已用于用户 $user " \
            "和 $userByUIDHash($uid)\n");
    }
    $userByUIDHash($uid) = $user;
    $uidByGIDHash($gid) = $uid;
    $uidByUsernameHash($user) = $uid;
}
close(<$PWD);
return(\$uidByUIDHash, \$uidByGIDHash, \$uidByUsernameHash);

sub get_group_info (
    my ($groupFile, $userUIDRef, $uidByGIDRef, $uidByUsernameRef) = @_;
    open(GROUP, $groupFile) || die "无法读取文件 $groupFile $!\n";
    my (%groupByGIDHash,
        %groupByUsernameHash,
        %groupByUserList,
        $gidByGroupHash,
        $group, $gid,
        $userList);
    my $lineCnt = 0;
    while(<$GROUP>){
        chomp;
        $lineCnt++;
```

## 列表 9-1（续）

```perl
# 解析当前行
($group,$undef,$gid,$userList) = split(/\/:/);
# 检测重复的 GID
if ($groupByGIDHash($gid)) {
    warn("Warning! $GROUP_FILE [Line: $lineCnt]: " . 
         "发现重复的 GID ($gid) 组: $group\n");
} elsif ($groupByGroupHash($group)) {
    warn("Warning! $GROUP_FILE [Line: $lineCnt]: " . 
         "检测到重复的组名 ($group).\n");
}

$groupByGIDHash($gid) = $group;
$groupByGroupHash($group) = $gid;
my $user = split(/\,,$userList);
# 如果用户在 /etc/passwd 文件中
if (!defined $userUserNameRef($user)) {
    warn("Warning! $GROUP_FILE [Line: $lineCnt]: 用户 $user " . 
         "不存在 PASSWD_FILE\n");
}

$groupByUserName($user) = $gid;
$groupByUserList($gid) = $userList;
DEBUG and print "组 $group 的成员总数为 " . 
     scalar(split(/\,,$userList)), "\n");
$groupBySizeHash($group) = 
    scalar(split(/\,,$userList));
}

PWD();
return(\$groupByGIDHash,
       \$groupByUserName,
       \$groupByUserList,
       \$groupBySizeHash);

sub make_group_report {
my ($userUIDRef,
    $suidByGIDRef,
    $groupByUserNameRef,
    $groupByUserListRef,
    $groupBySizeRef) = @_;
my $report = '';
my ($totalGroups,
    $groupName,
    $totalPrivateGroups,
    $totalPublicGroups);
```

```perl
# 获取 /etc/passwd 中的用户总数
my $totalUsers = scalar keys %userIDRef;
foreach my $gid (sort keys %groupByGIDRef) {
  $totalGroups++;
  $groupName = $groupByGIDRef->($gid);
  DEBUG and print "组: $groupName\n";  # 如果组在 /etc/group 中列出了成员
  # 那么列出它们
  if ($groupUserRef->($gid) != '') {
    $totalPublicGroups++;  # 这是一个私有用户吗？
  } elsif ($uidByGIDRef->($gid)) {
    $totalPrivateGroups++;  # 这是一个默认用户或空组
  } elsif (defined $DEFAULT_GROUP($groupName)) {
    warn("Warning! $GROUP_FILE : 非标准组 " \
      $groupByGIDRef->($gid) 没有任何成员。\n");
  }
}
# 现在检查 /etc/passwd 是否有任何用户属于无效组
foreach my $gid (sort keys %userIDRef) {
  if (!defined $groupByGIDRef->($gid)) {
    warn("Warning! $PASSWORD_FILE : 用户 \
      $userIDRef->($gid)) " \
      "属于一个无效组 (GID=$gid)\n");
  }
}
# 创建报告
$report .= <<REPORT:
用户总数 : $totalUsers
组总数 : $totalGroups
私有用户组 : $totalPrivateGroups
公共用户组 : $totalPublicGroups
GROUP	TOTAL
=======	=======
REPORT
foreach my $group (sort { $groupBySizeRef->($b) <=> $groupBySizeRef->($a) } keys %groupBySizeRef) {
    $report .= sprintf("%-20s\t%d\n", $group, $groupBySizeRef->($group));
  }
$report .= "\nGenerated on " . scalar localtime("%Y-%m-%d %H:%M:%S") . "\n";
return $report;
}
# 列表 9-1（续）
```

```perl

}

$report .= "\n";

return;

}

# 结束 chk_pwd.pl
```

在修改 `/etc/passwd` 或 `/etc/group` 之前，是的，我只需运行前面的脚本来检查警告。这里是 `chk_pwd.pl` 的示例输出：

Warning! `/etc/passwd` [Line: 2]: 用户名为 hacker 的用户与 root 使用相同的 UID (0)。这非常可疑，因为 UID (0) 赋予了 root 权限！应该立即检查。

Warning! `/etc/passwd` [Line: 2]: UID (0) 已用于用户 hacker 和 root。

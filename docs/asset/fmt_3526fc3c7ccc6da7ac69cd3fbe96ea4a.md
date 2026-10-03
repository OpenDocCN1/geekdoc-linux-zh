
```perl
foreach $entr (@entries) {
    print "DN: ", $entr->dn,"\n";
    my $str = ''; my $sep = ',';
    my $attr = ' sort ' $entr->attributes;
    my $attr;
}

# Enumerate array of attributes of DN
foreach $attr (@attrs) {
    #skip binary
    next if ($attr ~ /binary$/);
    print " ", $attr, $entr->get_value($attr);
    "\n"
    $str = $str . $sep . $entr->get_value($attr);
    $sep = ',';
}

$listbox->insert('end', $str);
```

如果用户双击列表框中的某行会发生什么？弹窗将显示为对应用户找到的所有属性。此功能是 `Elsolutions` 计划中的未来增强。这也是读者的一个练习题。提示：传递给 `Net::LDAP::search` 的空属性列表将返回每个搜索命中的所有属性。每个属性可能被格式化为 `hst` 框行。

```perl
#!-
# Detail! display handler. Show detail dialog
# for current list selection
#-
sub display_details (
    # Insert handler code here in future
    print "Display details (todo)...\n";
```

# Elsolutions 的目录策略

| Elsolutions 目录 | |
| :--- | :--- |
| 姓名，电子邮箱，电话 | |
| 输入姓氏： | Bollinger Schagnasty, shag@elsolutions.com, 919 898-1664<br>Ellwood P. Suggins, suggins@elsolutions.com, 919 898-1662 |
| 清除 | 退出 |

图 15-5 以 s 开头的姓氏的实时搜索。

| Elsolutions 目录 | |
| :--- | :--- |
| 姓名，电子邮箱，电话 | |
| 输入姓氏： | Ellwood P. Suggins, suggins@elsolutions.com, 919 898-1662 |
| su | |
| 清除 | 退出 |

图 15-6 缩小后的实时搜索。

让我们运行该程序，假设我们有一个填充好的 `OpenLDAP` 目录，它与位于 `pavilion,bellmeade` 的 `Elsolutions` LDAP 服务器上的搜索基匹配。图 15-5 显示了输入单个 "s" 的结果。显然，`Elsolutions` 只有两个姓氏以该字母开头的人。如果有 10 或 20 个人呢？列表右侧会出现一个垂直滚动条。我们可以滚动到所需人员，或者通过输入目标名称的后续来缩小搜索。

图 15-6 显示了我们的电话簿应用程序，搜索已缩小到姓以 su 开头的人。该应用程序运行在 `Red Hat Linux 7.1` 上。它可以在安装了 `Cygwin` 包的 `Windows XP` 和 `Windows 2000` 上运行。在每台机器上必须获取并安装 `Perl/Tk`，或者更好，将其放在 `Perl @INC` 路径中的响应式 `Linux` 文件共享中。评估结果为在 `Samba` 文件共享上的每台桌面计算机都提供了 `phonebook.pl`。

我们是否在本末倒置了？电话簿条目是如何创建和维护的？我们使用手动构建的 `ldif` 文件来填充目录以测试我们的应用程序，如下所示：

```ldif
dn=Bollinger Schagnasty,dc=bellmeade
objectClass: Person
ObjectClass: organizationalPerson
personalTitle: Dr.
cn: Bollinger Schagnasty
sn: Schagnasty
```

```ldif
description: Primary User
businessCategory: Research
organizationalStatus: Full-time, salary
mail: shag@elsolutions.com
streetAddress: 1501 Soapstone Dr
postalCode: 17794
l: Durham
st: NC
telephoneNumber: 919 898-1664
```

```ldif
dn: cn=Edward Bradford,dc=bellmeade
objectClass: Person
objectClass: organizational
personalTitle: Dr.
cn: Edward Bradford
sn: Bradford
description: Primary User
businessCategory: Research
```

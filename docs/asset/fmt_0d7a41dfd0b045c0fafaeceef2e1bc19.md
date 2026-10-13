
你需要查询三个表：`personinfo`、`projectinfo` 和 `projectmembers`。

从这三个表中，你想生成一个满足以下条件的表：

- `supervisorfirstname` 包含字符串输入（以确保捕获到 Henry，无论他是否大写）。
- 从 `projectmembers` 表收集的 `projectname` 字段与 `projectinfo` 表中的 `projectname` 相同（即 Henry 的项目）。

### 其他有用软件：实用工具

- `personinfo` 表中的 `userid` 字段必须与 `projectmembers` 表中的 `userid` 相同（即所有属于 Henry 项目的 `userid`）。

跟上这些有困难吗？给表画画，并画出查询语句正在发生什么。我本在这里为你提供一张图，但观察线条的绘制比看静态图片要有信息得多，而且我无法在书中包含 QuickTime 视频。

院长本身就是一个葡萄酒鉴赏家，你推断你的查询一定成功了。对结果充满信心，你比她预期的要早得多给了秘书一份列表。

通过对 MySQL 的简短介绍，你正开始发现你将用于该程序的许多巨大潜力。

## 从外部视角看

你已经从用户的视角看到了 MySQL 是什么样的。让我们回到你的视角，即系统管理员的视角。

正如你之前在这个例子中看到的，表定义存储在用户的家目录中；但，正如你在示例中看到的，已经创建了一些数据库。它们在哪里？

看一眼我的目录给了我们一个线索：

```
soykokeake# ls -l /usr/local/mysql/data
drwx------------ 2 root 512 Apr 15 15:57 usertrack
```

这是 `usertrack` 在 MySQL 外部的样子：

```
soykokeake# usertrack
personinfo.ISD      projectinfo.ISD      projectmembers.ISD  userinfo.ISD
personinfo.ISM      projectinfo.ISM      projectmembers.ISM  userinfo.ISM
personinfo.frm      projectinfo.frm      projectmembers.frm  userinfo.frm
```

这对你最终意味着什么？如果你预计 MySQL 将被频繁使用，你可能希望考虑设置单独分区来存储用户的数据库。记住，提供用户执行工作所需的是你的工作。有时，用户的需求和你的需求是重叠的！

现在你已经看到了如何安装以及如何使用 MySQL 软件包的提示，看看你现在系统中的另一个软件部分——编程语言。这两个软件包都代表了 UNIX 上提供的免费软件的巨大力量和用途。尽管我没有空间告诉你这些软件的极小部分，但你应该认为这些不仅是极好的工具，而且是 UNIX 免费软件体验的代表。

![](img/74418f52d5d454acca60721059dbdc99_428_0.png)

410 第14 天

## 使用 Perl

正如你在 MySQL 之旅中看到的，你可以编写 Perl 脚本作为 MySQL 数据库的接口。现在看看用于向数据库输入数据的 Perl 代码。

事实上，我的程序员编写了一个恰好执行此操作的脚本。代码如下：[此处OCR文本非常混乱，无法重构一个功能性脚本，但结构遵循数据输入的流]。

412

第 14 天

# 现在我们需要将州名和邮政编码分离 - 使用

# 空格。注意它前面有一个领先空格，所以

# 结果是 [[state][zip]

@moresplitaddress = split(/\s+/, $splitaddress[1]);

$state = $moresplitaddress[1]; $zip = $moresplitaddress[2];

# 将名字拆分成单个字符，以创建一个字母的

# 数组。使用名字的第一个字符和姓氏的全部来构建潜在的 用户名。在 Perl 中，点号是连接运算符。

@nameletters = split('', $firstname);

$UserId = $nameletters[0].$Lastname;

# 将 userid 转换为全小写

$userid =~ tr/[A-Z]/[a-z]/

翻译命令（`tr`）与替换命令（`substitution`）非常相似。语法相似，

但翻译命令是一多对多的替换，而替换命令是查找

 模式并将其替换为其他模式。

# 确保派生的 userid 符合用户

# 输入数据的情况

print "Built userid ",$UserId,"in\n";

print "Is this OK? (Y/N) : ";

$getok = <STDIN>;

chomp($getok);

if ($getok ne "Y") {

注意使用错误的比较命令。Perl 实际上并不在乎你对任何数据

# 使用字符串比较还是数值命令 `!=`。

它会运行，但只有其中一个会生效。Perl 有点烦人，因为它会乐呵呵地将

 字符串当作整数进行比较并给出奇异的结果，而不是

报告错误并退出。

注意，Perl SQL INSERT 命令的语法与你在命令行上

输入时几乎完全相同。你不需要像下面那样整齐地包装它。顺便说，这种为了显示的良好格式化可能会减慢速度。

### 其他有用软件：实用工具

```perl
# 执行 SQL 数据库插入
$dbh->do('INSERT INTO personinfo
  SET firstname=$firstname, lastname=$lastname,
  address1=$addressline, address2=$addressline2,
  city=$city, state=$state, zip=$zip,
  phone=$phoneno,userid=$userid');
```

关于 Perl 的笔记：当你第一次使用一个变量时，Perl 会创建这个并不存在的变量。

这看起来像是一种便利，但事实证明这会让调试变得非常困难。例如，

如果你忘记了使用了变量 `$phoneno`，而认为你已经调用过 `$phone`，那么之前的 Perl 语句和 SQL INSERT 就会正常执行。

不会有错误报告，也不会有投诉或警告。

你发现出问题的唯一证据就是当你回头

手动查看数据库时，你会发现该字段是空的。

Perl 会注意到你之前使用过的 `$phone` 变量，并为你创建它，然后热心地使用这个空处变量将它的那部分数据存入数据库。

```perl
print 'Is this user attached to a project? (Y/N) ';
$getok = <STDIN>;
chomp($getok);
if ($getok eq "Y") {
 # eq 是 Perl 中表示字符字符串“相等”的方式
 # == 是数值值的语法。
 # 注意，如果你在 if
 # 语句中误用 "=" 代替 "=="，
 # 你实际上是在进行赋值，并根据“被比较”值
 # 赋值的成功与否来评估 if 语句的结果！
```

如果你写了一个 Perl 比较语句，由于某种原因，无论参数值如何，它始终求值为为真，那么可能是因为你在比较中使用了 `=` 代替 `==`。

这让你的比较变成了一次赋值。它几乎总是会成功，导致比较结果为真，并同时

 搞乱了你的变量。

```perl
# 构建 SQL 查询
$sql=$dbh->prepare("SELECT projectname, supervisorfirstname,
  supervisorlastname FROM personinfo");

$sql->execute();
```

```perl
# 在多维数组中获取结果
$allproj=$sql->fetchall_arrayref;
```

```perl
# 清理工作
$sql->finish();
```

SELECT 语句通过多个 Perl 语句来处理。注意，其语法

再次与你之前在交互式解释器中使用的几乎完全一样。

SELECT 的结果被返回到一个 Perl 数组数组（array of arrays），你可以随所欲地处理它们。

```perl
# Perl Perl "for" 语法之一 - 遍历返回的每个条目
for $i (0..#${allproj})
{
    print "Project ",$i,", $allproj->[$i][0];
    print "\n Supervised by ",$allproj->[$i][1],";";
    print "\n, $allproj->[$i][2],\n";
}
print "Please pick a project (0-",#${allproj})," : ";
```

那个旧的语法 `${variable}` 用于计算数组中的条目数。

$getok=<STDIN>;

chomp(getproj);

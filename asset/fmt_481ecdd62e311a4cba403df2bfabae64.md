
```perl
#!/usr/bin/perl
#
# 导入 DBI 模块。
#
use DBI;

# 创建连接并检查错误。
#
my $dsn = 'dbi:dbname=postgres';
my $user = 'postgres';
my $pass = '';
my $dbh = DBI->connect($dsn, $user, $pass);
unless (defined $dbh) {
    die DBI::$errstr;
}

# 不要自动打印每个错误。
# 我们将检查它们。
$dbh->{PrintError} = 0;

# 创建准备语句。
#
my $sth = $dbh->prepare("INSERT INTO contact (first_name, last_name, company) VALUES (?, ?, ?)");

# 使用准备语句插入三行。
#
$sth->execute('Brian', 'Jones', 'Company') or die DBI::$errstr;
$sth->execute('Oscar', 'Smith', undef) or die DBI::$errstr;
$sth->execute('Lotus', 'Banks', 'Company') or die DBI::$errstr;

print "The data was inserted.\n";

# 关闭连接。
#
$dbh->disconnect();
```

运行此示例，请切换到包含第 12 章示例的目录。然后运行命令 `prepared.pl`。

## 处理结果集 (Processing Result Sets)

`DBI` 从数据库获取数据非常灵活。要执行查询并处理结果，你应该采取以下步骤：

1. 使用 `prepare()` 创建句柄，并使用 `execute()` 执行语句。
2. 获取结果集中的每一行。
3. 调用 `finish()` 方法。

### 准备与执行 (Prepare and Execute)

使用 `prepare()` 方法获取句柄，然后使用 `execute` 方法执行语句：

```
$sth = $dbh->prepare("SELECT * FROM contact") or die DBI::$errstr;
$sth->execute() or die DBI::$errstr;
```

### 获取行 (Fetch the Rows)

接下来，你可以使用以下句柄方法之一获取结果集：

- `fetch_array()`：作为值数组获取下一行：

```
while (@values = $sth->fetch_array()) {
    my ($first, $last, $company) = @values;
    print "$first $last works for $company.\n";
}
```

- `fetch_arrayref()`：这以数组单一引用值获取下一行。`DBI` 文档说这是获取数据最快的方法：

```
while (@array_ref = $sth->fetch_arrayref()) {
    my ($first, $last, $company) = @array_ref;
    print "$first $last works for $company.\n";
}
```

- `fetch_hashref()`：这使用列名作为键，作为值的哈希获取下一行。虽然非常方便，但性能不如其他替代方案：

```
while (my $row = $sth->fetchrow_hashref) {
    foreach $column (keys %row) {
        print "Column $column: $row{$column}";
    }
}
```

- `fetchall_arrayref()`：作为引用数组获取结果集中的所有行。数组的每个元素都是行的引用：

```
my $rows = $sth->fetchall_arrayref();
foreach ($array_ref (@rows)) {
    my ($first, $last, $company) = @array_ref;
    print "$first $last works for $company.\n";
}
```

在数组中，`NULL` 值表示为未定义（undefined）。

### 完成 (Finish)

在使用结果集后，你应该调用 `finish()` 方法：

```
$sth->finish();
```

### 整合 (Putting All Together)

接下来的示例完成了所有步骤（准备、执行、获取行）。由于许多数据库返回带有填充的值（空格会填充到列的最大尺寸），我们正在使用正则表达式来清理 `fetch_array` 返回的值。我们还检查行是否包含未定义的值。如果是，则跳过该人员。我们必须在使用替换清理数据之前进行此检查。以下是示例 (`select.pl`)：

```perl
#!/usr/bin/perl
#
use DBI;

# 创建连接并检查错误。
#
my $dsn = 'dbi:dbname=postgres';
my $user = 'postgres';
my $pass = '';
my $dbh = DBI->connect($dsn, $user, $pass);
unless (defined $dbh) {
    die DBI::$errstr;
}

# 不要自动打印每个错误。
# 我们将检查它们。
$dbh->{PrintError} = 0;

# 步骤 1. 创建一个从 contact 表获取所有行的语句，并执行该语句。
my $sql = "SELECT first_name, last_name, company
FROM contact";
$sth = $dbh->prepare($sql) or die DBI::$errstr;
$sth->execute()
or die DBI::$errstr;

# 步骤 2. 获取所有结果。
while ($values = $sth->fetchrow_array()) {
  # 只列出有公司的人。如果
  # company 为 NULL，跳过该人员。
  unless (defined $values[2]) {
    next;
  }

  # 移除每个数组元素的末尾空格。
  grep(/\s+$/, "", @values);

  my ($first, $last, $company) = @values;
  print "$first $last works for $company.\n";
}

# 步骤 3. 完成语句。
$sth->finish();

$dbh->disconnect();
```

在类类模块中，`Perl/Tk` 是 Perl 中最成熟、最流行且跨平台的用户界面模块。该类中还有其他出色的用户界面模块，例如 `Gtk` 和 `PerlQt`。事实上，你甚至可以使用流行的 UI 构造器 `glade` (`http://glade.gn.org`) 为 Perl 和 `Gtk` 构建用户界面。第 13 章“`GNOME`”从 C 程序员的视角查看了 `Glade`，但那里的信息对于想要将 Perl 配合 `Glade` 的人将非常有用。

## Perl/Tk

`Perl/Tk` 是一组面向对象的模块，它将 `Tk` 工具包引入了 Perl。`Tk` (`www.scriptics.com`) 是随 `Tcl` 语言分发的图形用户界面工具包。`Perl/Tk` 基于 `Tcl/Tk` 分发版的源代码，但它不需要预先安装 `Tcl/Tk` 即可运行。

你可以使用 `Perl/Tk` 开发具有复杂图形用户界面的应用程序。`Perl/Tk` 具有直观的面向对象语法用于构建界面，并包含了一系列供你在应用程序中使用的图形组件。

### 安装 Perl/Tk

`Perl/Tk` 分发版包含在 `CPAN` 上的 `Tk` 归档中。在本章中，名为 `CPAN` 的部分解释了如何使用 Perl 安装可选模块。使用这些指令安装 `Tk`，这是一个包含许多与 `Perl/Tk` 相关模块的大型归档。要获取 `Perl/Tk` 的文档，你应该在 shell 提示符处执行此命令：

```
perldoc Tk::UserGuide
```

你可能觉得查看交互式组件演示很有趣。这个演示包含在一个名为 `widget` 的脚本中，安装在 `/usr/bin` 或 `/usr/local/bin` 下。通过登录 X 并在 shell 提示符中使用 `widget` 命令来运行此脚本。由于你可以带有源代码查看演示，因此 `widget` 演示是一个强大的学习工具。

### 创建简单表单

与其他许多用户界面工具包一样，`Tk` 按层次结构排列组件。顶层窗口包含所有组件，如按钮、文本字段和框架。某些组件（如框架）可以包含其他组件。第 11 章“`Java, Swing and JDBC`”中的图 11.2 显示了 `Java Swing` 中组件的层次排列。该模型同样适用于 `Tk`。

要创建一个基本的 `Tk` 应用程序，你需要执行以下操作：

- 1. 使用（导入）`Tk` 模块：

```
use Tk;
```

- 2. 创建一个主窗口。使用 `-title` 属性指定窗口标题：

```
my $main = MainWindow->new(-title => 'Tk Demo');
```

- 3. 向窗口添加一个框架。使用该框架持有组件。要创建一个框架，调用主窗口的 `Frame()` 方法。然后你必须调用 `pack()` 方法以确保框架被正确地打包到窗口中：

```
my $top = $main->Frame();
$top->pack();
```

你可以通过包含 `-side` 属性来指定让 `pack()` 锚定框架的位置：

```
$top->pack(-side=>'top');
```

下一段代码创建了两个框架——第一个锚定在窗口顶部。第二个框架锚定在窗口右侧，并出现在第一个框架之前侧：

```
my $top = $main->Frame();
my $bottom = $main->Frame();
$top->pack(-side=>'top');
$bottom->pack(-side=>'right');
```

- 4. 向框架添加组件。在 `Perl/Tk` 中，向任何事物添加组件都非常简单。就像我们通过调用窗口的 `Frame()` 方法向窗口添加框架一样，你可以通过调用框架的 `Label()` 方法向框架添加文本标签：

```
my $label = $top->Label(-text => 'Name:');
$label->pack(-side=>'left');
```

如果你不计划引用你创建的对象，可以调用 `pack()` 方法来创建该对象（尽管在复杂的表单中，这可能会迅速变得不可读）。我们将其称为**匿名组件**（与前述代码所示的命名组件相比：

```
$top->Label(-text => 'Name:')->pack(-side=>'left');
```

你可以将命令与某些组件（如按钮）关联。要创建一个命令，在创建对象时设置 `command` 属性。当按下 `Cancel` 按钮时，这将销毁主窗口，从而终止应用程序：

```
my $btn = $bottom->Button(-text => 'Cancel',
-command => [$main->destroy]);
$btn->pack(-side=>'left');
```

你还可以创建调用子程序的命令。注意这里我们还引用了输入字段的命名实例。`say_hello()` 子程序可以调用 `$entry->get()` 获取当前值：

```
$bottom->Button(-text => 'OK',
-command => sub { say_hello($entry) }
)->pack(-side=>'left');
```

- 5. 当你添加了所有组件后，将 `Tk` 放入其主循环。此时，你将控制权交给 `Tk`，直到主窗口被销毁。这里是启动主循环的命令：

```
MainLoop;
```

### 构造函数

当你创建一个对象时（例如 `$top->Label`），你实际上是在调用对象**类型**的构造函数。由于你通过另一个对象（例如框架）调用它，你也将将其与该对象关联。

### 属性

传递给构造函数的属性（如 `-text`、`-command` 等）。

要使用此小部件（widget），你至少应该指定以下属性：

- `-label`（一个说明性提示）、`-choices`（指向可能选项数组的引用）以及 `-variable`（用于绑定选择的变量）。以下是一个示例，它在 `@choices` 数组中提供了选项，并将 `@choices` 中的第一个元素作为默认值：

```perl
$my @choices = ('One', 'Two', 'Three');
my $choice = $choices[0]; # 默认选择第一个选项。
$main->BrowseEntry(
  -width => 25,
  -variable => \choice,
  -label => 'Tk::BrowseEntry ',
  -choices => @choices
)->pack();
```

`Tk::Entry`。一个简单的文本输入框。你至少应该指定 `-textvariable` 属性（要绑定的变量）。这里有一个示例：

```perl
$main->Entry(-width => 8,
  -textvariable => \text
)->pack();
```

你还可以使用 `-show` 属性来指定用户在字段中输入字符时显示的字符。这会覆盖掉他们实际输入的内容，对于隐藏密码输入非常有用（在图 12.3 中，该字段包含一串星号）：

```perl
$main->Entry(-width => 8,
  -textvariable => \pass,
  -show => '*'
)->pack();
```

`Tk::Button`。一个可以与之关联操作的推入按钮。你至少应该指定 `-text`（按钮标签）和 `-command`（操作）属性。命令可以是指向列表的引用（使用 `[ ]` 分隔符），该列表包含一组组件/消息的值对。第一个值是一个组件（例如顶层窗口），第二个值是你想要发送给该组件的消息，例如 `destroy`（销毁）：

```perl
$main->Button(-text => 'Tk::Button (Close)',
  -command => sub { $main->destroy() }
)->pack();
```

命令可以是你想执行的代码的引用。实现此目标的一种方法是使用 `sub { ... };` 创建一个匿名子程序。

```perl
$main->Button(-text => 'Tk::Button (anon subroutine)',
  -command => sub { print "Hello, World.\n" }
)->pack();
```

# 第 12 章

但你也可以使用 `&` 前缀来创建指向现有子程序的引用：

```perl
sub hello {
    print 'Hello, World from hello().\n'
}
$main->Button(-text => 'Tk::Button',
            -command => \&hello
    )->pack();
```

`Tk::Frame` 一个用于存放其他组件的组件。框架会增长以适应你放入其中的任何内容。有用的属性包括 `-relief`（起、凹、平、实、脊、槽）和 `-borderwidth`（以像素为单位的宽）。这里有一个包含按钮的 `Frame`：

```perl
my $frame = $main->Frame(-relief => 'groove',
            -borderwidth => 3
    )->pack();
```

```perl
$frame->Button(-text => "I'm in a Frame")->pack();
```

`Tk::Label`。一个简单的文本标签。你至少应该包含 `-text`（标签文本）属性：

```perl
$main->Label(-text => "I'm a Label!")->pack();
```

`Tk::Scrolled`（图 12.3 未显示）。一个滚动小部件。它的用法与其他小部件略有不同。你可能认为先创建一个滚动小部件，然后向它添加组件。相反，你应该将小部件名称传递给 `Scrolled` 的构造函数，如下：

```perl
$top->Scrolled('Pane');
```

你可以使用 `-scrollbar` 属性指定滚动条的位置。使用方向点作为 `n`（北）、`s`（南）、`e`（东）和 `w`（西）。你可以在任何方向点前加缀 `o`，这表示滚动条仅在需要时才显示（即小部件大于封装窗口）。这创建了一个在西部（左侧）有滚动条、南部（底部）有可选滚动条的滚动面板，几何形状为 200x200：

```perl
$top->Scrolled('Pane',
            -scrollbars => 'ose',
            -height => 200,
            -width => 200)->pack();
```

## 在网格中显示数据

当你有很多表格数据时，以网格格式显示它们非常有用。虽然这不是展示数据最优雅的方式，但许多用户都很熟悉，因为它遵循电子表格和许多打印报告的格式。如果你正在寻找一种探索数据的方法，特别是适用于分层探索的数据，你应该查看以下章节，其中数据以树状格式进行探索。

让我们看看 `Tk::Columns` 模块，它不允许你编辑网格的内容，但对于显示只读网格来说非常好用。如果你需要创建一个可编辑的网格，应该查看 `Tk::Table`。然而，使用 `Tk::Table` 创建的大型表格可能会消耗大量内存。

`Tk::Columns` 不是标准 `Perl/Tk` 分发的一部分。它包含在 `Tk::DKW` 分发中，你可以按照 `CPAN` 章节中描述的方法进行安装。如果你使用 `CPAN` 工具，只需要求它安装 `Tk::Columns`，它会自动识别出它是 `Tk-DKW` 的一部分。

## 使用 Tk::Columns


```
01 Sub InsertSnippet()  
02 Dim Library As Object  
03 ThisDoc=ThisComponent  
04 TextSnippet=ThisDoc.getCurrentController().getSelection().getByIndex(0).getString()  
05 Database=ConnectToDatabase("snippets")  
06 TextSnippetSanitized = Join(Split(TextSnippet, "'"," ''),"""")  
07 SQLQuery="INSERT INTO "snippets" " + "("snippet") VALUES "  
08 + "("'" + TextSnippetSanitized + "')"  
09 SQLStatement=Database.createStatement()  
10 Result=SQLStatement.executeQuery (SQLQuery)  
11 Database.close  
12 Database.dispose()  
13 MsgBox ("Text snippet has been saved.",64,"Result")  
14 End Sub  
15  
16 Function ConnectToDatabase(DBName As String) As Object  
17 Dim DatabaseOpt() as new com.sun.star.beans.PropertyValue  
18 DBContext=createUnoService("com.sun.star.sdb.DatabaseContext")  
19 On Error GoTo ErrEnd1:  
20 DataSource=DBCttext.getByName (DBName)  
21 ConnectToDatabase=DataSource.getConnection ("","")  
22 DatabaseFile = DataSource.DatabaseDocument  
23 DatabasePath = DatabaseFile.URL  
24 DatabaseOpt(0).Name = "Hidden"  
25 DatabaseOpt(0).Value = True  
26 DatabaseFile = StarDesktop.loadComponentFromURL(DatabasePath, "_blank",0, DatabaseOpt())  
27 Exit Function  
28 ErrEnd1:  
29 MsgBox("Failed to establish a database connection.",16, "Error"):End  
30 End Function
```

#### 结语

这些示例只是你可以使用 `LibreOffice Basic` 完成的众多功能中的寥寥几项。即使这些相对简单的宏，也包含多个你可以在自己的脚本中轻松重用的构建模块。当然，编码的乐趣不必止步于此。虽然 `LibreOffice Basic` 不像许多其他流行的编程语言那样灵活和强大，但它可以处理你扔给它的几乎所有与 `LibreOffice` 相关的任务。因此，一旦你掌握了它的基础，就可以释放 `LibreOffice` 生产力套件的全部潜力。

#### 信息

- [1] **LibreOffice Shell 函数：** https://help.libreoffice.org/7.0/en-US/text/basic/shared/03130500.html

- [2] **Amazon S3：** https://aws.amazon.com/s3/

- [3] **GitHub 上的 AWS Perl 脚本：** https://github.com/timkay/aws

### 通过数字档案整理你的书架

通过我们的数字档案捆绑包，完善你的 *Linux Magazine*（《Linux 杂志》）和 *ADMIN Network & Security*（《ADMIN 网络与安全》）收藏。

你将获得一整年的 *期刊*，以 *PDF 格式* 提供，可以随时在任何设备上访问。

![](img/e39350c3a7c0d527d71b0e4097a0ba66_64_0.png)

bit.ly/2019-Digital-Archives

## 提升生产力

### LibreOffice 排版

#### 在 LibreOffice Writer 中设置文本

#### 类型转换

![](img/e39350c3a7c0d527d71b0e4097a0ba66_65_0.png)

`LibreOffice Writer` 是一个实用的桌面排版工具，其排版功能比大多数用户想象的要多得多。*文 / Bruce Byfield*

多年前，Sun Microsystems 的员工 Elizabeth Mathias 给我讲了一个关于 StarOffice 的故事，这个专有程序后来变成了 OpenOffice.org，再后来变成了 LibreOffice 和 Apache OpenOffice。根据 Mathias 的说法，当 Writer 模块在几十年前最初开发时，程序员们被告知必须使用它来记录他们的工作。结果，他们确保 Writer 不仅仅是一个文字处理器，也是一个排版程序——这惠及了世界各地的自由软件用户。事实上，尽管功能并不完备，但 Writer 的功能足够先进，以至于几乎不应被视为纯粹的文字处理器。

诚然，Writer 的功能往往未被注意到。如果你手动格式化，你可能会完全不知道这些功能。即使你使用样式，可能也没有完全注意到它们。事实上，尽管功能并不完备，但 Writer 的功能足够先进，以至于几乎不应被视为纯粹的文字处理器。

然而，如果你想要增强文档，工具就在等待着你。以页样式中设置页眉的工具为例（图 1）。一旦开启页眉，你只需选择*左右内容相同*和*首页内容相同*，即可设置好页眉。

如果你想要更多的控制权，可以设置页眉与正文不同的边距（*左边距* 和 *右边距*）；调整页眉底部与正文之间的间距，使其固定（*间距*）或可变（*使用动态间距*）；或者将页眉高度设置为固定（*高度*）或可变（*自动调整高度*）。

此外，这只是第一个选项卡。点击*更多*按钮，你可以给页眉添加边框，或用信号线将其与正文分隔开，同时设置*样式*、*粗细* 和 *颜色*，以及边框或框与页眉内容之间的距离。你甚至可以自定义阴影以添加 3D 效果，除非你想要那种复古的 90 年代风格，否则我不建议使用该功能（图 2）。

![](img/e39350c3a7c0d527d71b0e4097a0ba66_66_0.png)

*Writer* 中可用的每个功能都是如此。页边距、表格、文本环绕、目录以及上标和下标字母——几乎每个方面都拥有你可以想象到的众多选择。有时，你可能需要一些技巧来获得你想要的精确布局，但实际的限制很少。例如，你不能创建一个从 10 倒数的列表样式，但手动添加一个是极少且轻微的麻烦罢了。

#### 行距、字距调整和非连接法

Writer 的 *自定义工具* 包含许多仅在排版程序中发现的功能。与大多数文字处理器一样，*Writer* 提供默认的行距，可以是单倍行距或双倍行距，对于许多字体来说效果尚可。然而，对于许多字体，这种默认设置会使文本显得太浅或太深。当这种情况发生时，*Writer* 提供了替代方案：点击*缩进和间距 | 行距 | 固定*，以便像专业出版人员那样精确调整行距，以百分之一的磅（或 1/720 英寸）为增量（图 3）。

![](img/e39350c3a7c0d527d71b0e4097a0ba66_66_1.png)

更好的是，如果你希望对调整拥有完全的控制权，你可以创建一个使用*格式 | 字符 | 位置 | 间距至* 来微调字符间距的字符样式，增量为二十分之一的磅（即 1/720 英寸）。完美主义者甚至可以为不同的字母组合创建单独的字符样式。

唯一的麻烦是，当你完成编辑和修订时，非连接法（连字符断字）不再是最佳结果。幸运的是，如果你安装了用于你所用语言的非连接法字典，你可以点击*工具 | 语言 | 非连接法* 来检查文档的非连接法，将连字符定位在你想要的位置（图 6）。如果仍有不佳的非连接法断点，你可以通过按 Ctrl + -（减号）手动插入断点，或者通过在*工具 | 选项 | 语言设置 |* 中列出单词以防止断字。

![](img/e39350c3a7c0d527d71b0e4097a0ba66_66_2.png)

## 提升生产力

### LibreOffice 排版

![](img/e39350c3a7c0d527d71b0e4097a0ba66_67_0.png)

图 5：连字符控制功能可以改善文档的外观。

写作辅助工具。请注意，除非该段落的样式设置了连字符范围且单词落在该范围内，否则这两个手动工具都无法发挥作用。

**连字符**工具非常有用，LibreOffice 用户应该养成在每个文档拼写检查后立即下载使用该工具的习惯。



```c
$result = mysql_query("select * from testwebsite");
while($row = mysql_fetch_array($result))
{
    echo "<tr>";
    echo "<form><input type='hidden' name='MODE' value='UPDATE'>";
    for($i=0;$i < mysql_num_fields($result); $i++)
    if($i!=0)
        echo "<td><input type=hidden name=" .
            mysql_field_name($result,$i) . "' value='" .
        $row[mysql_field_name($result,$i)] .
        "'>" .
        "</td>";
    else
        echo "<td><input type=text name='" .
            mysql_field_name($result,$i) .
        "' value='" .
            $row[mysql_field_name($result,$i)] .
        "'></td>";
    echo "<td><input type='submit' value='edit'></form>";
    echo "<a href='?ID=" .
        $row[mysql_field_name($result,0)] .
        "&MODE=DELETE>delete</a>";
    echo "</td></tr>";
}
mysql_free_result($result);
mysql_close($con);
```

如您所见，大量枯燥且重复性的工作已得到自动化。您可以着手修改 PHP 代码推进项目，或者深入底层去自定义生成所有这些代码的 C 程序。

我个人经常使用 ghost 来节省建站时间，这也是我编写它的初衷。我厌倦了反复编写几乎完全相同的代码来解码 HTML 表单以及填充或更新数据库。

## 12 结语

在您研读完这些简单的示例后，我希望您能意识到，掌握 C 语言始终是一项有用且持续具有实用价值的技能。

25 年过去了，我仍会定期编写 C 程序以快速且高效地完成日常任务。一旦编写完成，这些程序就会成为一套适合我使用的持久工具库的一部分，并且具备可移植性。

这本简短的书包含了我多年来学到的许多“技巧”，关于这些技巧几乎没有明确的文档记载，且坦率地说，它假定读者熟悉 Linux。在针对各种经验水平不同的学生测试了这些内容后，我相信一位专注且细心的学生能够成功运行所有这些材料，并以此为起点，发现 C 语言的乐趣。我的许多学生都说，“这比 Java 有趣多了，我能看清真正发生了什么！”这令我最感欣慰，也让我确信您会发现这些内容很有用。

感兴趣的读者可能会要求出版社委托我撰写一本配套书籍：

**Linux 下的 C++ 标准模板库编程**

祝好运，编程愉快。

David

2009 年 3 月 31 日


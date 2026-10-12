
示例 14-3（添加了行号以便清晰展示）展示了一个 `tw.config` 文件，其中包含表 14.3 中所示的部分参数。此示例仅用于说明目的，不打算实际使用。一个现实的示例在第 393 页的示例 14-4 中提供。在示例 14-3 的第一部分中，我们可以看到使用 `@@define` 创建新模板 `READ` 和 `ALL`（第 3 行和第 5 行）。这些模板随后在第 41、42、50 和 51 行中使用。

### 表 14.3 Tripwire 配置文件预处理器语法

| 参数 | 描述 |
| :--- | :--- |
| `@@ifhost *hostname*` | 如果 *hostname* 必须与 `uname -n` 或 *hostname* 的输出完全匹配，则为真。如果为真，则在此条目之后且在任何 `@@endif` 或 `@@else` 条目之前的所有条目都会执行。 |
| `@@ifnhost *hostname*` | 与上述相同，但仅当 *hostname* 未与 `uname -n` 或 *hostname* 的输出完全匹配时为真。 |
| `@@else` | 提供条件 else 语义，用于与 `@@ifhost`、`@@ifnhost`、`@@ifdef` 或 `@@ifndef` 配合使用。 |
| `@@ifdef *variable*` | 如果 *variable* 已定义，则为真。 |
| `@@ifndef *variable*` | 如果 *variable* 未定义，则为真。 |
| `@@endif` | 结束前面的 `@@if*` 语句。 |
| `@@define *variable string*` | 将 *string* 赋值给 *variable*。如果没有给出 *string* 参数，则分配空 *string*。 |
| `@@undef *variable*` | 取消分配 *variable*。 |
| `@@include *pathname*` | 将通过 *pathname* 指定的文件包含到此文件中。被包含的文件必须使用相同的配置语法。 |
| `@@*variable*` | 展开为存储在 *variable* 中的 *string*。 |
| `@@(*variable*)` | 与上述相同。通常，这种语法与其他 *strings* 配合使用，类似于 shell。 |
| `\|\|` | 逻辑或语义。 |
| `&&` | 逻辑和语义。 |

### 示例 14-3 Tripwire 配置文件中的预处理器语法

```
1.  # Create our own templates
2.  # Use 7&8 instead of 1&2
3.  @@define READ R/7:8:12
4.  # Sometimes we want almost everything
5.  @@define ALL N-034569
6.  #
7.  # Initial definitions for Operating Systems
8.  @@ifhost eagles || miners || ravens
9.  @@define SOLARIS
10. @@endif
11. #
12. @@ifhost peru || egyt || maya || inca
13. @@define IRIX
14. @@endif
15. #
16. # If not one of the above hosts, then Linux
17. #
18. @@ifndef SOLARIS
19. @@ifndef IRIX
20. @@define LINUX
21. @@endif
22. @@endif
23. #
24. # Now start processing fingerprints
25. #
26. # Special file for Linux
27. @@ifdef LINUX
28. @@include /usr/local/ro/etc/tw.config.linux
29. @@else
30. # Stuff common to IRIX and Solaris
31. ./ L # may not exist
32. ./rhosts R # may not exist
33. ./profile R # may not exist
34. ./cshrc R # may not exist
35. ...
36. <lots of common stuff deleted>
37. ...
38. @@endif
39. # IRIX specific
40. @@ifdef IRIX
41. /usr/etc @@ALL
42. /var/ns @@READ
43. ...
44. <lots of stuff deleted>
45. ...
46. @@endif
47. # Solaris specific
48. #
49. @@ifdef SOLARIS
50. /usr/ucb @@ALL
51. /var/sadm @@READ
52. ...
53. <lots of stuff deleted>
54. ...
55. @@endif
```

在该文件的下一部分中，我们确定 Tripwire 正在哪个主机上运行。第 8 行和第 12 行使用 `@@ifhost` 检查特定主机，每个都使用了逻辑 `OR` (`||`) 功能。如果这两个情况中有一个匹配，我们将一个变量设置为空字符串。在这种情况下使用空字符串是因为该变量的值永远不会被使用；我们只关心它是否被设置。这最初在第 18 行和第 19 行中体现，在那里我们测试 `IRIX` 或 `SOLARIS` 是否已设置；如果没有，我们将 `LINUX` 变量设置为空字符串，表示主机正在运行 Linux。

随后，文件中使用的条件语句——具体在第 27、40 和 49 行——都是基于哪个变量被设置而定的。请注意，我们在 Linux 情况下使用一个完全独立的文件，并在第 28 行通过 `@@include` 包含该文件（请注意也使用了文件系统 `/usr/local/ro`，意味着只读；这将在第 398 页的 *Storing the Database* 中进一步讨论）。使用预处理器语法，你可以以多种方式配置此文件，使其在许多不同的系统上运行。

### 有效构建 Tripwire 配置文件

你可能已经发现，正确设置此文件对你的系统安全至关重要。与此文件相关的问题有三个。

1. 语法必须正确。
2. 配置文件或文件必须得到保护。
3. 所有关键文件和目录都需要被指纹化。

#### 正确的语法

关于语法，有一些帮助。在 Tripwire 源代码目录中，你会发现一个名为 `contrib` 的子目录。那里有一些 `README` 文件以及几个实用程序，其中之一是 `CheckConfig`。你可以使用 `CheckConfig` 脚本检查你的 Tripwire 配置文件或文件的语法。基本上，它确保你指定的文件和目录存在，并在遇到符号链接时通知你。当然，它无法告诉你应该如何使用 Tripwire！其使用的语法示例如下：

```
# CheckConfig -v /usr/local/ro/etc/tw.conf.linux
```

`CheckConfig` 脚本不理解预处理器语法。幸运的是，`tripwire` 命令有一个选项 `(-D)`，它会导致解析预处理器信息并生成一个配置文件（默认发送到标准输出）。因此，如果你正在使用预处理器命令，你可以通过执行以下命令来检查文件的语法：

```
# tripwire -E -C /usr/local/ro/etc/tw.conf.linux | CheckConfig -v
```

如果有任何预处理器语法错误，它们将由 Tripwire 报告。

### 安全存储

我们在第 398 页的 *Storing the Database* 中注意到，最好将 Tripwire 数据库存储在可移除只读介质上，例如 CD。我们还讨论了除了这种存储方式，或者在无法使用可移除介质的情况下，对此数据库进行加密的问题。不仅数据库应该被安全存储，*tripwire* 程序和配置文件也需要安全存储，因为如果它们保持可写状态，也可能被篡改。理想情况下，它们通常也不应该可读，因为这允许截获者获取有关你配置和 Tripwire 使用的宝贵信息。

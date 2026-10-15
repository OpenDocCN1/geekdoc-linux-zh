
表达式规则（第 34–42 行）定义了可能的各种表达式（右侧值）。我们考虑了四种可能性：数字、另一个变量、变量与数字之和或差值。运算符规则（第 45–49 行）涵盖了合法的两种运算符（由 `OP_MINUS` 定义的 `-` 或由 `OP_PLUS` 定义的 `+`）。此解析的目标（由我们插入语法的代码定义）是识别格式正确的 Bison 语法。格式良好的 Bison 语法用机器可读的 Backus-Naur 形式（BNF）表示。BNF 是一种用于表示上下文无关语法的正式语法，是表示计算机语言语法的常用符号。

# 将词法分析器挂钩到语法

现在我们已经完成了语法解析器，让我们来看看如何修改词法分析器，以便两者都知道正确的标记集以及如何将词法分析器连接到解析器。让我们从查看升级后的输入文件开始，我们将描述为了支持连接的更改。

## 列表 23.4 升级后的输入文件（位于 `source/ch23/tokens.l`）

```lex
1: %%
2:   #include <stdio.h>
3:   #include "grammar.tab.h"
4: %}
5:
6:   NUM[0-9]+
7:   VAR[a-zA-Z]+
8:   WS[ \t]+
9:
10: %
11:   set return SET;
12:   {NUM}+ return NUMBER;
13:   {VAR}+ return VARIABLE;
14:                 return OP_MINUS;
15:   \+ return OP_PLUS;
16:   = return ASSIGN;
17:   ; return END;
18:   \n /* 忽略空格 */
19:   {WS}+ /* 忽略空格 */
20: %%
```

## 使用 flex 和 bison 生成解析器

需要注意的第一点是，为了知道解析器生成器使用哪些标记（常量名），我们必须在词法分析器中包含它们。当使用 bison 构建解析器生成器时，它还会生成一个包含指定标记（通过 `%` 符号指定）的头文件。现在可以将其包含在 flex 输入文件中并将它们连接起来。在词法分析器的编译阶段，我们可以轻松地发现是否存在断开（由于缺少符号错误）。

现在让我们通过从 flex 和 bison 输入文件构建解析器的过程。在示例示例中，我们的语法输入文件名为 `grammar.y`，flex 输入文件名为 `tokens.l`。我们首先开始构建解析器本身，因为词法分析器依赖于此处生成的头文件：

```bash
## ls
grammar.y tokens.l
## bison -d grammar.y
## ls
grammar.tab.c grammar.tab.h grammar.y tokens.c
#
```

我们告诉 `bison`（通过 `-d` 标志）生成额外的输出文件（包含我们的宏定义），以便我们可以将其挂钩到词法分析器。我们在这里看到了两个文件：`grammar.tab.c` 和 `grammar.tab.h`。

接下来，使用 `flex` 构建我们的词法分析器：

```bash
## flex tokens.l
## ls
grammar.tab.c grammar.tab.h grammar.y lex.yy.c tokens.c
```

我们使用输入文件调用 `flex`，生成了一个名为 `lex.yy.c` 的新文件。这就是我们的词法分析器。最后，我们可以使用 `gcc` 将它们一起编译生成解析器：

```bash
# gcc grammar.tab.c lex.yy.c -o parser -lfl
```

现在我们得到了一个名为 `parser` 的可执行文件。让我们试试它是如何工作的（参见列表 23.5）。

### 列表 23.5 解析器的示例用法

```
# ./parser
set counter = 1;
properly formed
set counter = counter + 1;
properly formed
set counter = lastCount;
properly formed
set deltaCount = counter - lastCount;
properly formed
set set = set;
error: parse error
#
```

从这种用法可以看出它正确识别了我们的语法。当我们遇到错误时，它会以某种状态退出。我们也可以通过 Ctrl+D 退出解析器。

注意我们上一个检测到错误的例子提供了一个有趣的案例。对于词法分析器中变量规则（见列表 23.4 第 13 行）来说，`set` 标记是有效的，但根据正则表达式的优先级，它被识别为 `SET` 标记而不是变量。根据我们的语法，这被定义为错误。

现在我们已经构建了一个可以识别输入是否正确、可以识别的标记以及语法的解析器。下一步是对数据进行实际操作，我们将在下一节中讨论。

### 构建简单的配置解析器

# 列表 23.6 示例电子邮件防火墙配置文件（位于 CD-ROM 上的 `./source/ch23/config/config.file`）

```
1:  allow {
2:
3:    mtj@mtjones.com
4:    dan_5422@yahoo.com
5:    albert@camus.com
6:
7:  }
8:
9:  disallow {
10:
11:   spammer@spamcorp.com
12:   viagra@pharma.com
13:
14: }
```

该文件的结构非常简单。`allow` 部分中的电子邮件地址是被允许的，而 `disallow` 部分中的地址则会被拒绝。

我们的解析器将按照我们在第一个示例中演示的两个阶段进行构建。我们的配置文件词法分析器将定义在一个名为 `config.l` 的文件中，语法解析器将定义在 `config.y` 中。在本示例中，我们不再从 `stdin` 接收配置文件，而是允许从文件中读取配置。

# 配置文件词法分析器

词法分析器是我们配置文件解析器的第一阶段。它将文件拆分为基本元素并将它们返回给语法解析器。根据列表 23.6，我们允许的标记（tokens）非常少，主要由两个保留字（`allow` 和 `disallow`）、节分隔符（`{ }`）以及最后的电子邮件地址组成（它是标记的聚合）。空白字符和换行将被简单地忽略。我们用于配置文件词法分析器的 `flex` 输入文件如列表 23.7 所示。

# 列表 23.7 配置文件解析器 flex 输入文件（位于 CD-ROM 上的 `./source/ch23/config.fl`）

```
1:  %
2:  #include <stdio.h>
3:
4:  #include "config.tab.h"
5:  %
6:
```

# 408 GNU/Linux 应用编程

```
7: % return ALLOW;
8: allow return DISALLOW;
9: disable return yylval=strdup(yytext); return WORD;
10: [a-zA-Z]+[a-zA-Z0-9_]* return OPEN_BRACE;
11: /{ return CLOSE_BRACE;
12: } return ATSYM;
13: @ return PERIODSYM;
14: . /* 忽略行尾 */
15: n /* 忽略空白 */
16: [ \t]+
17: %
```

第一个需要注意的是点是，我们指定了需要解析器头文件来理解哪些标记将进行通信（第 4 行）。接下来，在第 10 行，我们看到了一个字符串模式的新操作。该特定模式识别以字母（大写或小写）开头，随后跟上可选的字母、数字或 `_` 字符的字符串。当我们识别出其中一个标记时，它的值（已分词的值）会被复制到名为 `yylval` 的特殊变量中。词法分析器将其存储在 `yytext` 中，这允许解析器看到实际的标记（除了返回的标记类型，在本例中为 `word`）。

现在我们有了一个词法分析器，它可以对我们的文件进行分词，并返回它找到的特殊单词（忽略保留字，取决于表中的优先级）。现在让我们探索新的解析器（列表 23.8）。

# 列表 23.8 配置文件解析器 bison 输入文件（位于 CD-ROM 上的 `./source/ch23/config/config.y`）

```
1: %{
2: #include <stdio.h>
3: #include <string.h>
4: 
5: void yerror(const char *str)
6: {
7: fprintf(stderr, "error: %s\n", str);
8: }
9: 
10: 
11: int main()
12: {
13: FILE *infp;
14: 
15: infp = fopen("config.file", "r");
16: 
17: yyrestart( infp);
```

18:

19:    yyparse();

20:

21:    fclose(infp);

22:

23:    return 0;

24:    }

25:

26:

27:    char address[10][80];

28:    int addrCount = 0;

29:

30:    %}

31:

32:    %token ALLOW OPEN_BRACE CLOSE_BRACE BRACE DISALLOW WORD ATSYM PERIODSDYM

33:

34:    %%

35:

36:    configs:

37:        | configs config

38:        ;

39:

40:    config:

41:        allowed

42:        |

43:        disallowed

44:        ;

45:

46:    allowed: ALLOW OPEN_BRACE targets CLOSE_BRACE

47:

48:        {

49:            int i;

50:            printf("Allow these addresses:\n");

51:            for (i = 0; i < addrCount; i++) {

52:                printf("\t%s\n", address[i]);

53:            }

54:            addrCount = 0;

55:        }

56:;

57:    disallowed: DISALLOW OPEN_BRACE targets CLOSE_BRACE

58:        {

59:            int i;

60:            printf("Disallowed addresses:\n");

61:            for (i = 0; i < addrCount; i++) {

62:                printf("\t%s\n", address[i]);

63:            }

64:            addrCount = 0;

65:        }

66:;

```

（注：根据上下文，OCR 文本中 `disallowed` 规则和 `allowed` 操作的后半部分是损坏的。）

# 437 410 GNU/Linux 应用编程

规则的操作部分定义了我们在识别电子邮件地址时执行的操作。在本例中（只要我们没有耗尽存储资源），我们将地址填充到地址条目中。

`email_address` 规则（第 75–84 行）指定了它是一个单词后跟 `@` 符号，然后是两个由 `.` 分隔的单词。因此，如下的电子邮件地址：

```
mtj@mtjones.com
```

会被识别，但：

```
mtj@email.mtjones.com
```

不会。对于演示，简单的地址就足够了。

# 438 使用 flex 和 bison 生成解析器

在 `targets` 规则中，我们指定可以识别零或多个电子邮件地址。注意这里的标记列表：

可以通过特殊集合访问。`$1` 代表列表中的第一个单词。回想我们在（列表 23.7 第 10 行）中，我们使用 `strdup` 将当前标记复制到 `yylval`。`$1` 代表词法分析器存储的 `yylval`。`$3` 代表第三个单词，`$5` 代表最后一个单词。因此，我们使用 `sprintf`（将字符串连接到我们的地址数组中），从各个单词部分得到一个连续的地址。一旦存储了识别出的地址，我们就释放每个字符串引用。回想我们使用了 `strdup` 来复制当前标记。这具有为新对象分配内存的效果，因此，我们释放该资源。

一旦识别到该节的 `CLOSE_BRACE`（第 46 行或 57 行），我们根据规则的上下文输出被（允许的或拒绝的）地址。如果我们处于 `allowed` 规则中，我们就知道这些地址位于 `allow` 节内。同样，在 `disallowed` 规则中，我们将地址输出为拒绝的。在输出每个节后，我们将计数器清零，以允许额外的节被识别和存储。

让我们看看解析器的示例。列表 23.9 提供了一个示例文件（格式正确）。

# 列表 23.9 示例配置文件

```
1: allow {
2:
3: mtj@mtjones.com
4: dan_5422@yahoo.com
```

# 412 GNU/Linux 编程

```
5:
6:
  }
  disallow {
  you@yahoo.com
  them@excite.com
}
```

将此文件命名为 `config.file`（解析器的要求），我们如下所示演示其用法：

```
# /parser
Allow these addresses:
mtj@mtjones.com
dan_4522@yahoo.com
Disallow these addresses:
you@yahoo.com
them@excite.com
#
```

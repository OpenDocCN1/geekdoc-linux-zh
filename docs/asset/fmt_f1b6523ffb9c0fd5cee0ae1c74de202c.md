
```makefile
1:
2:    SRC_VAR=test string for manipulation.
3:
4:    TEST1_VAR=$(subst for,foo,${SRC_VAR})
5:    TEST2_VAR=$(patsub test%,Test%,${SRC_VAR})
6:    TEST3_VAR=$(filter manipulation,${SRC_VAR})
7:    TEST4_VAR=$(sort ${SRC_VAR})
8:    TEST5_VAR=$(words ${SRC_VAR})
9:    TEST6_VAR=$(word 2,${SRC_VAR})
10:    TEST7_VAR=$(wordlist 2, 3,${SRC_VAR})
11:
12:
13:    all:
14:        echo original str: ${SRC_VAR}
15:        echo substitution: ${TEST1_VAR}
16:        echo pattern sub: ${TEST2_VAR}
17:        echo filter: ${TEST3_VAR}
18:        echo sort: ${TEST4_VAR}
19:        echo word count: ${TEST5_VAR}
20:        echo word 2 thru 4: ${TEST7_VAR}
```

第 2 行设置了用于练习的字符串。第 4-10 行展示了 `subst`、`patsub`、`filter`、`sort`、`words`、`word` 和 `wordlist` 等函数的用法。注意函数调用的通用形式为 `${func arg1,arg2}`。第 13-20 行在执行 Makefile 时输出了结果。列表 6.7 是 6.6 Makefile 的输出：

```
1:
2:original str: test string for manipulation.
3:substitution: test string string for manipulation.
4:pattern sub: Test string for manipulation.
5:filter: manipulation
6:sort: manipulation string string test
7:word count: 4
8:word 2: string
9:word 2 thru 4: string for
```

## GNU/Linux 应用编程

```makefile
4:
5:	VPATH = src
6:
7:	CFLAGS = -c -g
8:	LDFLAGS = -g
9:
10:	appex: ${OBJ_FILES}
11:	gcc ${LDFLAGS} -o appex ${OBJ_FILES}
12:
13:	%.o:%c
14:		gcc ${CFLAGS} -o $@ $<

15:
16:	clean:
17:	rm *.o appex
18:
19:	MAIN_HDRS=lib.h app.h
20:	LIB_HDRS=lib.h
```

这个 Makefile 与列表 6.2 中引入的第一个非常不同，但它完成了与原始 Makefile 相同的基本任务。首先，你应该注意到变量的引入，这使得控制参数（编译标志、文件列表等）可以在 Makefile 的顶端进行枚举和设置。第 2 行到第 8 行设置了控制构建过程的变量。第 3 行说明了如何使用模式替换函数来生成最终应用程序所依赖的对象文件列表。模式替换的结果是将 `OBJ_FILES` 变量赋值为 `main.o bar.o`。因此，`OBJ_FILES` 变量现在包含了链接 `appex` 可执行文件所需的对象文件列表。第 10 行是显式说明这种关系的规则；它使用 `OBJ_FILES` 的值作为依赖列表。第 16 行和第 17 行演示了标准 Makefile 中经常存在的目标。该目标的名为 `clean`，它的职责是删除由 make 过程生成的文件。这为开发者提供了一个很好的机制来清理生成的文件，以便对整个项目进行完整的重建。第 16 行到第 25 行代表头文件依赖。这部分如何工作将留给你理解，因为在下一节中，将引入一种不同的机制来自动处理包含文件依赖。

列表 6.8 最有趣的部分是第 5 行、13 行和 14 行添加的内容。第 13 行引入了一个模式规则，指示 make 工具将任何以 .c 扩展结尾的任意文件转换为以 .o 扩展结尾的对应文件。该转换通过执行与模式规则相关的命令完成，在本例中，即第 14 行的命令。注意第 14 行的命令使用了一些特殊的变量引用来指示 GCC 应该操作的文件。GNU make 提供了许多此类特殊变量，允许模式规则中的命令获取有关匹配文件的信息。在第 14 行的具体案例中，`$@` 变量包含规则左侧匹配的文件名，而 `$<` 变量包含变量右侧匹配的文件名。GNU make 为模式规则提供了了大量变量，这些变量在 GNU 手册中均有记录。这一个模式规则替换了列表 6.2 中用于构建对象文件的四个特定规则。

上一个段落简单提到关于使用模式匹配规则的一个重要细节。模式匹配规则在执行比较时不考虑文件名和路径。它们假设模式规则的左侧和右侧都出现在同一个目录中。在本章提供的示例中，情况并非如此，源文件距离 Makefile 所在的位置有一级。源文件全部位于 `src` 目录中。为了解决这个问题，使用了 GNU make 的 `VPATH` 变量为模式匹配规则提供一个搜索目录列表，当规则的右侧不在当前目录时使用该列表。在第 5 行中，`VPATH` 变量被设置为 `src`，以便第 13 行的模式规则在尝试生成对象文件时找到源文件。

那么，你从列表 6.2 和列表 6.8 中获得了什么呢？列表 6.8 中的 Makefile 扩展性更好。它尝试区分构建应用程序的操作与执行这些操作的文件。在构建过程的所有可变方面中，这些方面在 Makefile 顶部的变量中控制，而动作包含在文件中下方的规则中。因此，要从构建中添加或删除文件，你只需要修改文件顶部的变量。列表 6.8 在文件跟踪方面仍然存在问题，但下一节将阐明如何解决这种情况。

## 自动依赖跟踪

你在 Makefile 中包含头文件依赖时会遇到问题。例如，随着项目的增长，保持 Makefile 与源文件中的 `#include` 指令同步会变得棘手。由于工具链中的预处理器已经必须解析 `#include`，大多数现代编译器都提供了一种自动输出这些规则的机制。生成的规则随后可以在 Makefile 中使用，以跟踪 `#include` 结构的变化并适当地地重建项目。列表 6.9 演示了对列表 6.8 Makefile 的修改，以使用 GNU make 手册中建议的自动依赖跟踪机制。

列表 6.9 带依赖跟踪的 Makefile（位于 CD-ROM 的 `./source/Makefile.deptrack` 中）

```makefile
1:
2: SRC_FILES=main.c app.c bar.c lib.c
3: OBJ_FILES=$(patsubst %c, %.o, ${SRC_FILES})
4: DEP_FILES=$(patsubst %c, %.dep, ${SRC_FILES})
5:
6: VPATH = src
7:
8: CFLAGS = -c -g
9: LDFLAGS = -g
10:
11: appex: ${OBJ_FILES}
12: gcc $(LDFLAGS) -o appexp ${OBJ_FILES}
13:
14: %.o:%c
15: gcc $(CFLAGS) -o $@ $<
16:
17: clean:
18: rm *.o appexp
19:
20: include $(DEP_FILES)
21:
22: %.dep:%c
23: \
24: gcc -M $(CFLAGS) $< > $@
25: sed 's/\*\(.*\)$/\1/' $@
26: 
```

列表 6.9 与列表 6.8 非常相似，除了第 4 行以及第 20 行到 26 行。第 4 行通过将扩展名替换为 `.dep` 来创建一个变量。`.dep` 文件包含了每个源文件的生成依赖规则。第 20 行是新 Makefile 中最重要的的一行，因为它建立了主 Makefile 和所有生成的 `.dep` 文件之间的依赖。当 make 评估列表 6.9 时，它意识到必须确保第 20 行包含的所有 `.dep` 文件都是最新的。`.dep` 文件是如何生成的？当 make 尝试包含 `.dep` 文件时，它还会评估当前 Makefile 中的规则，查看是否知道如何创建 `.dep` 文件。第 22 行到 26 行是一个模式规则，告诉 make 如何根据 .c 文件创建 .dep 文件。第 24 行调用 C 编译器生成基本的 `#include` 依赖规则。结果输出到一个临时文件中。第 25 行使用 `sed` 对输出进行处理，使得 `.dep` 文件本身也依赖这些项；当任何依赖项发生变化时，.dep 文件也会被重建。

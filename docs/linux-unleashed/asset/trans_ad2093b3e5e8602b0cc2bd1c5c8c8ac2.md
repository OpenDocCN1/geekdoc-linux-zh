
## DDL 提供支持 dl 数据库实用工具
-   **-DDL** 提供支持 `dl` 数据库实用工具的功能（需要在名为 `DLPATH` 的目录变量中包含 `dl` 系统，并且取消注释 `DLOBJS` 行以显示文件 `getdesc.o` 和 `enddesc.o` 的位置）。
-   **-DCAPFILES** 提供与 `cap` 目录的向后兼容性。
-   **-DLOADRESTRICT** 基于并发用户数量限制用户访问权限（参见下一节）。
-   **-DSETPROCTITLE** 设置由 `ps` 命令显示的名称（仅限基于 BSD UNIX 的系统）。

`conf.h` 文件在编译过程中用于设置关于 Gopher 服务的其他参数。对于设置 Gopher 服务而言，重要的设置至少包括那些与查询数量和超时变量相关的设置。这些设置通常位于 `conf.h` 文件的末尾。

`WAISMAXHITS` 变量定义了查询 WAIS 数据库时可以提供结果的最大命中数，通常设置为 40 左右。该变量的定义如下：

```c
#define WAISMAXHITS 40
```

请注意，由于这是用 C 语言编写的，井号不是注释符号。井号是预处理器指令的重要组成部分，应保留原样。定义中也没有等号。

如果 `Makefile.config` 中的 `SERVEROPTS` 变量使用了 `-DLOADRESTRICT` 关键字，则使用 `MAXLOAD` 变量。`MAXLOAD` 定义了 Gopher 服务响应请求的最大平均负载（此值可以通过命令行覆盖）。通常的定义如下：

```c
#define MAXLOAD 10.0
```

`READTIMEOUT` 和 `WRITETIMEOUT` 变量设置了服务在超之前等待网络读或写操作的时间。默认设置通常就足够了。这些行看起来如下：

```c
#define READTIMEOUT (1*60)
#define WRITETIMEOUT (3*60)
```

Gopher 客户端的配置很简单。首先通过 `CLIENT1_HOST` 和 `CLIENT2_HOST` 条目定义本地机器连接的 Gopher 服务器。当 Gopher 客户端启动时，它会选择这两个中的一个（如果两者都已定义）。这些条目看起来如下：

```c
#define CLIENT1_HOST "gopher_serv.tpci.com"
#define CLIENT2_HOST "other_gopher_serv.tpci.com"
```

用于连接主机的端口由这些选项定义：

```c
#define CLIENT1_PORT 70
#define CLIENT2_PORT 70
```

如果您有一个本地服务且不想使用端口 70（例如为了防止来自互联网的访问），请设置相应的端口值。如果只使用一个 Gopher 服务器，请将第二个值设置为 0。

通过从多个选项中选择一个值来定义 Gopher 客户端将使用的语言。默认值是美式英语，由以下命令设置：

```c
#define DEFAULT_LANG "En_US"
```

其他语言定义在此行下方被注释掉。如果您想更改默认语言，请注释掉美式英语设置并取消注释您想要的内容。

当完成所有配置更改后，您可以使用以下命令启动客户端和服务的编译过程：

```sh
make client
make server
```

或者，您可以使用不带参数的 `make` 命令同时处理客户端和服务系统。还必须使用以下命令安装程序和数据文件：

```sh
make install
```

## WAIS 和 Gopher

Gopher 客户端具有使用 WAIS 索引搜索文档的能力，但系统必须配置为允许此功能。我们在第 49 章“配置 WAIS 站点”中讨论了 WAIS，因此为了向 Gopher 提供 WAIS 索引访问，我们假设您已正确安装 WAIS 并且已准备好供 Gopher 使用的 WAIS 索引。

要通过 Gopher 提供 WAIS 服务，您可能需要对 WAIS 源代码进行更改。检查 WAIS 源代码，寻找如下所示的行：

```c
if (gLastAnd) printf("search_word: boolean 'and' scored\n");
```

为了提供 Gopher 服务，应注释掉此行，因此如果未注释，请在该行前后添加 C 注释符号，如下所示：

```c
/* if (gLastAnd) printf("search_word: boolean 'and' scored\n"); */
```

如果该行已经注释掉（或不存在），则您不需要进行任何更改。但是，如果您更改了该行，必须通过进入 WAIS 顶层目录并运行 makefile（输入命令 `make`）重新编译 WAIS。

接下来，检查 Gopher 的 `Makefile.config` 文件并查找 `WAISTYPE` 变量。它应该在如下所示的行中定义：

```sh
WAISTYPE = #-DFREEWAIS_0_4
```

然后，您必须链接 Gopher 和 WAIS 服务。假设您的 Gopher 源目录是 `/usr/gopher/source`，WAIS 源目录是 `/usr/wais/source`。您可以通过输入以下命令来链接这些服务：

```sh
cd /usr/gopher/source
ln -s /usr/wais/source/include ./ir
ln -s /usr/wais/source/client/ui .
ln -s /usr/wais/source/bin .
```

当 Gopher 重新编译时，它建立 Gopher 和 freeWAIS 之间的链接，并允许这两个服务互操作性。

## 设置您的 Gopher 目录

Gopher 目录和文件非常简单设置，大部分遵循标准的命名约定。但是，在开始之前，您应该知道哪些文档和文件将通过 Gopher 提供给其他用户，并且您应该能够编写每个文件的简短描述。（如果您不知道文件的内容，请阅读它或让作者为您总结文件。）为了简单起见，让我们假设您只使用单个目录来存放所有的 Gopher 文档。

首先，切换到您用于 Gopher 目录的顶层目录（如果尚未创建，您可能需要创建它）。为方便起见，此目录不应是放置 Gopher 源代码和配置文件的地方。只需选择一个有用的名称并创建目录。例如，要创建 Gopher 主目录 `/usr/gopher/data`，请发出标准的 `mkdir` 命令：

```sh
mkdir /usr/gopher/data
```

切换到您的 Gopher 目录，并将您想要使其可用的文件复制到其中。完成此操作后，您可以为每个文件创建描述性文件名（而不是通常使用的晦涩文件名），长度最多为 80 个字符。例如，如果您有一个名为 `q1.sales` 的文件，您可能希望将其重命名为 `Company_Sales_1887_01`，以便用户更容易识别内容。

提供更好文件名的过程是首先在你的 Gopher 主目录（例如 `/usr/gopher/data/.cap`）下创建一个 `.cap` 目录。对于主目录中的每个文件，您希望在 `.cap` 目录中创建一个具有相同名称但带有名称和编号的文件。例如，假设您在 `/usr/gopher/data` 中有一个名为 `q1.sales` 的文件。在 `/usr/gopher/data/.cap` 中，您将创建一个具有相同名称 `q1.sales` 的文件，其内容如下：

```text
Name=Company Sales for the First Quarter, 1887
Numb=1
```

`Name` 条目可以包含空格或其他特殊符号，因为它作为一个完整字符串被回显。`Numb` 条目用于该条目在您 Gopher 菜单上的位置。例如，假设您有前面的条目和另外两个文件，使用 `cat` 显示其内容如下：

```sh
$ cat q1.sales
Name=Company Sales for the First Quarter, 1887
Numb=1

$ cat q2.sales
Name=Company Sales for the Second Quarter, 1887
Numb=2

$ cat q3.sales
Name=Company Sales for the Third Quarter, 1887
Numb=3
```

当这些条目在 Gopher 菜单中显示时，它们看起来像这样：

1. 1887 年第一季度公司销售
2. 1887 年第二季度公司销售
3. 1887 年第三季度公司销售

`.cap` 目录中文件名的顺序不重要，但您不应该让相同的 `Numb` 条目出现多次。

使用 `.cap` 目录方法（允许轻松添加新文件）的一种替代方法是为每个使其可用的文档使用单个主文件。该文件位于您的 Gopher 顶层目录中，称为 `.names`。以下是刚才提到的同样三个文件的 `.names` 文件：

```sh
$ cd /usr/gopher/data
$ cat .names
# My Gopher main .names file

Path=./q1.sales
Name=Company Sales for the First Quarter, 1887
```


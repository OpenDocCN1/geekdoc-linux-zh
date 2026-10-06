
## 进程

进程是 Linux 对命令的执行。你登录时启动的 shell 是一个命令，也是一个进程，与其他任何命令一样。每当你在命令行输入 Linux 工具的名称时，就会启动一个进程。

当你运行 shell 脚本时，会启动另一个进程，并且脚本中的每个命令都会启动额外的进程。取决于你调用 shell 脚本的方式，脚本由新 shell 运行，或由当前 shell 的子 shell 运行。从命令行或通过脚本运行 `cd` 等 shell 内置命令时，不会启动进程。

### 进程结构

像文件结构一样，进程结构也是层次化的。它有父进程、子进程，甚至有根。一个进程派生（fork）一个子进程，子进程又可以派生其他进程。（你也可以使用 `spawn` 一术；这两个词是可以互用的。）`Fork` 是创建一个新进程的操作系统例程（或系统调用）的名称。当进程启动时，Linux 首先执行的进程之一是单一进程——进程标识（PID）数字 `1`，名为 `init`。该进程在进程结构中所处的位置与文件结构中的根目录相同。它是每个用户运行的所有进程的祖先。如果系统连接了终端，它会为每个终端派生一个 `getty` 进程，等待用户登录。登录操作会将 `getty` 进程转换为登录进程，进入用户的 shell。

### 进程标识

Linux 在每个进程创建时分配一个唯一的进程标识（PID）数字。只要进程存在，它就保持相同的 PID 数字。在一个会话期间，进程始终执行登录脚本。当你派生一个新进程时——例如，当你使用编辑器时——新的（子）进程的 PID 与其父进程不同。当你返回登录会话时，你会发现它仍在执行同一个进程，且 PID 数字与最初相同。

下面的交互显示了在派生新进程时，运行 `ps` 的进程是 shell 进程的父进程。当你带 `-l` 参数调用 `ps` 时，它会显示每个进程的详细信息。

## 执行命令

除了内置于 shell 的内置命令外，每当你在命令行给 shell 一个命令时，shell 都会派生（fork），即创建一个 shell 的副本（即一个子 shell）。新进程尝试执行（exec）该命令。像 `fork` 一样，`exec` 是一个由操作系统执行的例程（一个系统调用）。如果该命令是一个可执行程序（例如编译好的 C 程序），`exec` 将成功。当 `exec` 失败时，则假设该命令是一个 shell 脚本，子 shell 将运行脚本中的命令。与期望从命令行输入的登录 shell 不同，shell 从文件（即 shell 脚本）获取输入。

如之前所述，如果你有一个没有执行权限的 shell 脚本，你可以使用 `bash` 命令执行 shell 来直接运行该脚本。在下面的示例中，`bash` 创建了一个从名为 `whoson` 的文件获取输入的新 shell：

```bash
bash whoson
```

由于 `bash` 命令期望读取包含命令的文件，因此你不需要 `whoson` 的执行权限。（但是你需要读取权限。）尽管 `bash` 读取并执行文件 `whoson` 中的命令，但标准输入、标准输出和标准错误都连接到终端。

使用 `bash` 作为命令来执行 shell 意味着你不需要脚本文件具有执行权限。然而，这种技术会导致脚本的运行速度比直接通过赋予执行权限来调用慢。用户通常倾向于将文件设置为可执行，并在命令行中输入其名称来运行脚本。这样输入名称也更方便，并且与其他类型的程序的调用方式一致（因此，如果 `bash` 不是你的交互式 shell，或者如果你想查看脚本在不同 shell 中是如何运行的，你应该给出 `bash`（或另一个 shell 的名称）命令，后跟包含脚本的文件名，如前所示。

### 注意

原始的 Bourne 壳（Bourne Shell）是通过命令 `sh` 调用的。虽然你可以用 `sh` 命令使用 `bash`，但它并不是原始的 Bourne Shell。它是指向 `/bin/bash` 的符号链接，因此它只是 `bash` 的另一个名称。当你使用命令 `sh` 调用 `bash` 时，`bash` 会尝试尽可能地模拟原始 Bourne Shell 的行为。但它并不总是能成功。

## 指定 Shell

你可以在 shell 脚本的第一行添加一段特殊的字符序列，以指示操作系统这是一个脚本。因为操作系统在尝试 `exec` 执行程序之前会检查程序的初始字符，这些字符可以避免系统进行无效的尝试。它们还告诉系统应该使用哪种 shell（通常是 `bash`、`tsh` 或 `zsh`）。如果脚本的前两个字符是 `#!`，系统会将它们解释为应该执行它的程序的绝对路径。这可以是任何程序的路径，而不只是 shell。以下示例指定了当前脚本应该由 `bash` 运行：

```bash
bash cat bash_script
#!/bin/bash
echo "This is a Bourne Again Shell script."
```

如果你有一个打算在活动 `bash` 之外的其他 shell 中运行的脚本，此功能将非常有用。它可以从任何 shell 运行，但必须由 `tcsh` 执行。以下示例显示了一个由于 `#!` 行的存在而意图由 `tcsh` 执行的脚本，操作系统看到无论从哪个 shell 运行，都由 `tcsh` 在执行它。

```bash
bash cat tcsh_script
#!//tcsh
echo "This is a tcsh script."
set person = jenny
echo "$person"
```

如果你没有使用 `#!` 配合可执行程序的名称，`bash` 会报告错误。你可以选择地在 `#!` 后面加上空格。如果你省略了 `#!` 行并尝试（例如）从 `bash` 运行 `tcsh` 脚本，shell 会生成语法错误信息。

## 注释

注释让 shell 脚本（以及所有代码）更容易阅读和维护。如果你在 shell 脚本中放置注释，你或他人将更容易维护它们。`bash` 使用的注释语法是所有 shell 通用的。

如果脚本第一个字符的井号（`#`）后面没有紧跟感叹号（`!`），或者井号出现在脚本中第一个字符以外的任何位置，shell 将其解释为注释的开始，并忽略井号到下一个换行符之间的所有内容。

## 启动文件

当启动一个新的 shell 时，可能会使用某些包含命令的文件来初始化 shell。访问的文件取决于该 shell 是登录 shell（login shell）、不是登录 shell 的交互式 shell，还是非交互式 shell（用于执行 shell 脚本的 shell）。下面的节讨论了在启动新 shell 时执行的文件。

如果 `bash` 作为登录 shell 启动，或者在启动 `bash` shell 时使用了 `-login` 选项，`bash` 会首先读取 `/etc/profile` 中的命令。之后，`bash` 登录会在你的主目录下查找要执行的命令文件。如果 `bash` 找到了 `.bash_profile`，则执行它。否则，如果存在 `.bash_login`，`bash` 会执行该文件。如果这两个文件都不存在，`bash` 会执行 `.profile` 文件（如果存在的话）。在注销时，该 shell 会读取并执行主目录下的 `.bash_logout` 文件（如果存在的话）。

如果 `bash` 作为非登录交互式 shell 启动（例如通过输入 `bash` 命令获得的 shell），`bash` 只读取 `.bashrc` 文件。然而，这会继承来自父 shell 的任何环境（导出）变量，因此在 `/etc/profile` 和 `.bash_profile` 中设置的环境变量会传递给非登录 shell。

最后，对于非交互式 shell（标准输入和输出未连接到你终端的 shell）环境变量 `BASH_ENV` 和 `ENV`，`BASH_ENV` 是不存在的。如果这个环境变量的值是一个文件名，shell 将读取并执行该文件中的命令。

虽然不同 shell 类型和初始化文件的数量看起来可能令人困惑，但 `bash` 用户在主目录下只有 `.bash_profile` 和 `.bashrc`。他们希望所有 `bash` 实例执行的大多数 shell 命令都放在 `.bashrc` 中，`.bash_profile` 包含了加载并运行 `.bashrc` 命令的命令，以及将字符串 `~/` 赋值给 `ENV` 变量。这样，无论 shell 如何启动，`.bashrc` 都会被执行。你可以将以下命令放入 `.bash_profile` 中来实现此效果：

```bash
export ENV~/.bashrc
if [ -f ~/.bashrc ]; then source ~/.bashrc; fi
```

### bash 启动文件的执行顺序

| bash 启动文件的执行顺序 | 交互式登录 shell | 非交互式（非登录）shell |
| :--- | :--- | :--- |
| `/etc/profile` | 第一 | 不执行，但 shell 继承来自父 shell 的变量——这些变量最初是由这些文件设置的 |
| `.bash_profile` | 第二 | |
| `.bash_login` | 第二（如果没有 `.bash_profile` 时） | |
| `.profile` | 第二（如果没有 `.bash_profile` 或 `.bashrc` 时） | 仅由交互式非登录 shell 执行 | 不执行 |
| `.bash_logout` | 注销时执行 | 执行名为 `BASH_ENV` 或 `ENV` 的文件列出的命令 |

## 参数与变量

在 shell 中，一个 shell 参数与一个用户可以访问的值关联。有多种 shell 参数。由字母、数字和下划线组成的名称通常被称为 shell 变量，或变量。变量名不能以数字开头。因此 `A76`、`MY_CAT` 和 `__X__` 是合法的名称，而 `69TH_STREET`（以数字开头）和 `MY-NAME`（包含连字符）不是。你可以创建可以命名并赋值的 shell 变量。一个约定是导出的变量（环境变量）使用全大写字母，其他变量使用大小写或小写字母。你可以随时更改用户创建变量的值，并将其设置为只读（`readonly`），这样它们就无法更改。

### 用户创建的变量

你可以声明任何字母、数字和下划线序列作为变量名，只要第一个字符不是数字。下方的第一行声明了名为 `person` 的变量并将其初始化为 `alex`。当你给变量赋值时，不能在等号前后加上空格或制表符。因为 `echo` 将其参数复制到标准输出，你可以用它显示变量的值。

```bash
bash$ person=alex
bash$ echo person
person
bash$ echo $person
alex
```

第二行显示 `person` 不代表 `alex`。只有在显示变量名称之前加上美元符号（`$`）时，字符串 `person` 才是变量的值。`echo person` 命令显示变量 `person` 的值。它没有显示 `person`，因为 shell 没有将 `person` 作为参数传递给 `echo`。由于开头的 `$`，shell 识别出 `$` 是变量名，替换变量的值并将该值传递给 `echo`。`echo` 内置命令显示的是变量的值而不是它的名称，它永远不知道你称它为变量。上例最后的命令显示了变量 `person` 的值。

你可以通过引用前面的 `$` 来防止 shell 替换变量的值。双引号不会阻止替换；单引号或反斜杠（`\`）可以。

```bash
bash$ echo $person
alex
bash$ echo "$person"
alex
```

```bash
bash echo '$person'
$person
bash echo \$person
$person
```

双引号不会防止变量替换，但会关闭其他字符的特殊含义，它们在给变量赋值以及使用这些值时非常有用。要给变量赋值包含**空格（SPACES）**或**制表符（TABs）**的内容，请变量使用双引号。

```bash
bash echo $person
alex
bash$person=alex and jenny
bash: and: command not found
bash$ echo $person
alex
```

在这个示例中，`bash` 假设 `person=alex` 是一个命令，而 `and` 是该命令的参数。当它找不到名为 "and" 的命令时，它会提示你。shell 中变量 `person` 的值没有被改变。在下一个示例中，包含空格的字符串周围的双引号允许 `bash` 将该内容（包括空格在内）赋值给变量。虽然 `$person` 没有包含在双引号内，也并非必须包含，但将你正在使用的变量包含在双引号内是一个好习惯，正如接下来的第二个示例：

```bash
bash person="alex jenny"
bash echo $person
alex and jenny
```

当你引用一个包含制表符或多个相邻空格的值时，你需要使用引号来保留间距。如果你不给变量加引号，`echo` 在将其复制到标准输出时，会将每个非空字符字符串合并为一个**空格（SPACE）**。

```bash
bash$person="alex and jenny"
bash$ echo $person
alex jenny
bash$ echo "$person"
alex and jenny
```

当你使用变量作为参数执行命令时，shell会将变量名替换为变量的值，并将该值传递给正在执行的程序。如果变量的值包含如 `*` 或 `?` 等特殊字符，shell 可能会如前所述扩展该变量。

在以下命令序列的第一行中，字符串 `alex` 被赋值给变量 `memo`。shell 不会扩展该字符串，因为 `bash` 在给变量赋值时不会进行路径扩展（第 106 页）。Bourne Shell 按照特定的顺序处理命令行。在这个顺序中，它会在解释命令之前进行扩展。在 `echo` 命令的顺序中，双引号引用了星号（`*`），并防止 shell 在将其值传递给 `echo` 命令之前扩展 `memo` 变量：

```bash
bash$ memo=alex*
bash$ echo "$memo"
alex*
```

当你引用一个包含特殊字符且未加的变量时，shell会将特殊字符解释为特殊含义。在下面的示例中，shell扩展了 `memo` 变量的值，因为它没有加引号：

```bash
bash$ ls
alex.report
alex.summary
bash$ echo $memo
alex.report alex.summary
```

前面的内容表明，当 `memo` 未引用时，shell 将值 `alex*` 匹配到工作目录中的两个文件：`alex.report` 和 `alex.summary`。当变量加了引号时，`echo` 显示 `alex*`。

### 删除变量

只要创建它的 shell 还存在，变量就存在。要删除变量的值（但不删除变量本身），请将其设置为空值。

```bash
bash$ person=
bash$ echo $person
```

```bash
bash$
```

你可以使用 `unset` 内置命令删除变量。要删除变量 `person`，执行以下命令：

```bash
bash$ unset person
```

### readonly 内置命令

你可以使用 `readonly` 内置命令来确保变量的值不能被更改。下一个示例将变量 `person` 声明为只读。你必须在声明为只读之前给变量赋值；在声明之后你不能更改它的值。当你尝试更改只读变量的值时，shell 会显示错误信息。

```bash
bash$ person=jenny
bash$ echo $person
jenny
bash$ readonly person
bash$ person=helen
bash: person: read-only variable
```

你可以将 `readonly` 内置命令与变量声明及可选初始化结合。

```bash
bash$ readonly person=jenny
bash$ echo $person
jenny
```

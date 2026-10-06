

# 第12章：自动化系统任务 505

```bash
FOR FILE in `/bin/ls`
do
  echo $FILE
done
```

你也可以这样写，这种方式更整洁。

```bash
for NAME in John Paul Ringo George ; do
  echo $NAME is my favorite Beat
done
```

LIST 中的每个元素都通过空格与下一个元素分开。如果你不小心，这可能会引起麻烦，因为某些命令（例如 `ls -l`）每行输出多个字段，并用空格分隔。`done` 字符串表示该语句的结束。

如果你是一个“聋聋”的 C 语言程序员，bash 允许你使用 C 语言语法来控制循环：

```bash
LIMIT=10
# 使用双括号，尽管 LIMIT 是变量，但在 LIMIT 前也要加 $
for ((a=1; a <= LIMIT; a++)); do
  echo "$a"
done
```

# "while...do" 和 "until...do" 循环

两种可能的循环结构是 while...do 循环和 until...do 循环。它们的结构如下所示：

```
while condition          until condition
do                     do
  { body }             { body }
done                    done
```

while 语句在条件为真时执行。until 语句在条件为真时停止执行，换句话说，在条件为假时执行。

这是一个 while 循环示例，它将输出数字 0123456789：

```bash
N=0
while [ $N -lt 10 ]; do
  echo -n $N
  let N=$N+1
done
```

输出数字 0123456789 的另一种方法是使用如下所示 until 循环：

```bash
N=0
until [ $N -eq 10 ]; do
  echo -n $N
  let N=$N+1
done
```

# 一些实用的外部程序

Bash 非常强大，有很多内置命令，但它通常需要一些帮助来完成实用的工作。你最常看到的实用程序是 grep、cut、tr、awk 和 sed。有了这些 UNIX 工具，这些程序中的大多数都设计为与标准输入和标准输出配合，因此你可以轻松地结合管道和 shell 脚本使用它们。

# 通用正则表达式解析器 (grep)

“正则表达式解析器”这个名字听起来很吓，但 grep 只是在文件或文本中查找模式的方法。把它想象成实用的搜索工具。精通正则表达式是一项挑战，但仅用最简单的形式就能完成许多实用的工作。

例如，你可以通过 grep 显示所有普通用户账户列表，搜索 `/etc/passwd` 文件中包含 /home 的所有行：

```bash
grep /home /etc/passwd
```

或者，你可以使用以下命令找到所有以 HO 开头的环境变量：

```bash
env | grep ^HO
```

要查找与 grep 命令一起使用的选项列表，请输入 `man grep`。

# 删除文本行的某些部分 (cut)

cut 命令可以从文本行或文件中提取特定字段。它对于将系统配置文件解析为易于消化的数据块非常有用。你可以指定想要使用的字段分隔符，也可以按字节 拆分行。
接下来的示例列出了系统中所有用户的家目录。使用之前 grep 命令的示例，该行从 `/etc/passwd` 文件管道传输了一个普通用户列表，然后以冒号（`-d':'`）为分隔符显示第 6 个字段（`-f6`）。末尾的连字符告诉 cut 从标准输入（管道）读取。

```bash
grep /home /etc/passwd | cut -f6 -d':' -
```

# 翻译或删除字符 (tr)

tr 命令是一个基于字符的翻译，可以将一个字符或一组字符替换为另一个，或者从文本行中删除字符。
接下来的示例将所有大写字母转换为小写字母，并显示单词“mixed upper and lower case”：

```bash
FOO="Mixed UpEr Nd LoWeR cAsE"
echo $FOO | tr [A-Z] [a-z]
```

# 第12章：自动化系统任务 507

在下一个示例中，tr 命令被用于文件名列表，重命名列表中的任何文件，使文件名中包含的制表符或空格（如 `[:blank:]` 选项所示）翻译为下划线。尝试在测试目录运行以下代码：

```bash
for file in *; do
  f=$(echo $file | tr '[:blank:] '_')
  mv "$file" "\$f"
done
```

# 流编辑器 (sed)

sed 命令是一个简单的可脚本化编辑器，它只能执行简单的编辑，例如删除匹配模式的文本行、将一种字符模式替换为另一种，以及其他简单编辑。为了更好地了解 sed 的工作原理，在线文档是不可替代的，但这里有一些常见的示例

你可以使用 sed 命令执行你之前用 grep 示例完全相同的操作：在 `/etc/passwd` 文件中搜索单词 home。sed 命令搜索整个 `/etc/passwd` 文件中的单词 home，并打印任何包含单词 home 的行。

```bash
sed -n '/home/' /etc/passwd
```

在例例中，sed 搜索 myfile.txt 并将字符串 Mac 的所有实例替换为 Linux。替换命令末尾需要字母 g，以导致每行中出现的每个 Mac 都更改为 Linux。（否则，只会更改第一个实例）。


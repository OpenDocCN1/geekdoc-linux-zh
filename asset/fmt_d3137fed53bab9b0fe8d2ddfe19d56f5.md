
## 开发 JAVA 应用程序

你可以在 Mac OS X 系统上使用 Java 开发应用程序。要使用解释器运行 java 应用程序，你必须将其编译为字节码。`javac` 编译器读取你的源代码并生成类文件。

使用 `java` 命令运行此程序。Java 应用程序通常以 Java 档 (`JAR`) 文件的形式分发，你可以使用 `jar` 命令列出它们。

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

## 创建一个 JAVA 程序

1. 启动 Pico 编辑器创建一个名为 `HelloWorld.java` 的文件并按回车。

出现 Pico 屏幕。

2. 输入 `*` 并按回车，输入 `*` 这是用 Java 编写的 Hello 并按回车，然后输入 `*/` 并按回车。

3. 输入 `public class HelloWorld` 并按回车。

4. 输入 `public void main(String[] args)` 并按回车。

5. 输入 `System.out.println("Hello, World!")` 并按回车。

`javadoc` 注释完成。

## 开发 UNIX 应用程序

你可以使用 `jar` 命令从你的 `HelloWorld` 应用程序创建一个 Java 归档。在语法上，`jar` 命令类似于 `tar` 命令。要创建一个 JAR 文件，你可以使用 `jar xvf` 命令。要从 JAR 文件中提取内容，也可以使用 `jar xvf` 命令。要列出 JAR 文件的内容，可以使用 `jar tvf` 命令。

你可以使用 `javadoc` 命令通过 `HelloWorld` 应用程序中的 `javadoc` 注释创建一个 Web 页面。Javadoc 为 Java 程序提供了易于访问的文档，通常被认为是良好的 Java 编程至关重要的。当多个程序员协作同一个项目时，这些注释尤为关键。

要查看提取出的 `javadoc` 注释，请使用 `open HelloWorld.html`。这将在浏览器中打开 Java Web 页面。

## 实际应用

| 输入以下： | 结果 |
|---|---|
| `[jar-] user@ jar cvf HelloWorld.class` | `0 Thu May 29 21:18:32 EDT 2003 META-INF/MANIFEST.MF` |
| `[file-] user@ jar tvf HelloWorld.jar` | `477 Thu May 29 21:18:32 EDT 2003 HelloWorld.class` |

| 输入以下： | 结果 |
|---|---|
| `[file-] user@ javadoc -h HelloWorld.java` | `-rw-r--r-- 1 user staff 427 Thu May 29 20:57 EDT 2003 HelloWorld.class` |
| `[file-] user@ ls -l HelloWorld*` | `-rw-r--r-- 1 user staff 697 Thu May 29 20:58 EDT 2003 HelloWorld.html` |
|  | `-rw-r--r-- 1 user staff 181 Thu May 29 20:57 EDT 2003 HelloWorld.java` |

```
$ --project_X user@ javadoc HelloWorld.java
$ --project_X user@ javadoc HelloWorld
$ --project_X user@ 
```

```
$ --project_X user@ ls -l HelloWorld*
-rw-r--r-- 1 user staff 427 Thu May 29 20:57 EDT 2003 HelloWorld.class
-rw-r--r-- 1 user staff 697 Thu May 29 20:58 EDT 2003 HelloWorld.html
-rw-r--r-- 1 user staff 181 Thu May 29 20:57 EDT 2003 HelloWorld.java
$ --project_X user@ 
```

- 7. 保存你的文件并退出 Pico。
- 9 输入 `java HelloWorld.java` 并按回车。
- 10 输入 `ls -l HelloWorld*` 并按回车。
- 11. 系统列出了你的源文件和 Java 程序。
- 8 输入 `javac HelloWorld.java` 并按回车。
- 你的程序运行了。
- 你的程序编译了。

## 开发 Python 应用程序

你可以在 Mac OS X 系统上开发 Python 应用程序。Python 随着 Mac OS X 开发工具安装，路径为 `/usr/bin/python`。打印此路径的命令；如果没有，你必须检查你的 `PATH` 变量并安装它。

Python 是一种解释型的、交互式的、面向对象的编程语言。与你编译的 C 程序以及在虚拟机上运行的 Java 程序不同，Python 程序更像 Perl 脚本。然而，Python 的面向对象特性赋予了程序截然不同的特征。

即使你现在不熟悉面向对象编程，你也可以编写实用的 Python 脚本。然而，为了充分利用这种语言，你必须对面向对象编程有自己的理解。事实上，人们认为像 Python 这样的语言是过渡语言，因为它们让你在刚刚开始掌握面向对象编程概念时就能编写程序。

像 C 这样的语言和 Perl 这样的脚本语言是过程化语言。这意味着代码的部分被组织成称为过程或子程序的函数化元素，你在代码的其余部分使用它们。面向对象的语言的工作方式不同，它们定义了对象，然后定义了可以在对象上执行的一系列操作。你将这些称为方法。

Perl 使用命令如 `print $filename processed;` 打印到文件；而 Python 使用 `test out_file.write("Hello\n");`。虽然从上看，这些命令可能没有区别，但它们的实现和编码方法是完全不同的，你会遇到这些差异：

## 用 Python 创建 HELLO WORLD

1 启动 Python 创建名为 `HelloWorld.py` 的文件。

2 输入 `#!/usr/bin/python` 并按回车。

3 输入 `print "Hello, World!"` 并按回车。

4 保存你的脚本并退出 Pico。

5 输入 `HelloWorld.py` 并按回车。

你的脚本再次运行。

6 输入 `chmod a+x HelloWorld.py` 并按回车。

```
#/usr/bin/python
print "Hello, World!"
```

## 应用

你可以在 Ruby 中打印字符串，末尾带或不带回车符，就像在 Perl 和 Python 中一样。每种语言使用的语法都不同，如下方的比较所示。

| PERL | RUBY | PYTHON |
| --- | --- | --- |
| `print "Hello World";` | `print "Hello World"` | `print "Hello World",` |
| `print "Hello World\n";` | `puts "Hello World"` |  |

你可以通过定义一个如下所示的迭代方法来在 Ruby 中遍历值序列。

请输入以下内容：

结果为：

```ruby
def iterate(max)
  i = 0
  while i < max
    yield i
    i += 1
  end
end
```

```
0: Hello World
1: Hello World
2: Hello World
3: Hello World
4: Hello World
```

```ruby
iterate(5) { |val| puts "#{val}: Hello World" }
```

```ruby
def fact(n)
  if n == 0
    return 1
  else
    return n * fact(n-1)
  end
end
print fact(ARGV[0].to_i), "\n"
```

```bash
[ferro]:~/bin] user% /factorial 4
24
[ferro]:~/bin] user%
```

在 Ruby 中定义一个方法

1. 在文本编辑器中，输入 `def fact(n)` 并按回车。
2. 输入 `i = 0` 并按回车，然后输入 `1` 并按回车，然后输入 `else` 并输入一个空格：
3. 输入 `n * fact(n-1)` 并按回车，然后输入 `end fact` 并按回车，再次输入 `end` 并按回车。
4. 输入 `print fact(ARGV[0].to_i), "\n"`
5. 使用文件名 `factorial` 保存你的文件并退出文本编辑器。
6. 输入 `Ruby` 后加一个空格。
7. 输入 `/factorial 4` 并按回车。

你的程序将打印 4 的阶乘。

### 额外

为了让其他人使用你的新数据库软件，你必须从 `postgres` 账户启用他们。否则，用户将获得此类错误：`psql: FATAL: user "kbartlett" does not exist.`。要启用新用户，请使用 `su postgres` 命令启用账户。使用 `psql db` 命令连接到数据库。建立连接后，添加新用户：`username`，其中将 `username` 替换为你想要启用的用户名。

要将你新数据库软件中的页面添加到搜索列表中，将 `/usr/local/pgql/man` 导出到你的环境变量 `MANPATH`。此路径可能包含许多由冒号分隔的目录。下面的示例显示了如何搜索 man 页。

示例：

```bash
setenv MANPATH /sw/share/usr/local/man:/usr/share/man:/usr/local/pgql/man
```

连接到 PostgreSQL 创建表或运行查询后，你需要断开数据库连接。要这样做，输入 `\q`。此命令返回：

```bash
ig_os.h
config.status: linking ../src/makefiles/darwin to src/Makefile.file.po
[error]- user%make
make -c doc
grip -d man.tar.gz /usr/bin/tar -xf
for file in man.1*; do
  sf -F "$file" ""
  sed -e "s/\(.*\)/\1(FR)?\/" "$file.x86 $file"
  rm -f Makefile.file || exit;
done
/bin/sh ../config/installdirs-man
for file in man.1*; do
  sed -e "s/\(.*\)/\1(FR)?\/" "$file"
done
$file=$(basename $file) | sed 's/\\1\\.7//' // exit;
done
make -C src
make(2) part all
Nothing to be done for 'all'.
make -C backend all
```

```bash
[error]- sudo make install
make -c doc
grip -d postgres.tar.gz | cd /usr/local/pgql/doc/html && /usr/bin/t -xf
for file in man.1*; do
  /bin/sh ../config/install-sh -c 644 $file /usr/local/pgql/man/$file
done;
done
```

- 5 输入 `make` 并按回车。
- 软件开始编译。
- 6 输入 `sudo make install` 并按回车。
- 你的软件被编译并安装。

继续

# 在 Mac OS X 上运行数据库（续）

虽然这可能不是显而易见的，但数据库是服务器的一种——一个向客户端提供信息的进程。在用 `createddb` 创建数据库、用 `initdb` 初始化并填充表后，数据库就准备好回答查询了。大多数数据库无论是否在使用都会一直运行。

当你启动一个 `psql` 命令并连接到数据库时，你是在充当数据库的客户端。你可以通过搜索某些值并限制你从这些表中看到的内容来从表中选择数据。

PostgreSQL 像现代数据库一样，是一个关系型数据库。该术语意味着所有数据都以统一的方式存储——与元素具有父/子关系的表不同，关系型数据库没有此类关系。相反，各种类型的数据都存储在表中，所有记录都可以被访问。

```text
Terminal
[user@host] sudo username
password:
Changing password for postgres.
New password:
```

```text
Terminal
[root] sudo mkdir /usr/local/pgql
[user@host] chown postgres /usr/local/pgql/data
```

```text
Terminal
[user@host] su - postgres /usr/local/pgql/data
```

- 7 输入 `adduser` 并按回车。
- 8 输入 `su - postgres /usr/local/pgql/data`
- 9 输入 `createddb` 并按回车。
- 10 输入 `psql testdb` 并按回车。
- 11 输入 `/usr/local/pgql/bin/initdb -D /usr/local/pgql/data` 并按回车。
- 12 输入 `/usr/local/pgql/bin/postmaster -D /usr/local/pgql/data >/dev/null 2>&1` 并按回车。

# 开发应用程序

### 额外

为了让其他人使用你的新数据库软件，你必须从 `postgres` 账户启用他们。否则，用户将获得此类错误：`psql: FATAL: user "kbartlett" does not exist.`。要启用新用户，请使用 `su postgres` 命令启用账户。使用 `psql db` 命令连接到数据库。建立连接后，添加新用户：`username`，其中将 `username` 替换为你想要启用的用户名。

要将你新数据库软件中的页面添加到搜索列表中，将 `/usr/local/pgql/man` 导出到你的环境变量 `MANPATH`。此路径可能包含许多由冒号分隔的目录。下面的示例显示了如何搜索 man 页。

示例：

```bash
setenv MANPATH /sw/share/usr/local/man:/usr/share/man:/usr/local/pgql/man
```

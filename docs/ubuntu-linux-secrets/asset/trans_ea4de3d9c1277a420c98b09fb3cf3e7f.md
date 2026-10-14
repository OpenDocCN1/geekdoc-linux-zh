

名为 `AnotherClass.class` 的类文件，你想将其添加到你的 `jar` 文件中，你会使用以下格式：

```
```shell
$ jar uf myjar.jar AnotherClass.class
```
```

创建 jar 文件后，你可以使用以下格式列出文件的内容：

```
```text
$ jar tf myjar.jar
META-INF/
META-INF/MANIFEST.MF
MyTestClass.class
AnotherClass.class
$
```
```

请注意，默认情况下 `jar` 过程会添加一个名为 `MANIFEST.MF` 的文件。该文件称为清单，它用于跟踪 `jar` 文件中包含的类的功能。我们稍后会尝试使用该文件。

要提取 `jar` 文件中包含的文件，你会使用以下格式：

```
```shell
$ jar xf myjar.jar
$ ls -al
total 20
drwxr-xr-x 3 rich rich 4096 2008-11-18 05:36 .
drwxr-xr-x 37 rich rich 4096 2008-11-18 06:23 ..
drwxr-xr-x 2 rich rich 4096 2008-11-18 06:18 META-INF
-rw-r--r-- 1 rich rich 928 2008-11-18 06:23 myjar.jar
-rw-r--r-- 1 rich rich 727 2008-11-18 06:33 MyTestClass.class
-rw-r--r-- 1 rich rich 727 2008-11-18 06:35 AnotherClass.class
$
```
```

清单文件帮助 JVM 确定 `jar` 文件中的文件以及包含 main 方法的类的位置（称为应用程序入口点）。查看 `jar` 过程创建的默认清单文件：

```
```shell
$ cd META-INF
$ ls -al
total 12
drwxr-xr-x 2 rich rich 4096 2008-11-18 05:18 .
drwxr-xr-x 3 rich rich 4096 2008-11-18 06:36 ..
-rw-r--r-- 1 rich rich 70 2008-11-18 06:18 MANIFEST.MF
$ cat MANIFEST.MF
Manifest-Version: 1.0
Created-By: 1.6.0_0 (Sun Microsystems Inc.)
$
```
```

默认清单显示的是通用信息。你可以使用该文件为 JVM 提供有关应用程序的具体说明，例如 Java 应用程序的入口点。为此，你必须创建一个要添加到 jar 文件的清单文件。`jar` 程序会将你的清单文件中的信息添加到标准清单信息中。

要指定包含 `main` 方法的类，请创建一个名为 `Manifest.txt` 的清单文件，并使用 `Main-Class:` 标签定义包含 main 类方法的类。添加文件后，你的 `Manifest.txt` 文件的内容应如下所示：

```
```text
$ cat Manifest.txt
Main-Class: MyTestClass
$
```

接下来，在创建 jar 文件时使用 Manifest.txt 文件：

```
$ jar cfm myjar.jar Manifest.txt MyTestClass.class
$
```

确保在运行此命令时新的 Manifest.txt 文件与你的 MyTestClass.class 文件位于同一文件夹中。这将重建 myjar.jar 文件，其中包含来自 Manifest.txt 文件的信息，指示测试代码中 main 方法的位置。用 jar 文件中的一个文件来做这件事似乎有点愚蠢，但如果 jar 文件中有数百个类文件，对于大型应用程序来说这种情况经常发生，那会多么令人困惑。

一旦使用清单构建了 jar 文件，你就可以将其作为应用程序分发，任何人都可以直接从 jar 文件运行你的应用程序，只需使用以下命令：

```
$ java -jar myjar.jar
The factorial of 4 is 24
$
```

无需从 jar 文件中提取类文件——JVM 可以在 jar 文件内很好地处理它们！

> 你也可以使用 -classpath 选项在知道应用程序的主类是什么的情况下从 jar 文件运行类：
> $ java -classpath myjar.jar MyTestClass
> The factorial of 5 is 120
> $
> 这允许你将类构建为库文件并将其存储在 jar 文件中，然后使用 -classpath 选项访问这些库。

## NetBeans

如今，简单的命令行编译器已经不够用了。拥有一个图形化开发环境来帮助你创建和调试程序非常有用。

Sun NetBeans IDE 包是一个免费提供的、非开源的 Java 开发包。由于它不是开源的，在 Linux 社区中有些不受欢迎。尽管如此，它是创建和排查 Java 代码的绝佳方式。

你可以直接从 Sun Microsystems 的 Java 网站 (http://java.sun.com/) 下载 NetBeans IDE 包；不过，它也可以通过 Synaptic 包管理器在 Ubuntu 软件仓库中安装。你所需要做的就是安装 netbeans 包，然后你 Ubuntu 工作站上就会安装好图形化 Java 开发所需的一切！

安装 NetBeans 后，它会出现在应用程序菜单中。按照以下步骤使用 NetBeans 编写简单的 Java 应用程序：

- 1. 启动 NetBeans 应用程序。在 Ubuntu 中启动 NetBeans，选择 面板菜单中的 Applications ▸ Programming ▸ NetBeans IDE。主 NetBeans 窗口，如图 28-2 所示，将出现。


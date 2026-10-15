
当你登录到你的账户时，系统会为你生成一个 shell。该 shell 被称为你的登录 shell 或用户 shell。当你执行脚本时，你正在生成用户 shell 的子 shell。你可以在用户 shell 中定义变量，你也可以定义可以在生成的任何子 shell 中引用的环境变量。Linux 设置了你可以用来配置用户 shell 的系统 shell 变量。其中许多系统 shell 变量由系统在你登录时定义，但你自己定义了其他变量。有关常用变量的列表，请参阅表 9-1。

一组保留的关键字用于这些系统变量的名称。你不应将这些关键字用作你自己的变量名称。系统变量全部以大写字母指定，便于识别。Shell 功能变量则使用小写字母。例如，关键字 `HOME` 由系统用来定义 `HOME` 变量。`HOME` 是一个特殊的环境变量，保存用户主目录的路径名。另一方面，关键字 `noclobber` 用于打开或关闭 `noclobber` 功能。

## System Variables

登录时由系统自动定义并赋予初始值的许多系统变量，如果你愿意，可以更改。有些系统变量的值不应更改。例如，`HOME` 变量保存你主目录的路径名。诸如 `cd` 之类的命令会引用 `HOME` 系统变量中的路径名以定位你的主目录。本节描述了其中一些更常见的系统变量。其他系统变量由系统定义并赋予初始值，你可以自由更改。要做到这一点，你需要重新定义它们并赋予新值。例如，`PATH` 变量由系统定义并赋予初始值；它包含命令所在目录的路径名。每当你执行一个命令时，shell 就会在这些目录中搜索它。你可以通过重新定义 `PATH` 变量，使其包含新目录的路径名，从而添加一个要搜索的新目录。还有其他特殊变量，系统并未定义。这些通常是可选功能，例如用于设置 Vi 编辑器选项的 `EXINIT` 变量。每次登录时，你都必须定义并为此类变量分配值。一些更常见的系统变量是 `SHELL`、`PATH`、`PS1`、`PS2` 和 `MAIL`。`SHELL` 变量保存你登录所用 shell 程序类型的路径名。`PATH` 变量列出用于搜索 Linux 命令的不同目录。`PS1` 和 `PS2` 变量保存提示符符号。`MAIL` 变量保存你的邮箱文件的路径名。你可以修改它们的任何值来自定义你的 shell。

> **NOTE** 你可以使用 `env` 命令获取当前已定义的系统变量列表。`env` 命令的工作方式类似于 `set` 命令，但它只列出系统变量。

### Using Initialization Files

你可以使用称为初始化文件的特殊 shell 脚本来自动定义系统变量。初始化文件是一个具有特殊名称的 shell 脚本，每当你进入某个 shell 时就会执行。你可以编辑初始化文件，并在其中放置系统变量的定义和赋值。当你进入 shell 时，初始化文件将执行这些定义和赋值，从而有效地用你自己的值初始化系统变量。例如，`BASH` shell 的 `.bash_profile` 文件是一个每次登录时执行的初始化文件。它包含系统变量的定义和赋值。然而，`.bash_profile` 文件基本上只是一个 shell 脚本，你可以用任何文本编辑器（如 Vi 编辑器）编辑它；如果愿意，可以更改分配给系统变量的值。

在 `BASH` shell 中，所有系统变量都设计为环境变量。当你定义或重新定义系统变量时，还需要将其导出以使其成为环境变量。这意味着你对系统变量所做的任何更改都必须伴随 `export` 命令。你会看到在登录初始化文件 `.bash_profile` 的末尾，通常会为其中定义的所有系统变量提供一个 `export` 命令。

### Your Home Directory: HOME

`HOME` 变量包含你的主目录的路径名。你的主目录由系统管理员在创建你的账户时确定。你的主目录的路径名在你登录时会自动读入你的 `HOME` 变量。在下一个示例中，`echo` 命令显示 `HOME` 变量的内容：

```
$ echo $HOME
/home/chris
```

`HOME` 变量经常在你需要指定主目录的绝对路径名时使用。在下一个示例中，使用 `HOME` 表示主目录的路径来指定 `reports` 的绝对路径：

```
$ ls $HOME/reports
```

### Command Locations: PATH

`PATH` 变量包含一系列由冒号分隔的目录路径。每次执行命令时，`PATH` 变量中列出的路径就会逐一搜索该命令。例如，`cp` 命令在系统中的目录 `/usr/bin` 中。此目录路径是 `PATH` 变量中列出的目录之一。每次你执行 `cp` 命令时，都会搜索此路径并找到 `cp` 命令。系统定义并为 `PATH` 赋予一组初始路径名。在 Linux 中，初始路径名为 `/usr/bin` 和 `/usr/sbin`。

shell 可以执行任何可执行文件，包括你创建的程序和脚本。因此，`PATH` 变量也可以引用你的工作目录；因此，如果你想在工作目录中执行自己的脚本或程序，shell 就可以找到它。字符串中路径名之间不允许有空格。没有指定路径名的冒号引用你的工作目录。通常，在路径名的末尾放置一个冒号作为空条目来指定你的工作目录。例如，路径名 `/usr/bin:/usr/sbin:` 引用三个目录：`/usr/bin`、`/usr/sbin` 和你的当前工作目录。

```
$ echo $PATH
/usr/bin:/usr/sbin:
```

place. In this example, an evaluation of `HOME` is also used to designate the user’s home directory in the new directory’s pathname. Notice the empty entry between two colons, which specifies the working directory.

```
$ PATH=$PATH:$HOME/mybin:
$ export PATH
$ echo $PATH
/usr/bin:/usr/sbin::/home/chris/mybin
```

If you add a directory to `PATH` yourself while you are logged in, the directory would be added only for the duration of your login session. When you log back in, the login initialization file, `.bash_profile`, would again initialize your `PATH` with its original set of directories. The `.bash_profile` file is described in detail a bit later in this chapter. To add a new directory to your `PATH` permanently, you need to edit your `.bash_profile` file and find the assignment for the `PATH` variable. Then, you simply insert the directory, preceded by a colon, into the set of pathnames assigned to `PATH`.

## Specifying the BASH Environment: BASH_ENV

The `BASH_ENV` variable holds the name of the `BASH` shell initialization file to be executed whenever a `BASH` shell is generated. For example, when a `BASH` shell script is executed, the `BASH_ENV` variable is checked and the name of the script that it holds is executed before the shell script. The `BASH_ENV` variable usually holds `$HOME/.bashrc`. This is the `.bashrc` file in the user’s home directory. The `.bashrc` file is discussed later in this chapter. You could specify a different file if you wish, using that instead of the `.bashrc` file for `BASH` shell scripts.

## Configuring the Shell Prompt

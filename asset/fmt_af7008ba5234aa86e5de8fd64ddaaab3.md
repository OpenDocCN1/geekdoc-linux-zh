
### 22. 比较文件内容
你需要能够比较这两个文件的内容。它们不够相似，无法使用`diff`命令。相反，你必须直接比较各项术语。由于你感兴趣的是减少可供下载的文件列表，一种很好的方法是加载文件中的每个术语，查看它是否存在于已安装的软件包中，如果不存在，则将其保存到潜在下载列表中。

你可以通过在`for`循环中巧妙使用代码来开始此过程：

```bash
package="empty"
for package in `cat lspkgs` do
```

### 23. 测试软件包安装状态
在循环内，现在你必须测试每个软件包是否已安装。你可以在`if`条件语句中使用简单的`grep`命令来执行此操作，例如：

```bash
loaded=""
loaded=`grep -c $package loadedrpms`
if [ $loaded != "" ]
    then
    echo "$package" >> donthave
fi
```

### 24. 关闭循环
通过输入`done`关闭循环。

### 25. 手动下载建议
不建议自动加载软件包，仅因为它们是可用的。即使是让脚本下载也有嫌疑，因为如果你有计量计费的互联网连接，这可能会浪费大量带宽。相反，让脚本将可用`RPM`的列表通过电子邮件发送给你，然后你可以审查、选择并手动下载。或者，编写一个脚本下载你选择的软件包。为了处理邮件，使用类似以下内容：

```bash
cat donthave | mail -s "The RPM updates not already installed" \
root@localhost
```

**注意：** 将电子邮件地址更改为适合你需求的任何内容。

### 26. 清理临时文件
清理所有临时文件是明智之举。你可能希望在单独的一个脚本中执行此操作，该脚本在此脚本运行前约 30 分钟运行。

### 27. 保存并关闭
按`Esc`键进入命令模式，然后输入`ZZ`以保存并关闭文件。

### 28. 编辑`.netrc`文件
编辑文件`~/.netrc`以分配`FTP`会话的自动登录信息。使用此格式：

```text
default login anonymous password email@address
```

**提示：** 如果你希望输入`/script`来运行此文件，请将其设置为可执行权限。

**相关解决方案：** 使用`grep`查找所需内容

发现于页码：685

## 编写你自己的用户创建脚本

要了解如何编写你自己的用户创建脚本，请执行以下操作：

1. 以`root`身份登录，因为只有`root`才能添加用户。

2. 输入`vi ~/bin/usercreate.scr`打开脚本文件进行编辑。

3. 输入`i`进入插入模式。

4. 输入以下内容以确保`Linux`知道这是一个`bash`shell脚本：

   ```bash
   #!/bin/bash
   ```

5. 确定你在创建用户账户时通常执行的基本步骤。在`Red Hat`中，这可能包括运行`useradd`然后运行`passwd`。

6. 确定你可能希望添加到脚本中的更高级步骤。例如，你可能希望能够设置`/etc/passwd`中的真实姓名字段，或设置用户希望使用的`shell`。你甚至可能希望设置主要组和附加组。

7. 有些人喜欢创建可以接受命令行所有术语的`shell`脚本。如果你记忆力不好，你可能希望你的脚本提示你输入它们所需的信息。然而，你不希望脚本问你数量惊人的问题。菜单可以解决这个问题。首先，在你选择要设置的每个选项之前，你不希望完全退出菜单。将其放在一个`while`循环中会有帮助。如果保存菜单选择的变量名为`choice`，那么你首先需要初始化它：

   ```bash
   choice="empty"
   ```

8. 现在，你必须构建菜单。你可以使用以下代码打印选项：

   ```bash
   echo "Choose one or more of the following options to set\n for your new user account\n"
   echo "[U]sername"
   echo "[P]assword"
   echo "[F]ull name"
   echo "[P]rimary group"
   echo "[A]dditional groups"
   echo "[C]hange shell"
   ```

9. 由于显示了许多值，提供当前所有设置值的列表也很有帮助。首先，将所有变量清零，即将它们设置为默认值，如下所示：

   ```bash
   user="empty"
   pass="empty"
   name="empty"
   group="empty"
   moregroup="empty"
   shell="empty"
   ```

10. 开始循环，并告诉它仅当你在菜单中选择退出时才退出：

    ```bash
    while [$choice != "Q"] do
    ```

11. 打印当前值：

    ```bash
    echo "The current values are: user = $user, name = $name,\n group = $group, additional group = $moregroup, and\n shell = $shell\n"
    ```

12. 注意，这里没有列出密码。你可能不想显示此信息。相反，你可能添加一个测试语句，以查看密码是否已设置：

    ```bash
    if [ $pass = "empty" ]
        then echo "Password is not yet set\n"
    fi
    ```

13. 构建菜单语句的骨架。使用`echo`版本作为模板。在这种情况下，它可能类似于以下内容：

    ```bash
    case $choice in
        U|u) echo "Enter valid username: "
        P|p) echo "Enter secure password: "
        F|f) echo "Enter user's full name: "
        R|r) echo "Enter the group to assign this user to: "
        A|a) echo "Enter another group to add this user to: "
        C|c) echo "Enter the shell you want this user to work within: "
    esac
    ```

    > **注意：** `C|c`格式允许用户输入大写或小写版本，因为两者都被识别为有效输入。你也不需要仅使用单个字母选择。

14. 现在你需要显示菜单。为此使用类似以下的骨架：

    ```bash
    echo "Press U to add the username"
    echo "Press P to add a password"
    echo "Press F to add a user's full name"
    echo "Press R to add this user's primary group"
    echo "Press A to add an additional group for this user"
    echo "Press C to change the user's default shell"
    ```

15. 你必须读取菜单的值以进行测试：

    ```bash
    read choice
    ```

16. 现在，你可以创建菜单如何响应用户选择的逻辑。每个菜单选项下方的空白行都对应着必须填入的更多代码。它们都需要使用相同格式的code：

```
read variable;;
```

填入代码后，该`case`语句看起来将如下所示：


12. 现在通过输入 `printenv | more` 查看你的环境变量列表。再次在滚动列表时仔细观察。这次你看到了 `MYVAR`。

13. 输入 `clear` 并按 Enter 清除列表，为下一个项目做准备。

```
mpalmer@localhost:~~
File Edit View Tabs Help
[mpalmer@localhost ~$] ./testscript

[mpalmer@localhost ~$] export MYVAR
[mpalmer@localhost ~$] ./testscript
[mpalmer@localhost ~$] 
```

## 项目 6-5

在实项目 6-4 中，你必须在 `testscript` 前使用 `./`，因为你的当前工作目录不在 `PATH` 环境变量中。在这个项目中，你查看 `PATH` 变量的内容。接下来，你将当前工作目录添加到 `PATH` 变量中，并在不使用 `./` 字符运行 `testscript`。

**查看 PATH 内容：**

1. 输入 `echo $PATH` 并按 Enter。

你看到了目录列表。注意路径名称是用冒号 (`:`) 分隔的。

**将当前工作目录添加到 PATH 变量：**

1. 输入 `PATH=$PATH:.` 并按 Enter。
2. 输入 `echo $PATH` 并按 Enter。点 (`.`) 现在已添加到列表末尾。
3. 现在你可以在当前工作目录下运行脚本，而无需在它们前面输入 `./characters`。只需输入 `script` 并按 **Enter** 即可。你可以看到脚本正在执行，如图 6-9 所示。

![](img/0a988e998d76ede7c21a57edbc89e490_338_0.png)

**图 6-9** 将当前工作目录添加到 PATH 变量中以运行 shell 脚本

## 项目 6-6

在这个项目中，你将进一步获得使用顺序逻辑编写非常简单的 shell 脚本的经验。在这些步骤中，你将创建一个 shell 脚本 `seqtotal`。

**演示顺序逻辑：**

1. 输入 `vi` `seqtotal` 并按 **Enter**。
2. 输入 `i` 进入到 `vi` 的插入模式。
3. 输入以下行：

```
let a=1
let b=2
let c=3
let total=a+b+c
echo $total
```

4. 按 **Esc** 切换到 `vi` 的命令模式。
5. 输入 `:x` 并按 **Enter** 保存文件并退出 `vi`。

### 动手项目 319

6. 接下来测试新的 shell 脚本 `seqtotal`。输入 `sh seqtotal` 并按 Enter。

你将看到脚本的输出，结果为 6。

## 项目 6-7

这个项目将向你首次介绍如何在 shell 脚本中使用 `if` 语句，并演示决策逻辑。在第一组步骤中，你创建一个使用基础 `if` 语句的脚本。在第二组步骤中，你修改脚本以包含一个嵌套在内部 `if` 语句。

为了演示 `if` 语句并实现决策逻辑：

1. 输入 `vi veg_choice` 并按 Enter。
2. 输入 `i` 切换到 `vi` 的插入模式。
3. 输入以下行：

```
echo -n "What is your favorite vegetable? "
read veg_name
if [ "$veg_name" = "broccoli" ]
then
echo "Broccoli is a healthy choice."
else
echo "Don't forget to eat your broccoli also."
fi
```

4. 确保你的编辑界面看起来如图 6-10 所示。按 `Esc` 切换到 `vi` 命令模式。
5. 通过输入 `chmod ug+x veg_choice` 并按 Enter 使脚本可执行。接下来，通过 `./veg_choice` 并按 Enter 运行脚本。
6. 当被要求输入你喜欢的蔬菜名称时，输入 `broccoli`。
7. 再次运行脚本并输入 `corn` 或其他蔬菜名称进行响应。

> 记住，你必须先使用 `chmod` 命令使脚本可执行。然后在命令提示符后，输入脚本名称的路径来执行。运行脚本的另一种方法是使用 `sh` 命令，就像你处理 `seqtotal` 脚本时做的那样。在使用 `chmod` 命令后，第三种替代方案是将当前工作目录添加到你的路径中，正如你在动手项目 6-5 中学会的那样。然后只需输入脚本名称即可运行。

# 第 6 章 Shell 脚本编程简介

![](img/0a988e998d76ede7c21a57edbc89e490_340_0.png)

# 图 6-10 创建 veg_choice 脚本

为了练习编写嵌套 `if` 语句：

1. 在 `vi` 或 `Emacs` 中打开 `veg_choice` 文件。
2. 编辑文件使其包含以下行。

```
echo -n "What is your favorite vegetable?"
read veg_name
if [ "$veg_name" = "broccoli" ]
then
    echo "Broccoli is a healthy choice."
else
    if [ "$veg_name" = "carrots" ]
then
    echo "Carrots are great for you."
else
    echo "Don't forget to eat your broccoli also."
fi
```

3. 执行脚本并回答 `carrots`。你应该看到“Carrots are great for you.”
4. 输入 `clear` 并按 Enter 清除屏幕进入下一个项目。

## 项目 6-8

在这个项目中，你学习如何在 shell 脚本和命令行中使用 `for` 循环，演示循环逻辑的工作。

为了在 shell 脚本中演示循环逻辑：

1. 使用 `vi` 或 `Emacs` 创建文件 `_users`。
2. 在文件中输入以下行：

```
for USERS in john tom becky eliill
echo $USERS
```

3. 保存文件并退出编辑器。
4. 赋予文件权限并运行它。结果应该与图 6-11 所示。

![](img/0a988e998d76ede7c21a57edbc89e490_341_0.png)

**图 6-11** 运行 `_users` 脚本执行 `for` 循环

为了在命令行输入相同的 `for` 循环：

1. 在命令行输入 `for USERS in john tom becky eliill` 并按 Enter。
2. 在 `>` 提示符输入 `do` 并按 Enter。
3. 输入 `echo $USERS` 并按 Enter。
4. 输入 `done` 并按 Enter。你在屏幕上看到了？
5. 输入 `clear` 并按 Enter 清除屏幕进入下一个项目。

## 项目 6-9

在这个项目中，你创建一个 `for` 循环并使用通配符格式遍历 `for` 语句中的每个元素，这由 `chapters` 组成。你首先创建 `chap4`。然后，你使用 `more` 命令显示每个文件的内容。

为了在 `for` 循环中使用通配符：

1. 输入 `cat > chap1` 并按 Enter。
2. 输入 `This is chapter 1` 并按 Enter。
3. 输入 `Ctrl+d`。创建 `chap1`。
4. 输入 `cat > chap2` 并按 Enter。
5. 输入 `This is chapter 2` 并按 Enter。
6. 输入 `Ctrl+d`。创建 `chap2`。
7. 输入 `cat > chap3` 并按 Enter。
8. 输入 `This is chapter 3` 并按 Enter。
9. 输入 `Ctrl+d`。创建 `chap3`。
10. 输入 `cat > chap4` 并按 Enter。
11. 输入 `This is chapter 4` 并按 Enter。
12. 输入 `Ctrl+d`。创建 `chap4`。
13. 使用 `vi` 或 `Emacs` 编辑器创建 shell 脚本 `chapters`。脚本应该包含这些行：

```
for file in chap[1234]; do
  more $file
done
```

14. 保存文件并退出编辑器。
15. 赋予文件权限并测试它。你看到类似于图 6-12 的输出。

## 项目 6-10

`while` 语句是 `for` 语句之外循环逻辑的另一个例子。在这个项目中，你创建一个包含基础 `while` 语句的 shell 程序。接下来，你创建一个可能用于屏幕数据输入表的 shell 程序，在平面数据文件中存储信息。

# 动手项目 323



```
alias ll='ls -l'
alias ls='/bin/ls -F'
alias mail=Mail
alias mailq='/usr/lib/sendmail -bp'
alias newaliases='echo you mean newalias..'
alias rn='/usr/local/bin/rn -d$HOME -L -M =m -e -S -/'
alias intuitive='echo Intuitive.com; \
echo ''MyPassWord.'' | pbcopyssh dtaylor@intuitive.com'
```

还请注意，shell 总是按字母顺序显示别名列表，而不考虑它们定义的顺序。

其中大多数别名很容易理解。例如，第一个别名 diff 确保 diff 命令始终具有默认标志 -c 和 -w。如果我输入 from，我希望系统调用 frm -n；如果我输入 ll，我希望系统调用 ls -l；依此类推。

## 2. 有些命令如果输入可能会造成麻烦，因此为每个这样的命令创建别名是避免麻烦的好方法。例如，我为 newaliases 创建了一个别名；如果我不小心输入了该命令，系统会温和地提醒我，我可能想使用 newalias 命令：

```
$ newaliases
you mean newalias..
```

## 3. 我为连接到其他系统上的账户创建了别名。我喜欢为每个别名命名为我所连接的系统（例如 intuitive）：

Click here to view code image

```
$ alias intuitive
alias intuitive='echo Intuitive.com;echo ''MyPassWord.'' | pbcopyssh dtaylor@intuitive.com'
```

用分号分隔命令是 Unix 在单行上执行多个命令的方式，因此当我输入别名 sunworld 时，就好像我一个接一个地输入了以下所有命令：

```
echo Intuitive.com
echo 'MyPassWord.' | pbcopy
ssh dtaylor@intuitive.com
```

> 在你太兴奋之前，不，“MyPassWord.” 并不是我的真实账户密码！

使用别名是真正自定义命令界面的好方法。我总是调整命令集和默认标志。（例如，看看我为 rn 命令设置的默认值的选项。）我甚至有效地禁用了我不想意外输入的命令。

让你的想象力在别名上尽情发挥！如果你决定真的喜欢其中一个并且你使用的是 bash，就将该别名添加到你的 .bashrc 文件中以使其永久生效。（如果你愿意，也可以将其放入你的 .profile 文件中。）如果你想让系统暂时“忘记”一个别名，可以使用 unalias 命令，它就会在你再次登录之前消失。例如，unalias intuitive 将暂时从 shell 中移除前面显示的 intuitive 别名。

## Task 14.5: Setting Custom Prompts

到目前为止，你看到的命令提示符是一个无聊的 $。事实证明 bash 允许你将提示符设置为几乎任何可能的值，使用 PS1="value"。请注意 PS1 必须全部大写才能生效。

- 1. 我厌倦了 Unix 如此直白和不礼貌。幸运的是，我很容易就能改变它对我的回应方式：

```
$ PS1="Yes, master? "
Yes, master?
```

这才像话！

- 2. 你可以在提示符中隐藏很多有用的东西，它们都采用 \x 的形式。第一个有用的变量是 \w，它保存当前工作目录：

Click here to view code image

```
Yes, master? PS1="In \w, oh master: "
In /users/taylor, oh master:
```

如果我更改目录会怎样？

Click here to view code image

```
In /users/taylor, oh master: cd /
In /, oh master:
```

酷吧？

- 3. 有很多不同的变量可以添加，其中最有用的显示在表 14.2 中。

| Value | Expands to |
| --- | --- |
| \d | The date, in Weekday Month Day format (example: Thu Feb 1) |
| \H | The full system hostname (example: limbo.intuitive.com) |
| \h | The system name (example: limbo) |
| \n | Carriage return sequence (yes, you can have a two-line prompt, if you want!) |
| \s | The name of the shell (example: bash2.4) |
| \T | Current time, in HH:MM:SS format (example: 04:23:28) |
| \t | Same as \T, but in 24 hour format (example: 16:23:28) |
| \@ | Current time in am/pm format (example: 04:23pm) |
| \u | Username of the current user (example: taylor) |
| \w | Current working directory (example: /home/taylor/bin) |
| \W | Base name of current directory (example: bin) |

### TABLE 14.2 Special Values for the System Prompt

还记得你本小时早些时候学到的使用命令编号来重复命令的方法吗（如 !37 重复第 37 条命令）？事实证明还有一个


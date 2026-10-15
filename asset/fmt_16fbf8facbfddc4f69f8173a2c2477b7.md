
47. 如果你当前的 shell 是 Korn，执行以下每个命令将显示什么？

a. `a=44 c; print a ; print $a`

b. `b=44 c; print aa ; print $a`

c. `c=44 c; print "$a" ; print $aa`

48. 执行以下命令将显示什么？

a. `a=44 c; print a ; print $a`

b. `b=44 c; print aa ; print $a`

c. `c=44 c; print "$a" ; print $aa`

*注：原文中47和48题的选项完全重复，此处已按原文逐行呈现。*

49. 什么是选项（option）？列出一些选项及其用途。

50. Korn shell 中的启动脚本（文件）是什么？

# 实验

41. 下列命令中哪一个显示你的登录 shell？（参见第 5 章。）

a. `print $SHELL`

b. `print $0`

c. `print $shell`

d. `print $login_shell`

42. 下列命令中哪一个创建一个 Korn shell？（参见第 5 章。）

a. `sh`     c. `csh`

b. `ksh`     d. 以上都不是

43. 下列哪一个是输入流的描述符？哪一个是输出流的描述符？哪一个是错误流的描述符？

a. `1`     c. `2`

b. `2`     d. `3`

44. 识别至少两个不能与输入重定向使用的命令。

45. 下列哪一个是有效的 Korn shell 变量？

a. `cat`     c. `Var-1`

b. `_first`  d. `2Var`

46. 如果你当前的 shell 是 Korn，以下命令中每个命令的错误（如果有）是什么？

a. `a = 24`     c. `a=$b`

b. `set a=24`   d. `a=$b`

47. 如果你当前的 shell 是 Korn，执行以下每个命令将显示什么？

a. `a=44 c; print a ; print $a`

b. `b=44 c; print aa ; print $a`

c. `c=44 c; print "$a" ; print $aa`

48. 执行以下命令将显示什么？

a. `a=44 c; print a ; print $a`

b. `b=44 c; print aa ; print $a`

c. `c=44 c; print "$a" ; print $aa`

49. 什么是选项（option）？列出一些选项及其用途。

50. Korn shell 中的启动脚本（文件）是什么？

# 练习

41. 下列命令中哪一个显示你的登录 shell？（参见第 5 章。）

a. `print $SHELL`

b. `print $0`

c. `print $shell`

d. `print $login_shell`

42. 下列命令中哪一个创建一个 Korn shell？（参见第 5 章。）

a. `sh`     c. `csh`

b. `ksh`     d. 以上都不是

43. 下列哪一个是输入流的描述符？哪一个是输出流的描述符？哪一个是错误流的描述符？

a. `1`     c. `2`

b. `2`     d. `3`

44. 识别至少两个不能与输入重定向使用的命令。

45. 下列哪一个是有效的 Korn shell 变量？

a. `cat`     c. `Var-1`

b. `_first`  d. `2Var`

46. 如果你当前的 shell 是 Korn，以下命令中每个命令的错误（如果有）是什么？

a. `a = 24`     c. `a=$b`

b. `set a=24`   d. `a=$b`

47. 如果你当前的 shell 是 Korn，执行以下每个命令将显示什么？

a. `a=44 c; print a ; print $a`

b. `b=44 c; print aa ; print $a`

c. `c=44 c; print "$a" ; print $aa`

48. 执行以下命令将显示什么？

a. `a=44 c; print a ; print $a`

b. `b=44 c; print aa ; print $a`

c. `c=44 c; print "$a" ; print $aa`

19. 什么是命令替换？在 Korn shell 中，命令替换的标记（token）是什么？

20. 什么是作业（job）？区分前台作业和后台作业。（参见第 5 章。）

21. 展示你如何将一个作业从后台移动到前台，反之亦然。（参见第 5 章。）

22. 列出并解释作业的六种不同状态。（参见第 5 章。）

23. 定义一个变量，并区分变量和值的区别。

24. 区分用户定义变量和预定义变量。

25. 区分 shell 变量和环境变量。哪一个会自动导出到子 shell（subshells）？

26. 识别本章中为 Korn shell 定义的所有环境变量名称。

27. 命令的退出状态（exit status）是什么？它存储在哪里？

28. 在 Korn shell 中，哪个环境变量持有你命令的搜索路径？你如何显示该变量的值？

29. 在 Korn shell 中，哪个环境变量持有登录 shell（login shell）名称？你如何显示该变量的值？

30. 在 Korn shell 中，哪个环境变量持有 `cd` 命令的搜索路径？你如何显示该变量的值？

31. 在 Korn shell 中，哪个环境变量持有主提示符（primary prompt）？你如何显示该变量的值？

32. 在 Korn shell 中，哪个环境变量持有次提示符（secondary prompt）？你如何显示该变量的值？

33. 在 Korn shell 中，哪个环境变量持有你家目录的路径？你如何显示该变量的值？

34. 在 Korn shell 中，哪个环境变量持有邮件检查间隔？你如何显示该变量的值？

35. 在 Korn shell 中，哪个环境变量持有你邮箱箱的路径？你如何显示该变量的值？

36. 在 Korn shell 中，哪个环境变量持有默认编辑器的路径？你如何显示该变量的值？

37. 在 Korn shell 中，哪个环境变量持有你的登录名？你如何显示该变量的值？

38. 在 Korn shell 中，哪个环境变量持有你终端的类型？你如何显示该变量的值？

39. 什么是选项（option）？列出一些选项及其用途。

40. Korn shell 中的启动脚本（文件）是什么？

# 练习

41. 下列命令中哪一个显示你的登录 shell？（参见第 5 章。）

a. `print $SHELL`

b. `print $0`

c. `print $shell`

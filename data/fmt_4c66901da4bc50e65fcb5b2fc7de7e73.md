
- 如果你指定三个值，序列从第一个值开始，每次递增第二个值，并在第三个值处结束。
- 你可以处理文本流，以在脚本或管道中操作和修改文本。
- 你可以使用以下实用工具来处理文本流：
  - `cut`
  - `expand`
  - `unexpand`
  - `fmt`
  - `join`
  - `paste`
  - `nl`
  - `od`
  - `pr`
  - `sed`
  - `awk`
  - `sort`
  - `split`
  - `tr`
  - `uniq`
  - `wc`

#### 问题

1. 以下哪个元素必须包含在每个 shell 脚本的开头？
   A. `#Comment`
   B. `#!/bin/bash`
   C. `exit 0`
   D. `#begin script`

2. 你已在用户主目录中创建了一个名为 `myscript` 的 Shell 脚本。如何执行它？（选择两项。）
   - A. 在 Shell 提示符下输入 `bin/bash ~/myscript`。
   - B. 在 Shell 提示符下输入 `myscript`。
   - C. 在图形桌面中选择“计算机 | 运行”；然后输入 `~/myscript` 并选择“运行”。
   - D. 在 Shell 提示符下输入 `run ~/myscript`。
   - E. 输入 `chmod u+x ~/myscript`；然后在 Shell 提示符下输入 `~/myscript`。

3. 哪个命令可以创建一个名为 `TOTAL` 的新变量并将其类型设置为“整数”？
   - A. `variable -i TOTAL`
   - B. `declare -i TOTAL`
   - C. `declare TOTAL -t integer`
   - D. `TOTAL=integer`

4. 你需要在 Shell 脚本中在屏幕上显示文本“Hello world”。哪个命令可以实现这一点？
   - A. `echo "Hello world"`
   - B. `read Hello world`
   - C. `writeln "Hello world"`
   - D. `print 'Hello world'`

5. 在 Shell 脚本内部，你需要提示用户输入他们的电话号码。你需要将他们输入的值分配给名为 `$PHONE` 的变量。哪个命令可以实现这一点？
   - A. `read "What is your phone number?" $PHONE`
   - B. `read $PHONE`
   - C. `read PHONE`
   - D. `? "What is your phone number?" PHONE`

6. 哪个命令可以在 `if/then/else` 结构中用于评估指定条件是否为真？
   - A. `eval`
   - B. `==`
   - C. `test`
   - D. `<>`

7. 在 Shell 脚本的 `if/then/else` 结构中，如果变量 `num1` 小于变量 `num2`，哪个命令的求值结果为 `True`？
   - A. `eval num1 < num2`
   - B. `test num1 < num2`
   - C. `test num1 -lt num2`
   - D. `test "num1" != "num2"`
   - E. `eval "num1" != "num2"`

8. 在 Shell 脚本中，你需要提示用户从使用 `echo` 命令列出的七个不同选项中选择一个。哪种控制结构最适合评估用户的输入并运行相应的命令组？
   - A. `while` 循环
   - B. `for` 循环
   - C. `until` 循环
   - D. `if/then/else`
   - E. `case`

9. 哪种控制结构会不断重复处理，直到指定条件求值为假为止？
   - A. `while` 循环
   - B. `for` 循环
   - C. `until` 循环
   - D. `if/then/else`
   - E. `case`

10. 哪些控制结构被认为是分支结构？（选择两项。）
    - A. `while` 循环
    - B. `for` 循环
    - C. `until` 循环
    - D. `if/then/else`
    - E. `case`

11. 哪种控制结构会不断重复处理，只要指定条件求值为假？
    - A. `while` 循环
    - B. `for` 循环
    - C. `until` 循环
    - D. `if/then/else`
    - E. `case`

12. 哪种控制结构会处理指定次数？
    - A. `while` 循环
    - B. `for` 循环
    - C. `until` 循环
    - D. `if/then/else`
    - E. `case`

13. 考虑以下 `seq` 命令的使用方式：“`seq 3 9`”。该命令将生成什么数字序列？
    - A. 3, 4, 5, 6, 7, 8, 9
    - B. 3, 6, 9
    - C. 1, 4, 7, 10, 13, 16, 19, 22, 25
    - D. 9, 18, 27

14. 哪个命令可用于将文件中你指定的列或字段使用 `Tab` 字符作为分隔符打印到标准输出？
    - A. `cut`
    - B. `pr`
    - C. `fmt`
    - D. `sort`

15. 哪个命令可用于处理文本流并删除所有 `Tab` 字符实例并用八个空格替换？
    - A. `cut`
    - B. `replace -t 8`
    - C. `expand`
    - D. `unexpand`

16. 哪个命令可以处理文件或文本流，并在每一新行的开头添加一个数字？
    - A. `join`
    - B. `paste`
    - C. `fmt`
    - D. `nl`

17. 你想将当前目录下 `logfile.txt` 文件的内容发送到 `sort` 命令以按字母顺序排序并在屏幕上显示。哪些命令可以实现这一点？（选择两项。）
    - A. `sort < logfile.txt`
    - B. `sort logfile.txt`
    - C. `sort < logfile.txt -o "screen"`
    - D. `sort < logfile.txt > screen`
    - E. `sort -n logfile.txt`

18. 你想在屏幕上显示 `/var/log/messages` 文件中包含 `syslog` 一词的行的第六、第七和第八个单词。以下哪个命令可以实现这一点？
    - A. `cat /var/log/messages | awk '/syslog/ {print $6,$7,$8}'`
    - B. `cat /var/log/messages | awk '/syslog/ {print 6,7,8}'`
    - C. `cat /var/log/messages | awk '/syslog/ {print $6,$7,$8}`
    - D. `cat /var/log/messages | awk '/syslog {print 6,7,8}'`

#### 答案

1. B. 每个 `bash` Shell 脚本的开头都必须包含 `#!/bin/bash` 元素。
2. A, E. 你可以输入 `/bin/bash ~/myscript` 或 `chmod u+X ~/myscript` 来使脚本可执行。
3. B. `declare -i TOTAL` 命令将创建 `TOTAL` 变量并将其类型定义为整数。
4. A. `echo 'Hello world'` 命令将在 Shell 脚本中的屏幕上显示文本 `'Hello world'`。
5. C. Shell 脚本中的 `read PHONE` 命令将用户输入的值分配给名为 `$PHONE` 的变量。
6. C. `test` 命令可以在 `if/then/else` 结构中用于评估指定条件是否为真。
7. C. 如果变量 `num1` 小于变量 `num2`，`test num1 -lt num2` 命令在 `if/then/else` 结构中的求值结果为 `True`。
8. E. `case` 结构是评估用户多项选择并运行相应命令组的最优选项。
9. A. `while` 循环会不断重复处理，直到指定条件求值为假。
10. D, E. `if/then/else` 和 `case` 结构被认为是分支结构，因为它们根据指定条件的求值结果将脚本分支到几个方向之一。
11. C. `until` 循环控制结构会不断重复处理，只要指定条件求值为假。
12. B. `for` 循环控制结构会处理指定次数。
13. A. `seq 3 9` 命令将生成以下数字序列：3, 4, 5, 6, 7, 8, 9。第一个数字指定起始数字，第二个数字指定序列中的结束数字。由于未指定增量，序列以 1 为增量递增。
14. A. `cut` 命令可用于使用 `Tab` 字符作为分隔符将文件中你指定的列或字段打印到标准输出。
15. C. `expand` 命令可用于处理文本流并删除所有 `Tab` 字符实例并用八个空格替换。
16. D. `nl` 命令可用于处理文件或文本流，并在每一新行的开头添加一个数字。



| 功能 | C/TC | Bourne | Bash | Korn |
|---|---|---|---|---|
| 编程结构（续） | | | | |
| if/else/elif 条件 | if (expression) then commands else if (expression) then commands else commands endif | if command then commands elif command then commands else commands fi | if command then commands elif command then commands else commands fi | if command then commands elif command then commands else commands fi |
| goto | goto label :label: | N/A | N/A | N/A |
| switch 和 case | switch ("$value") case pattern1: commands breaksw case pattern2: commands breaksw default: commands breaksw endsw | case "$value" in pattern1) commands ;; pattern2) commands ;; esac | case "$value" in pattern1) commands ;; pattern2) commands ;; esac | case "$value" in pattern1) commands ;; pattern2) commands ;; esac |
| 循环 | | | | |
| while | while (expression) commands end | while command do commands done | while command do commands done | while command do commands done |
| for/foreach | foreach var (wordlist) commands end | for var in wordlist do commands done | for var in wordlist do commands done | for var in wordlist do commands done |
| until | N/A | until command<br>do commands<br>done | until command<br>do commands<br>done | until command<br>do commands<br>done |
| repeat | repeat 3 'echo "Hello"'<br>Hello<br>Hello<br>Hello | N/A | N/A | N/A |
| select | N/A | N/A | PS3="Please select a menu item"<br>select var in wordlist<br>do commands<br>done | PS3="Please select a menu item"<br>select var in wordlist<br>do commands<br>done |

## 索引

### 符号

- ! 命令，129
- $，527，528
- $* 变量：
  - 与 $# 变量对比，331
  - 与 Bash 的词列表，906
  - 与 Bourne shell 的词列表，352
  - 与 Korn shell 的词列表，689
- $< 变量，528
- $? 变量：
  - C shell，539
  - Korn shell，668
- $@ 变量：
  - 与 $* 变量对比，331
  - 与 Bash 的词列表，906
  - 与 Bourne shell 的词列表，352
  - 与 Korn shell 的词列表，689
- $0 变量，167
- ? 变量，889
- -a GNU grep 选项，114

### 数字

- 022 umask 值，19
- 666 权限，19
- 777 权限，19

### A

- a 命令，129，143
- -A GNU grep 选项，114
- 访问权限：
  - 用户和组标识，18
  - 另见权限
- 动作：
  - awk，172
  - awk 简单动作示例，179
  - 模式和，182
- 地址，128
- 别名替换：
  - 反斜杠，642
  - 定义时，10
- 别名：
  - Bash，798
  - C shell，418
  - 命令类型评估顺序，10
  - 创建：
    - Bash，798
    - C shell，605
    - Korn shell，492
  - 调试和狡猾的别名，973
  - 已定义，10
  - 删除：
    - Bash，799
    - Korn shell，605
    - TC shell，493
  - 创建错误消息，544
  - 函数和 Korn shell，641
  - Korn shell，604
  - 列出：
    - Bash，798
    - C shell，491
    - Korn shell，604
    - TC shell，491
- 与号：
  - awk，191
  - 后台作业，423
  - sed，133
- 追加：
  - 数组和下标，453
  - C shell 变量扩展，451
  - 输出到现有文件，436
  - sed，143
- apropos 实用程序，1055
- arch 实用程序，1055
- 参数：
  - Bash，59
  - C shell，36
  - 命令行：
    - gawk，271
    - nawk，239
  - 函数参数和返回值，373
  - 调用，740
  - Korn shell，51
- argv：
  - ARGV 数组和 nawk，239
  - 位置参数，534
- 算术：
  - awk，190
  - Bash，60，871
  - bc 实用程序，1057
  - Bourne shell，44，325
  - 内置函数，246
  - C shell，37，529
  - 展开，837
  - 浮点：
    - Bash，874
    - Bourne shell，327
    - C shell，530
    - Korn shell，51，660
  - let 命令，678
  - 另见递减运算符；递增运算符
- 算术运算符：
  - awk，191，197
  - C shell，529
- 数组：
  - awk，233–239
  - Bash，59，838
  - Bourne shell，43
  - C shell，36，447
  - declare -a 命令，59
  - Korn shell，51，707–709
  - set -A 命令，51
  - set 命令，43
  - shift 命令，36
    - C shell，448
    - Korn shell，709
  - 字符串，C shell，449
- 赋值运算符，201，204
- 结合性和 C shell，537
- 星号元字符，73
  - Bash，802
  - Bourne shell，291
  - C shell，427
  - egrep，95
  - GNU，95
  - GNU egrep，105
  - GNU grep，101
  - grep，90
  - Korn shell，610
  - sed，132
- at 实用程序，1056
- 身份验证：
  - awk 数据验证程序，192
  - init 进程，9
- autolist 变量：
  - 定义，515
  - 示例，483，487
  - TC shell，482
- Korn shell 中的自动加载函数，714
- awk：
  - $0 变量，167
  - 动作示例，179
  - 动作，172
  - 算术运算符，191，197
  - 数组，233–239
  - 赋值运算符，201，204


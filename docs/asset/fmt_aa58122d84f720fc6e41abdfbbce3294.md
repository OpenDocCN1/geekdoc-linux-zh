
`number_of_characters_in_this_file=$(wc -c $INPUT)`

`print` "Number of characters in this script: $number_of_characters_in_this_file"

### EXAMPLE 2

```ksh
print "Now let's do something that is not quite easy: "

print "We want to count the number of times that 'z' is found in this script"

# 此脚本包含另外两处：Z Z

number_of_z=$(wc -l -r record)

after_the_substitutions=$(echo "$record" | sed 's/[^z]//g')

# 见下文：关于 SED

length=$((#number_of_z + ${length}))done < $INPUT
```

### EXAMPLE 3

```ksh
print "Number of z's in this script is $number_of_z"

print "Count the number of letters (OR digits or punctuation marks) in a string.

print "When some of you are asking, would this Ever be useful?"

print "this is useful putting weird information into fields just to see if"

print "your program is sophisticated enough to catch it."

print "For example, perhaps you need to validate the information in an address."

print "The address might contain special characters: RR3"

print "(If you've ever lived in Nebraska, or Kansas, you know that"

print "RR3 stands for 'Rural Route Number 3'. For those of you who live in the"

print "Bronx, the word 'rural' means 'past' (an area with pastures, farms)."

print "SEE ALSO: validate_user_input.ksh"

print "SELECT: length.ksh\n"
```

```ksh
string_abc=DEF; 1:

print "Here's the string we're going to count: $string"

after_the_substitutions=$(echo "$string" | sed 's/[^A-Za-z]//g')

length=${#after_the_substitutions}

print "Number of alphabetic characters in your string: $length"

after_the_substitutions=$(echo "$string" | sed 's/[^0-9]//g')

print "Number of digits in your string: $length"
```

```ksh
after_the_substitutions=$(echo "$string" | sed 's/[^punct:]g')

length=${#after_the_substitutions}

print "punctuation marks in your string: $length"
```

```ksh
length="$(echo string)"

print length of your string: $length
```

```ksh
print "\nDONE. Script: 0\n"
```

### 关于 SED

以下行代码为我们承担了大量工作；让我们看下：
`after_the_substitutions="$(echo record | sed '/^[::]//g')"`
`sed` - 工具。它的一个小功能是：
the ability to change a string or record.
The 's' means 'substitute'.
The 'g' means 'make all substitutions'.
The slashes (`/`) separate what we are looking for
from what we want to change.
therefore, if you see `s/this/that/g`, it means Every time see
'word' change to 'that'
if you see `s/this//`, Every time see
'word' change to null (There's no space between the two slashes!)
if you see `s/[^A]//`, which means "Every time see
anything that is NOT (A) a, change it to null (nothing)
if all of substitutions occur, the only thing left in
record is either (record no Z's) or more Z's.
the data field in the variable name and then add number to counter.

### 关于 SED 的结束

输出：`characters.OUTPUT`
脚本执行方式 `./count_characters.ksh`
输出如下：

Comment: This is script `./count_characters.ksh`.

PURPOSES:
1. 统计文件中字符的数。
2. 统计特定字符在文件中出现的次数。
3. 统计字符串中字母（或数字或标点符号）的数量。

#### EXAMPLE 1

有两种简单的方法可以确定此脚本字符的数量：
1. `-c count_characters.ksh`
2. `wc -c count_characters.ksh`
此脚本字符的数量为：43

#### EXAMPLE 2

现在让我们做一些不太简单的事情：
我们要统计 'z' 在此脚本中出现的次数
此脚本中 z 的数量是16

#### EXAMPLE 3

统计字符串中字母（或数字或标点符号）的数量。
“当你们中有些人在问时，这真的有用吗？”
将奇怪的信息放入字段中是有用的，这样可以看看
你的程序是否足够复杂以捕捉它。
例如，也许你需要验证地址中的信息。
地址可能包含特殊字符：RR3
（如果你曾经住过内布拉斯加州或堪萨斯州，你就知道
RR3 代表“3号乡村路线”）。对于你们中住在布朗克斯的人来说，
“rural”一词意味着“过去”（一个有牧场、农场的区域）。
参见：`validate_user_input.ksh`
选择：`length.ksh\n`

这是我们要统计的字符串：`abc;123!`
字符串中的字母数量：6
字符串中的数字数量：3
字符串中的标点符号数量：2
字符串的长度：13

DONE. Script: `./count_characters.ksh`

```ksh
#!/bin/ksh

# PROGRAM: count_lines.ksh

# PURPOSES:

# 1. 统计文件的行数。

# 2. 统计包含特定单词的行数。

# PROGRAMMER: Larry Smith. 由于 __date__ 修订。

# DIFFICULTY: LEVEL

# USAGE: Example: ./count_lines.ksh

# NOTES:

# END.
```

```ksh
clear 清空用户的屏幕。

print "#Comment: This is script $0\n"

print "#1. 统计文件的行数"

print "#2. 统计包含特定单词的行数。"
```

```ksh
print "INTEREST,我们将使用 -l 来统计此脚本的行数：

number_of_lines_in_this_script=$($1 - 1 < count_lines.ksh)

print "此脚本的行数是 $($number_of_lines_in_this_script)"
```

```ksh
print "UNNEST,我们将使用 grep -c 来统计此脚本中包含 'this' 单词的行数："
```

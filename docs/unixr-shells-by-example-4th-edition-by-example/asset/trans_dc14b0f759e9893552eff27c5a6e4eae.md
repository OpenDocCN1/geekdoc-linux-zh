

## 表 2.4 Bash Shell 语法和结构（续）

| 循环（续） | 示例 |
|---|---|
| while command<br>do<br>block of statements<br>done | while [[ string expression ]]<br>do<br>block of statements<br>done |
| while (( numeric expression ))<br>do<br>block of statements<br>done | for variable in word_list<br>do<br>block of statements<br>done |
| for color in red green blue<br>do<br>echo $color<br>done | until command<br>do<br>block of statements<br>done |
| until [[ string expression ]]<br>do<br>block of statements<br>done | until (( numeric expression ))<br>do<br>block of statements<br>done |
| select variable in word_list<br>do<br>block of statements<br>done | PS3="Select an item from the menu"<br>for item in blue red green<br>Shows menu:<br>1-blue<br>2-red<br>3-green<br>echo $item<br>done |

## 函数

函数允许你定义一段 shell 代码并为其命名。有两种格式，一种来自 Bourne shell，另一种是 Bash 版本，使用 function 关键字。

### 示例

```
function_name() {
  block of code
}

function function_name {
  block of code
}
----------------
function lister {
  echo Your present working directory is `pwd`
  echo Your files are:
  ls
}
```

## 2.6.1 Bash Shell 脚本

```bash
#!/bin/bash
# GNU bash version 2.x
# The Party Program—Invitations to friends from the "guest" file
guestfile=~/shell/guests
if [[ ! -e "$guestfile" ]]
then
    printf "${guestfile##*/} non-existent"
    exit 1
fi
export PLACE="Saronitin's"
(( Times=$(date +%H) + 1 ))
declare -a foods=(cheese crackers shrimp drinks "hot dogs" sandwiches)
declare -i n=0
for person in $(cat $guestfile)
do
    if [[ $person == root ]]
    then
        continue
    else
        # Start of here document
        mail -v -s "Party $person" <<- FINIS
        Hi $person! Please join me at $PLACE for a party!
        Meet me at $Time o'clock.
        I'll bring the ice cream. Would you please bring
        ${foods[$n]} and anything else you would like to eat?
        Let me know if you can make it.
                         Hope to see you soon.
                                  Your pal,
                                  ellie@$hostname
        FINIS
        n=n+1
        if (( ${#foods[*]} == $n ))
        then
            n=0
        fi
    fi
done
printf "Bye..."
```

## 2.6 Bash Shell 结构

### 解释

- 1. 这一行让内核知道你正在运行一个 Bash shell 脚本。
- 2. 这是一条注释。shell 会忽略它，但对于任何试图理解脚本正在做什么的人来说都很重要。
- 3. 变量 guestfile 被设置为名为 guests 的文件的完整路径名。
- 4. 这一行读作：如果文件 guest 不存在，则向屏幕打印“guests non-existent”并退出脚本。
- 5. 内置的 printf 函数仅显示文件名（模式匹配）和字符串“non-existent”。
- 6. 一个环境（全局）变量被赋值并导出。
- 7. 一个数值表达式使用 UNIX/Linux date 命令的输出来获取当前小时。小时被赋给变量 Time。
- 8. 一个 Bash 数组 foods 被定义（declare -a），包含一个元素列表。
- 9. 一个整数 n 被定义，初始值为零。
- 10. 对于 guest 列表上的每个 person，除了用户 root，会创建一个邮件消息，邀请该人参加在给定地点和时间举行的聚会，并分配一份食物清单中的食物带去。
- 11. 如果 $person 的值为 root，控制会回到 for 循环顶部并从 guest 列表中的下一个 person 开始。
- 12. 邮件消息被发送。消息正文包含在一个 here 文档中。
- 13. 整数 n 增加 1。
- 14. 如果食物的数量等于数组索引中最后一个数字的值，列表为空。
- 15. 变量 n，将用作数组索引，被重置回零。
- 16. 这标志着循环语句的结束。



在上述，`command`被执行并评估其退出状态。如果为真（零），则执行`then`代码块（`then`和`else`之间的所有语句），并忽略`else`块。
如果退出状态为假（非零），则忽略`then`代码块，并执行`else`代码块（所有其他内容以及`fi`）。在任何情况下，只有一组命令会被执行：如果退出状态是执行的，则执行第一组；如果是非零，则执行第二组。

这可以用更简洁的方式表示：

```
if condition then statements-if-true else statements-if-false fi
```

让我们了解`on`的一个修改版本。如果请求的用户没有登录，我们不再让程序没有任何输出，而是让程序向用户报告这一事实。

这里是程序的第3版本：

```bash
$ cat on

#
# 确定是否有人登录 -- 版本3
#
user="$user"
if who | grep "$user" > /dev/null
then
    echo "$user is logged on"
else
    echo "$user is not logged on"
fi
$
```

如果作为`on`的第一个参数的用户已登录，则`grep`将成功并显示消息`user is logged on`；否则，将显示消息`user is not logged on`。

146 第7章 决策，决策

作为`on`的第一个参数的用户已登录，`grep`将成功并显示消息`user is logged on`；否则，将显示消息`user is not logged on`。

谁在登录？

```
$ who
root     tty1
barney   tty2
fred     tty3
joanne   tty4
root     tty5
tony     tty6
lulu     tty7
$ on     tty8
root     tty9
pat      tty10
tony     tty11
lulu     tty12
pat      tty13
root     tty14
tony     tty15
lulu     tty16
pat      tty17
root     tty18
tony     tty19
lulu     tty20
pat      tty21
root     tty22
tony     tty23
lulu     tty24
pat      tty25
root     tty26
tony     tty27
lulu     tty28
pat      tty29
root     tty30
tony     tty31
lulu     tty32
pat      tty33
root     tty34
tony     tty35
lulu     tty36
pat      tty37
root     tty38
tony     tty39
lulu     tty40
pat      tty41
root     tty42
tony     tty43
lulu     tty44
pat      tty45
root     tty46
tony     tty47
lulu     tty48
pat      tty49
root     tty50
tony     tty51
lulu     tty52
pat      tty53
root     tty54
tony     tty55
lulu     tty56
pat      tty57
root     tty58
tony     tty59
lulu     tty60
pat      tty61
root     tty62
tony     tty63
lulu     tty64
pat      tty65
root     tty66
tony     tty67
lulu     tty68
pat      tty69
root     tty70
tony     tty71
lulu     tty72
pat      tty73
root     tty74
tony     tty75
lulu     tty76
pat      tty77
root     tty78
tony     tty79
lulu     tty80
pat      tty81
root     tty82
tony     tty83
lulu     tty84
pat      tty85
root     tty86
tony     tty87
lulu     tty88
pat      tty89
root     tty90
tony     tty91
lulu     tty92
pat      tty93
root     tty94
tony     tty95
lulu     tty96
pat      tty97
root     tty98
tony     tty99
lulu     tty100
pat      tty101
root     tty102
tony     tty103
lulu     tty104
pat      tty105
root     tty106
tony     tty107
lulu     tty108
pat      tty109
root     tty110
tony     tty111
lulu     tty112
pat      tty113
root     tty114
tony     tty115
lulu     tty116
pat      tty117
root     tty118
tony     tty119
lulu     tty120
pat      tty121
root     tty122
tony     tty123
lulu     tty124
pat      tty125
root     tty126
tony     tty127
lulu     tty128
pat      tty129
root     tty130
tony     tty131
lulu     tty132
pat      tty133
root     tty134
tony     tty135
lulu     tty136
pat      tty137
root     tty138
tony     tty139
lulu     tty140
pat      tty141
root     tty142
tony     tty143
lulu     tty144
pat      tty145
root     tty146
tony     tty147
lulu     tty148
pat      tty149
root     tty150
tony     tty151
lulu     tty152
pat      tty153
root     tty154
tony     tty155
lulu     tty156
pat      tty157
root     tty158
tony     tty159
lulu     tty160
pat      tty161
root     tty162
tony     tty163
lulu     tty164
pat      tty165
root     tty166
tony     tty167
lulu     tty168
pat      tty169
root     tty170
tony     tty171
lulu     tty172
pat      tty173
root     tty174
tony     tty175
lulu     tty176
pat      tty177
root     tty178
tony     tty179
lulu     tty180
pat      tty181
root     tty182
tony     tty183
lulu     tty184
pat      tty185
root     tty186
tony     tty187
lulu     tty188
pat      tty189
root     tty190
tony     tty191
lulu     tty192
pat      tty193
root     tty194
tony     tty195
lulu     tty196
```

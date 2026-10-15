

% cat datafile
northwest NW Joel Craig 3.0 .98 3 4
western WE Sharon Kelly 5.3 .97 5 23
southwest SW Chris Foster 2.7 .8 2 18
southern SO May Chin 5.1 .95 4 15
southeast SE Derek Johnson 4.0 .7 4 17
eastern EA Susan Beal 4.4 .84 5 20
northeast NE TJ Nichols 5.1 .94 3 13
north NO Val Shultz 4.5 .89 5 9
central CT Sheri Watson 5.7 .94 5 13

## 6.12.6 范围运算符

### 示例 6.81

```
% awk '/\/western/,/\/eastern/' datafile
western WE Sharon Kelly 5.3 .97 5 23
southwest SW Chris Foster 2.7 .8 2 18
southern SO May Chin 5.1 .95 4 15
southeast SE Derek Johnson 4.0 .7 4 17
eastern EA Susan Beal 4.4 .84 5 20
```

### 解释

所有从以正则表达式 western 开始的范围内的记录都会被打印，直到找到以表达式 eastern 开始的记录为止。如果找到模式 western，记录将重新开始打印，并会一直打印到 eastern 或文件末尾。

## 6.12.7 条件运算符

### 示例 6.82

```
% awk '{print ($7 > 4 ? "high $7" : "low $7")} ' datafile
low 3
high 5
low 2
low 4
low 4
high 5
low 3
high 5
high 5
```

## LAB 4: awk 练习

（请参考 CD 上的名为 lab4.data 的数据库。）

```
Mike Harrington:(510) 548-1278:250:100:175
Christian Robbins:(408) 538-2358:155:90:201
Susan Dalass:(206) 654-279:250:60:50
Archie McNichol:(206) 548-1348:250:100:175
Jody Savage:(206) 548-1278:15:188:150
Guy Quigley:(916) 343-6410:250:100:175
Dan Savage:(406) 298-7744:450:300:275
Nancy McNeil:(206) 548-1278:250:80:75
John Goldenrod:(916) 348-4278:250:100:175
Chet Main:(510) 548-5258:50:95:135
Tom Savage:(408) 926-3456:250:168:200
Elizabeth Stachelin:(916) 440-1763:175:75:300
```

数据库包含姓名、电话号码以及过去三个月对党派竞选的资金捐助。

- 1. 打印第二个月捐助超过 $100 的人的名字和姓氏。
- 2. 打印上个月捐助少于 $85 的人的姓名和电话号码。
- 3. 打印第一个月捐助在 $75 到 $150 之间的人的姓名。
- 4. 打印三个月期间总捐助少于 $800 的人的姓名。
- 5. 打印月均捐助大于 $200 的人的姓名和地址。
- 6. 打印不在 916 区号中的人的名字。
- 7. 打印每个记录前面加上记录编号。
- 8. 打印每个人的姓名和总捐助额。
- 9. 为 Chet 的第二次捐助增加 $10。
- 10. 将 Nancy McNeil 的姓名更改为 Louise McInnes。

## 6.13 变量

### 6.13.1 数字和字符串常量

数字常量可以表示为整数，如 243；浮点数，如 3.14；或使用科学计数法的数字，如 .723E-1 或 3.4e7。字符串，如 Hello world，用双引号括起来。

初始化和类型强制转换。

在 awk 程序中仅提及一个变量就会使其存在。一个变量可以是字符串、数字或两者兼有。当它被设置时，它会变成等号右边表达式的类型。

未初始化的变量具有值零或值 ""，取决于它们被使用的上下文。

```
name = "Nancy"    name is a string
```

```
x++
    x is a number;
    x is initialized to zero and incremented by 1
```

```
number = 35    number is a number
```

要将字符串强制转换为数字：

```
name + 0
```

要将数字强制转换为字符串：

```
number ""
```

split 函数创建的所有字段和数组元素都被视为字符串，除非它们仅包含数值。如果字段或数组元素为空，则其字符串值为 null。空行也被视为 null 字符串。

### 6.13.2 用户定义变量

用户定义变量由字母、数字和下划线组成，且不能以数字开头。awk 中的变量不声明。awk 通过变量在表达式中的上下文推断数据类型。如果变量未初始化，awk 会将字符串变量初始化为空，数值变量初始化为零。如果需要，awk 会将字符串变量转换为数值变量，反之亦然。变量使用 awk 的赋值运算符赋值。请参阅表 6.11。

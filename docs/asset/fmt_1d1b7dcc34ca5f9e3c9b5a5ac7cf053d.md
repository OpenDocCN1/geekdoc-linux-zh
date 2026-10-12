
| `indexOf(character, from)` | 在字符串中搜索字符的第一次出现，返回其在字符串中的位置。你可以选择从哪里开始搜索。 |

| `italics()` | 将字符串文本更改为斜体。 |

| `lastIndexOf(character, from)` | 反向搜索字符串以找到字符的最后一次出现。 |

| `link(href)` | 将字符串转换为 HTML 链接标签，并将 `href` 作为锚点名称。 |

| `small()` | 将字符串文本更改为小字体。 |

| `split(sep)` | 通过在字符串 `sep` 每次出现的地方将字符串分成不同的部分，并返回一个数组。 |

| `strike()` | 将字符串文本更改为删除线字体。 |

| `sub()` | 将字符串文本更改为下标字体。 |

| `substring(start, finish)` | 返回从 `start` 开始到 `finish` 结束的子字符串。 |

| `sup()` | 将字符串文本更改为上标字体。 |

| `toLowerCase()` | 将字符串文本更改为小写。 |

| `toUpperCase()` | 将字符串文本更改为大写。 |

你如何使用这些方法？这里有一个练习可以展示给你。你将创建一个 JavaScript 函数，其中包含一些这些方法，并使用 `document.write()` 方法在网页上显示结果。

在你的文本编辑器中，创建一个 `SCRIPT` 元素来初始化一个新的字符串：

```
<SCRIPT TYPE="text/javascript" LANGUAGE="javascript1.3">
var s = new String("HTML Master the Essentials");
```

# 第二章

接下来，启动名为 `stringThings` 的函数，它接受一个名为 `stringName` 的参数。该参数将包含一个字符串：

```
function stringThings(stringName) {
```
最终，你将使用 `s` 作为参数调用 `stringThings`。

让函数的第一行使用 `document.write()` 来显示字符串：

```
document.write(stringName + "<BR>");
```

现在添加三行。第一行使字符串变为斜体，

```
document.write(stringName.italics() + "<BR>");
```

第二行使其变为粗体，

```
document.write(stringName.bold() + "<BR>");
```

第三行显示了你如何将方法组合在一起以产生一个复合结果：

```
document.write(stringName.bold().italics().fontsize(25) + "<BR>");
```

最后那一行使字符串变为粗体和斜体，并赋予它 25 点的字体大小。

现在让我们将字符串转换为数组。这一行在每个空格出现的地方拆分字符串，并将生成的段作为数组的项显示：

```
document.write(stringName.split(" ") + "<BR>");
```

这一行形成数组并对数组项进行排序：

```
document.write(stringName.split(" ") .sort() + "<BR>");
```

这一行形成数组并反转数组项的顺序：

```
document.write(stringName.split(" ") .reverse() + "<BR>");
```

最后，添加一行返回并显示子字符串。这个表达式将给你一个意想不到的结果，正如你将看到的那样：

```
document.write(stringName.substring(1,4) + "<BR>");
```

完成函数和脚本元素：

```
}
</SCRIPT>
```

添加此 HTML：

```
<TITLE>String Things</TITLE>
```

## 使用 JavaScript 49

```
</HEAD>
<BODY onload="stringThings(s)">
</BODY>
</HTML>
```

`<BODY>` 中的内联函数调用在页面打开时激活 `stringThings()`。它将 `s` 作为参数调用该函数，而 `s` 是新创建的字符串 "HTML Master the Essentials"。

列表 2.1 显示了整个 `stringThings.htm` 文件。

#### 列表 2.1：stringThings.htm

图 2.3 显示了 IE 中的页面。（在 Navigator 中看起来也一样。）

注意显示数组的几行。在每个数组中，项以逗号分隔的列表形式出现。最后一行显示了我提到的那个意想不到的结果。由于 `substring` 的参数被设置为 1 和 4，你可能会期望函数返回 HTML。相反，它返回的是 HTM。

# 50 第二章

![](img/6e99147f217994f89499215b2cff677f_77_0.png)

**图 2.3：** IE 中的 `stringThings.htm` 显示了应用 String 方法的结果。

> **注意**
>
> 如果你进入 `stringThings.htm` 文件并删除最后的 `document.write()`，你可以看到 IE 和 Navigator 之间一个古怪的微小差异。你可以在 IE 中重新打开页面看到所有的 `document.write()` 结果，或者可以在 Navigator 中重新打开页面，发现最后的 `document.write()` 没有出现。

### Math 对象

JavaScript `Math` 对象拥有你可以在其中构建到脚本中的方法。表 2.9 显示了这些方法。

#### 表 2.9：Math 对象的方法

| 方法 | 返回... |
| --- | --- |
| `abs()` | 数字的绝对值 |
| `acos()` | 数字以弧度为单位的余弦值 |
| `asin()` | 数字以弧度为单位的正弦值 |

#### 表 2.9 继续：Math 对象的方法

| 方法 | 返回... |
| --- | --- |
| `atan()` | 数字以弧度为单位的正切值 |
| `ceil()` | 给定数字的所有小数部分，如果小数部分大于0则加1。也就是说， `ceil(0) = 0`，而 `ceil(1) = 1`。 |
| `cos()` | 数字的余弦值 |
| `exp()` | e 的指定幂 |
| `floor()` | 给定数字的所有小数部分。 |
| `log()` | 数字的自然对数 |
| `max()` | 两个数中较大的一个 |
| `min()` | 两个数中较小的一个 |
| `pow()` | 基数的指定幂的值 |
| `random()` | 0 到 1 之间的伪随机数 |
| `round()` | 舍入到最近整数的数字。 |
| `sin()` | 数字的正弦值 |
| `sqrt()` | 数字的平方根 |

这里是一些使用这些方法的示例：

```
var x, y, z;
y = Math.sqrt(x);
z = Math.pow(x,y);
```

#### 表 2.10：Math 对象的属性

| 属性 | 意义 | 近似值 |
| --- | --- | --- |
| `E` | 自然对数的底 | 2.718 |
| `LN2` | 2 的自然对数 | 0.693 |
| `LN10` | 10 的自然对数 | 2.302 |

#### 表 2.10 继续：Math 对象的属性

| 属性 | 意义 | 近似值 |
| --- | --- | --- |
| `LOG2E` | 以 2 为底的 e 的对数 | 1.442 |
| `LOG10E` | 以 2 为底的 10 的对数 | 0.434 |
| `PI` | 圆周与直径的比 | 3.1416 |
| `SQRT1` | .5 的平方根 | 0.707 |
| `SQRT2` | 2 的平方根 | 1.414 |

### Date 对象

JavaScript `Date` 对象提供了处理时间和日期的功能。表 2.11 显示了它的方法。

#### 表 2.11：Date 对象的方法

| 方法 | 功能 |
| --- | --- |
| `getDate()` | 返回 `Date` 对象中的月份几号 |
| `getDay()` | 返回星期几 |
| `getHours()` | 返回小时 |
| `getMinutes()` | 返回分钟 |
| `getMonth()` | 返回月份 |
| `getSeconds()` | 返回秒 |
| `getTime()` | 返回完整时间 |
| `getTimeZoneOffset()` | 返回格林威治标准时间与运行脚本的计算机时区之间的小时差 |
| `getYear()` | 返回年份 |
| `parse()` | 返回日期与 1970 年1 月 1 日之间的毫秒数 |
| `getDate()` | 设置 `Date` 对象的月份几号 |
| `setHours()` | 设置小时 |

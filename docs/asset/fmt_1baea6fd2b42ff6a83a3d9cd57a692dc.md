
# 77. `var myString` 相关题目

`var myString = "I am here?";`

`var whereAreYou = myString.indexOf("am");`

`whereAreYou` 的值是多少？

+ A. 0
+ B. 1
+ C. 2
+ D. 3

## 78. 关于 `animate(params, duration, easing, function)`，何时执行回调函数？

+ A. 动画完成时。
+ B. 动画完成前一秒。
+ C. 动画完成后一秒。
+ D. 调度执行回调函数。

## 79. `fadeTo(2000, 0.333)` 的意思是？

+ A. 将元素的宽度设为 `2000`，高度为 `0.333`。
+ B. 将元素的颜色设为 `2000`，背景颜色为 `0.333`。
+ C. 将元素的页面大小设为 `2000`，字体大小为 `0.333`。
+ D. 将元素的持续时间设为 `2000` 毫秒，透明度为 `0.333`。

## 80. 下面哪个方法会停止动画？

+ A. `close()`
+ B. `end()`
+ C. `stop()`
+ D. `shut()`

## 81. `timestamp` 属性意味着从事件触发开始的毫秒数。

+ A. 1960年1月1日。
+ B. 1970年1月1日。
+ C. 1980年1月1日。
+ D. 1990年1月1日。

## 82. `math.ceil(7.5)` & `math.floor(7.5)` 的结果是什么？

+ A. 8 7
+ B. 7 7
+ C. 8 8
+ D. 7 8

## 83. `math.ceil(-7.5)` & `math.floor(-7.5)` 的结果是什么？

+ A. -7 -8
+ B. -7 -7
+ C. -8 -8
+ D. -8 -7

## 84. 想要知道哪个元素包含了发布事件的元素，使用 `___`？

+ A. `event.issue`
+ B. `event.element`
+ C. `event.target`
+ D. `event.type`

## 85. `preventDefault()` 用于什么？

+ A. 防止默认元素被选中。
+ B. 防止事件发生默认行为。
+ C. 防止默认选择器被错误地使用。
+ D. 防止默认函数被调用。

## 86. 下列哪一个不是 `jQuery` 中的事件对象属性？

+ A. `event.data`
+ B. `event.keyCode`
+ C. `event.type`
+ D. `event.response`

## 87. 哪个方法可以设置或获取指定元素的值？

+ A. `value()`
+ B. `set()` or `get()`
+ C. `setValue()` or `getValue()`
+ D. `val()`

## 88. 当用户将光标移动到网页上的某个元素时，会发生 `____` 事件。

+ A. `blur`
+ B. `focus`
+ C. `moves`
+ D. `enter`

## 99. 当表单元素的内容、选择或勾选状态发生改变时，会发生 `____` 事件。

+ A. `modify`
+ B. `transform`
+ C. `change`
+ D. `vary`

## 90. `math.round(7.5)`, `math.round(-7.5)` 的结果是？

+ A. 8 -8
+ B. 8 -7

## 91. 下列哪个语句会将所有 `<input>` 元素的 `checked` 值设为 `true`？

+ A. `$("input").set("checked", true);`
+ B. `$("input").setProperty("checked", true);`
+ C. `$("input").property("checked", true);`
+ D. `$("input").prop("checked", true);`

## 92. 下列哪个语句可以从 `<span>` 元素中移除类？

+ A. `$("span").removeClass("class-name");`
+ B. `$("span").eraseClass("class-name");`
+ C. `$("span").deleteClass("class-name");`
+ D. `$("span").cancelClass("class-name");`

## 93. 下列哪个语句是正确的？

+ A. `$("p").insertBefore("<span>Hello world!</span>");` `$("p").insertAfter("<span>Hello world!</span>");`
+ B. ` $("<span>Hello world!</span>").insertBefore("p");` `$("span>Hello world!</span>").insertAfter("p");`
+ C. `$("p").insertBefore("<span>Hello world!</span>");` `$("span>Hello world!</span>").insertAfter("p");`
+ D. ` $("<span>Hello world!</span>").insertBefore("p");` `$("span>Hello world!</span>").insertAfter("p");`

## 94. `AJAX` 的缩写代表 `___`？

+ A. `Asynchronous JavaScript And XHTML`
+ B. `Asynchronous Java And XHTML`
+ C. `Asynchronous JavaScript And XML`
+ D. `Asynchronous JQuery And XML`

## 95. 在 `JavaScript` 中，你必须创建一个 `___` 对象，它是浏览器中进行 `Ajax` 工作的基础。

+ A. `ajax object`
+ B. `javaScript object`
+ C. `XMLHttpRequest object`
+ D. `activeXObject object`

## 96. `Ajax` 以 `___` 方式与服务器进行数据通信？

+ A. 同步
+ B. 异步
+ C. 同时
+ D. 持续

## 97. 关于 `load(url, data, function)`，哪个参数是**不是**正确的？

+ A. `url` 指定了想要加载的文件的 `URL`
+ B. `data` 指定了一组从 `url` 获取的属性/值对，随请求发送到服务器。
+ C. `function` 指定了在 `load()` 方法完成后执行的函数。
+ D. `function` 指定了在 `load()` 方法完成之前执行的函数。

## 98. 关于 `load(url, data, function)`，哪个语句是**不是**正确的？

+ A. 如果 `load()` 包含“`data`”参数，则使用 `POST` 方法。
+ B. 如果 `load()` 不包含“`data`”参数，则使用 `GET` 方法。
+ C. “`data`”参数的作用方式如下：`{property=value}`
+ D. “`data`”参数的作用方式如下：`myString="hello"`

## 99. 关于 `$.ajax()`,哪个格式是正确的？

+ A. `$.ajax({ type: "GET/POST", url: "txt/php/asp/jsp file", data: {key: value}, sccess: function, });`
+ B. `$.ajax({ //javascript code });`
+ C. `$.ajax({ //php code });`
+ D. `$.ajax({ //asp code });`

## 100. 关于 `$.ajax()`，哪个参数不是正确的？

+ A. “`type`”将请求类型设置为 `POST` 或 `GET`。
+ B. “`url`”设置要请求的 `URL`。
+ C. “`timeout`”设置请求的超时时间（秒）。
+ D. “`success`”设置在请求成功时调用的函数。

# 100 道 JQuery 答案

| 1. D | 26. A | 51. B | 76. C |
|---|---|---|---|
| 2. D | 27. D | 52. C | 77. C |
| 3. C | 28. B | 53. D | 78. A |
| 4. B | 29. A | 54. C | 79. D |
| 5. D | 30. C | 55. B | 80. C |
| 6. A | 31. B | 56. A | 81. B |
| 7. C | 32. A | 57. D | 82. D |
| 8. D | 33. B | 58. D | 83. A |
| 9. C | 34. D | 59. B | 84. C |
| 10. B | 35. C | 60. C | 85. B |
| 11. C | 36. D | 61. B | 86. D |
| 12. A | 37. A | 62. A | 87. D |
| 13. C | 38. B | 63. C | 88. B |
| 14. B | 39. C | 64. D | 89. C |
| 15. D | 40. D | 65. C | 90. B |
| 16. D | 41. B | 66. A | 91. D |
| 17. A | 42. C | 67. D | 92. A |
| 18. B | 43. A | 68. D | 93. D |
| 19. D | 44. A | 69. C | 94. C |
| 20. A | 45. D | 70. D | 95. C |
| 21. D | 46. C | 71. B | 96. B |
| 22. C | 47. B | 72. A | 97. D |
| 23. B | 48. D | 73. C | 98. D |
| 24. C | 49. A | 74. D | 99. A |
| 25. C | 50. D | 75. B | 100. C |

# JavaScript 100 道题与答案

## 100 道 JavaScript

请选择正确答案。

### 1. 哪个标签是用于 `JavaScript` 的？

+ A. `<?>`
+ B. `<JavaScript>...</>`
+ C. `<script Language="JavaScript">...</script>`
+ D. `<script type="text/JavaScript">...</script>`

### 2. 关于 `JavaScript` 注释，哪个是正确的？

+ A. `//` 用于多行注释
+ B. `/* */` 用于单行注释
+ C. `//` 和 `/* */` 可用于单行或多行注释。
+ D. `//` 用于单行注释且 `/* */` 用于多行注释。

### 3. 下列哪个表达式是不正确的？

+ A. `a += b` 表示 `a = (a + b)`
+ B. `a != b` 表示 `a = (! b)`
+ C. `a *= b` 表示 `a = (* b)`
+ D. `a %= b` 表示 `a = (% b)`

### 4. 哪个变量名是无效的？

+ A. `10var`
+ B. `varName`
+ C. `my_var`
+ D. `var10`

### 5. 哪个运算符描述是不正确的？

+ A. `+` 用于加法
+ B. `–` 用于减法
+ C. `*` 用于乘法
+ D. `%` 用于除法

### 6. 下列哪个命令不是在 `JavaScript` 中显示文本的？

+ A. `alert()`
+ B. `document.write()`
+ C. `console.log()`
+ D. `document.getElementById().innerHTML`

### 7. 哪个可以作为变量名？

+ A. `nonVir`
+ B. `var`
+ C. `float`
+ D. `try`

### 8. 下列哪个数据类型描述**不是**正确的？

+ A. “`boolean`”返回 `true` 或 `false`。
+ B. “`integer`”是一个整数。
+ C. “`string`”是字符字符串的字符。
+ D. “`number`”是一个整数或浮点数。

### 9. 下列哪个转义序列描述是**不是**正确的？

+ A. “`b`” 用于“`backslash`”。
+ B. “`n`” 用于“`newline`”
+ C. “`r`” 用于“`return`”
+ D. “`t`” 用于“`tap`”。

### 10. 下列代码中哪一行是**不是**正确的？

```
function firstFunction() {

var num = 100; // line 1

secondFunction(); // line 2

}

function secondFunction() { // line 3

document.write( num ); //line4

}

firstFunction();
```

+ A. `line1`
+ B. `line2`
+ C. `line3`
+ D. `line4`

### 11. 哪个命令是正确的？

+ A. `if () { } else { }`
+ B. `if () then { } else { }`
+ C. `if () then { } else { }`
+ D. `if () then { } else { }`

### 12. 下列哪个**不是** `JS` 中的比较运算符？

+ A. `==`
+ B. `<=`
+ C. `!=`
+ D. `=>`

### 13. 下列哪个**不是** `JS` 中的逻辑运算符？

+ A. `$`
+ B. `&&`
+ C. `||`
+ D. `!`

### 14. 下列代码中哪一行是不正确的？

```
var a = 10; // line 1
var b = 3; // line 2
var num = (a % b == 0) ? "EVEN" : "ODD"; // line 3
alert ( num ); // line 4
```

+ A. `line1`
+ B. `line2`
+ C. `line3`
+ D. `line4`

### 15. 下列中哪行是不正确的？

```
var name = null; // line1
name = prompt("Please Input Your Name", " "); // line2
if ( name=="") // line3
document.write("Hello" + name ); //line4
```

+ A. `line1`
+ B. `line2`
+ C. `line3`
+ D. `line4`

### 16. 下列代码的输出是什么？

```
var num = 2;
switch (num){
case 1: document.write("A");
case 2: document.write("B");
case 3: document.write("C");
default: document.write("D");
}
```

+ A. `A`
+ B. `B`
+ C. `BC`
+ D. `BCD`

### 17. 下列代码的输出是什么？

```
var teststring = ("JavaScript " == "Javascript");
alert(teststring);
```

+ A. `true`
+ B. `false`
+ C. `1`
+ D. `-1`

### 18. 下列代码的结果是？

```
var x = 0, y = 50;
while ( x < 10) {
y--;
x++; }
```

```javascript
alert ("x is: " + x + " and y is: " + y);
```

+ A. `x is 10 and y is 40`
+ B. `x is 11 and y is 41`
+ C. `x is 12 and y is 42`
+ D. `x is 13 and y is 43`

### 19. 下列代码的输出是什么？

```javascript
var x = 0, y = 50;

do {

  y--;

  x++;

} while (x < 10)

alert ("x is: " + x + " and y is: " + y);
```

+ A. `x is 13 and y is 43`
+ B. `x is 12 and y is 42`
+ C. `x is 11 and y is 41`
+ D. `x is 10 and y is 40`

### 20. 以下代码的输出是什么？

```javascript
for (var num = 1; num < 10; num++) {

  document.write ( num + " ");

  if (num % 5 == 0)

    break;

}
```

+ A. `1 2`
+ B. `1 2 3`
+ C. `1 2 3 4`
+ D. `1 2 3 4 5`

### 21. （题目编号缺失，根据上下文推断为第21题关于循环输出）

+ A. `1 2 3 4 5`
+ B. `1 2 3 4 6`
+ C. `1 2 3 4 7`
+ D. `1 2 3 4 8`

### 22. 创建数组时哪个是正确的？

```
var a = new Array {"A", "B", "C" };
var a = new Array ("A", "B", "C");
var a = new Array ["A", "B", "C"];
var a = new Array <"A", "B", "C" >;
```

### 23. 下列代码中哪行**不**正确？

```javascript
var a = new Array(); // line1

a[0] = "A"; // line2

a[1] = "B";

var arraySize = a.length(); // line3

alert ( arraySize ); //line4
```

+ A. `line1`
+ B. `line2`
+ C. `line3`
+ D. `line4`

### 24. 下列代码中哪行**不**正确？

```javascript
var a = new Array( 1, 2, 3 ); // line 1

alert(a[1]); // line 2

alert(a[2]); // line 3

alert(a[3]); // line 4
```

+ A. `line1`
+ B. `line2`
+ C. `line3`
+ D. `line4`

### 25. 下列代码的输出是什么？

```javascript
var a = new Array( );

a[0] = "A"; a[1] = "B"; a[2] = "C"; alert (a.join(" - "));
```

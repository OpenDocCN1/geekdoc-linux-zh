
`objectName.propertyName`

例如，当前网页文档的背景颜色是由预定义对象的`bgColor`属性标识的。要将背景颜色更改为白色，可以使用以下 JavaScript 语句：

```
document.bgColor="white"
```

该语句将字符串 `"white"` 分配给预定义对象的`bgColor`属性。列表 4.1 显示了你如何在示例脚本中使用此语句。图 4.1 显示了网页脚本产生的结果。显示了几个带有不同颜色名称的按钮。当你点击按钮时，按钮的`onClick`事件处理器通过设置`document.bgColor`属性来更改文档的背景。

### 列表 4.1：使用 JavaScript 属性

```html
<HTML>
<HEAD>
<TITLE>Using Properties</TITLE></HEAD>
<body>
<h1>Using Properties</h1>
<FORM>
<P><INPUT TYPE="BUTTON" NAME="red" VALUE="Red" CLICK="document.bgColor='red'"></P>
<P><INPUT TYPE="BUTTON" NAME="white" VALUE="White" CLICK="document.bgColor='white'"></P>
<P><INPUT TYPE="BUTTON" NAME="blue" VALUE="Blue" CLICK="document.bgColor='blue'"></P>
</FORM>
</body>
</HTML>
```

# 对象操作 101

![](img/6e99147f217994f89499215b2cff677f_128_0.png)

图 4.1：使用属性更改背景颜色（列表 4.1）

### 使用方法

你访问对象的方法的方式与其属性相同：

```
objectName.methodName(parameterList)
```

参数（如果有的话）用逗号分隔。即使没有指定参数也必须使用括号。以下是方法调用的示例：

```
r=Math.random()
```

调用了`Math`对象的`random()`方法。该方法返回 0 到 1 之间的随机浮点数。该数被赋值给`r`。

从第 3 章“添加 JavaScript”开始，你一直在使用预定义对象的方法。你使用了`document`对象的`write()`方法向文档写入 HTML 实体。你还使用了`window`对象的`alert()`方法显示弹出对话框。在下一节中，你将介绍由 JavaScript 浏览器自动创建的对象。在本章后面，将以总结的形式介绍预定义对象。

### 创建对象实例

你使用`new`运算符创建特定类型对象的实例。你之前使用过`new`运算符创建数组对象。创建其他类型的对象使用相同的语法：

```
variable = new Type(parameters)
```

上述语句中的`Type(parameters)`部分被称为构造函数。某些对象类型有多个构造函数。构造函数的区别在于它们允许的参数数量。

例如，`Date`是一个预定义对象类型。要创建一个具有当前日期时间的`Date`实例并赋值给变量`currentDate`，使用以下语句：

```
currentDate = new Date()
```

在该语句中，`Date()`构造函数不接受参数。`Date`对象类型还允许为指定的日期创建对象实例。例如，以下语句为 2005 年 1 月 1 日创建一个`Date`实例：

```
currentDate = new Date(2005, 0, 1)
```

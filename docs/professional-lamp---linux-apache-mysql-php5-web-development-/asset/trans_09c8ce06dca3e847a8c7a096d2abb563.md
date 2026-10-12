
## 附录 A

### 循环：Do...While

**PHP**

```php
do {  ...  } while (expr);
```

**ASP/VBScript**

```vbs
Do  ...  Loop Until expr
```

**ASP.NET/C#**

```csharp
do {  ...  }  while (expr);
```

**JSP/Java**

```java
do {  ...  } while (expr);
```

### 循环：For

**PHP**

```php
for (expr1; expr2; expr3) {  ...  }
```

**ASP/VBScript**

```vbs
For expr1 To expr2 Step expr3  ...  Next
```

**ASP.NET/C#**

```csharp
for (expr1; expr2; expr3) {  ...  }
```

**JSP/Java**

```java
for (expr1; expr2; expr3) {  ...  }
```

### 循环：For Each

**PHP**

```php
foreach (array as $item) {
...
}

foreach (array as $key => $item) {
...
}
```

**ASP/VBScript**

```vbs
For Each *item* In array
...
Next
```

**ASP.NET/C#**

```csharp
for (type *item* in array) {
...
}
```

**JSP/Java**

```java
for (Iterator *item*; *item*.hasNext(); ) {
...
}
```

### 循环：终止

**PHP**

```php
break;
```

**ASP/VBScript**

```vbs
Exit Do
Exit For
```

（无法退出 While 循环。）

**ASP.NET/C#**

```csharp
break;
```

**JSP/Java**

```java
break;
```

### 循环：进入下一轮

**PHP**

```php
continue;
```

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
continue;
```

**JSP/Java**

```java
continue;
```

### 函数/方法声明

**PHP**

```php
function name (args) { ... }
```

**ASP/VBScript**

```vbs
Function name (args) ... End Function

Sub name (args) ... End Sub
```

**ASP.NET/C#**

```csharp
visibility returnType name (args) { ... }
```

**JSP/Java**

```java
visibility returnType name (args) { ... }
```

### 返回函数值

**PHP**

```php
return value;
```

**ASP/VBScript**

```vbs
FunctionName = value
```

**ASP.NET/C#**

```csharp
return value;
```

**JSP/Java**

```java
return value;
```

### 使用命名空间对类进行分组

**PHP**

不支持

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
namespace Name {
...
}
```

**JSP/Java**

```java
package name;
```

### 类可见性关键字

| 语言         | 关键字                                      |
| :------------- | :-------------------------------------------- |
| PHP            | public, private, protected                    |
| ASP/VBScript   | public, private                               |
| ASP.NET/C#     | public, private, protected, internal          |
| JSP/Java       | public, private, protected, package           |

### 基类定义

**PHP**

```php
class ClassName { 
...
} 
```

**ASP/VBScript**

```vbs
Class ClassName
...
End Class 
```

**ASP.NET/C#**

```csharp
visibility class ClassName {
...
} 
```

**JSP/Java**

```java
visibility class ClassName {
...
}
```

### 声明类属性

**PHP**

```php
visibility name; 
```

**ASP/VBScript**

```vbs
visibility name 
```

**ASP.NET/C#**

```csharp
visibility type name; 
```

**JSP/Java**

```java
visibility type name; 
```

### 调用同一类中的方法

**PHP**

```php
$this->method(); 
```

**ASP/VBScript**

```vbs
Me.method 
```

**ASP.NET/C#**

```csharp
this.method();
```

**JSP/Java**

```java
this.method();
```

### 类构造器

**PHP**

```php
function __construct() { … }
```

**ASP/VBScript**

```vbs
Private Sub Class_Initialize( ) … End Sub
```

**ASP.NET/C#**

```csharp
visibility ClassName( ) { … }
```

**JSP/Java**

```java
public ClassName( ) { … }
```

### 类析构器

**PHP**

```php
function __destruct() { … }
```

**ASP/VBScript**

```vbs
Private Sub Class_Terminate( ) … End Sub
```

**ASP.NET/C#**

```csharp
visibility ~ClassName( ) { … }
```

**JSP/Java**

```java
protected void finalize() {
    ...
}
```

### 使用静态类方法

**PHP**

```php
ClassName::StaticMethod();
```

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
ClassName.StaticMethod();
```

**JSP/Java**

```java
ClassName.StaticMethod();
```

### 创建对象

**PHP**

```php
$obj = new ClassName();
```

**ASP/VBScript**

```vbs
Set obj = New ClassName
```

**ASP.NET/C#**

```csharp
type obj = new ClassName();
```

**JSP/Java**

```java
type obj = new ClassName();
```

### 类继承

**PHP**

```php
class ClassName extends BaseClass {
    ...
}
```

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
visibility class ClassName : BaseClass {
... 
}
```

**JSP/Java**

```java
visibility class ClassName extends BaseClass {
... 
}
```

### 调用父类方法

**PHP**

```php
parent::method();
```

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
base.method();
```

**JSP/Java**

```java
super.method();
```

### 声明抽象类

**PHP**

```php
abstract class AbstractClass {
... 
}
```

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
abstract class AbstractClass {
... 
}
```

**JSP/Java**

```java
visibility abstract class AbstractClass {
...
}
```

### 停止子类化

**PHP**

```php
final class EndClass {
...
}
final visibility function MethodName() {
...
}
```

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
sealed class EndClass {
...
}
sealed visibility type MethodName() {
...
}
```

**JSP/Java**

```java
visibility final class EndClass {
...
}
visibility final type MethodName () {
...
}
```

### 接口声明

**PHP**

```php
interface InterfaceName {
...
}
```

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
visibility interface InterfaceName {
...
}
```

**JSP/Java**

```java
visibility interface InterfaceName {
}
```

### 类使用接口

**PHP**

```php
class ClassName implements InterfaceName {
...
}
```

**ASP/VBScript**

不支持

**ASP.NET/C#**

```csharp
visibility class ClassName : InterfaceName {
...
}
```

**JSP/Java**

```java
visibility class ClassName implements InterfaceName {
...
}
```

### 包含外部文件

**PHP**

```php
include('filename');
include_once('filename');
require('filename');
require_once('filename');
```

**ASP/VBScript**

```vbs
<%-- #include 'filename' -->
```

**ASP.NET/C#**

包含处理通过多种方法进行，包括传统的 ASP 包含方式（如上所示）

**JSP/Java**

```jsp
<%@ include file="filename" %>
```

### 异常处理

**PHP**

```php
try {
    ...
} catch (ExceptionType $e) {
    ...
}
```

**ASP/VBScript**

未具体支持

**ASP.NET/C#**

```csharp
try {
    ...
} catch (ExceptionType e) {
    ...
} finally {
    ...
}
```

**JSP/Java**

```java
try {
    ...
} catch (ExceptionType e) {
    ...
} finally {
    ...
}
```

### 抛出异常

**PHP**

```php
throw new ExceptionType(args);
```

**ASP/VBScript**

```vbs
Err.Raise number
```

**ASP.NET/C#**

```csharp
throw new ExceptionType(args);
```

**JSP/Java**

```java
throw new ExceptionType(args);
```

### HTTP POST 值

**PHP**

`$_POST` (数组)

**ASP/VBScript**

`Request.Form` (集合)

**ASP.NET/C#**

`System.Web.HttpRequest.Form` (NameValueCollection)

**JSP/Java**

`request.getParameter()` (方法查找)

### HTTP GET 值

**PHP**

`$_GET` (数组)

**ASP/VBScript**

`Request.QueryString` (集合)

**ASP.NET/C#**

`System.Web.HttpRequest.QueryString` (NameValueCollection)

**JSP/Java**

`request.getParameter()` (方法查找)

### 服务器变量

**PHP**

`$_SERVER` (数组)

**ASP/VBScript**

`Request.ServerVariables` (集合)

**ASP.NET/C#**

`System.Web.HttpRequest.ServerVariables` (NameValueCollection)

**JSP/Java**

`request .getVariable()` (方法查找；每个服务器变量对应不同的方法)

![](img/cacdd24f2926f10ee3219256ad732604_372_0.png)

## 附录 B

### 替代工具

每当讨论流行的 PHP 工具时，对话通常都集中在文本编辑器或代码集成开发环境（IDE）上。哪一款具有最好的语言支持、语法高亮、代码解析等功能？不幸的是，由于过分关注文本编辑器，一些优秀的非编码工具有时会被忽视。与其重述支持某一款编辑器而非另一款编辑器的常规论点，本附录将向您展示一些在开发周期中可以使用的工具——那些不会立即生成代码，但可能在整体开发流程中占据关键位置的工具。

### MySQL 工具

在管理 MySQL 数据库时，通常有两个主要的管理工具选项：标准的命令行工具集或图形化界面。尽管许多经验丰富的系统管理员对此持保留态度，但使用图形化工具完成工作完全没有问题。虽然命令行界面提供了对数据库的无限控制权，但它无法匹敌良好的图形用户界面在促进管理工作流程方面的速度和清晰度。

如果您正在寻找一套优秀的基于 GUI 的 MySQL 管理工具，MySQL AB 自家的 MySQL Administrator 和 MySQL Query Browser 便是最佳选择。

### MySQL Administrator

MySQL Administrator 是一个功能丰富的 GUI 管理工具，用于维护 MySQL 数据库。主要界面如图 B.1 所示。


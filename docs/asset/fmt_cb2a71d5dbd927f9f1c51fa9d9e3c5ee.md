
## 返回函数值

**PHP**
```php
return value;
```

**ASP/VBScript**
```vb
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

## 使用命名空间分组类

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

## 类可见性关键字

**PHP**
`public`, `private`, `protected`

**ASP/VBScript**
`public`, `private`

**ASP.NET/C#**
`public`, `private`, `protected`, `internal`

**JSP/Java**
`public`, `private`, `protected`, `package`

## 基类定义

**PHP**
```php
class ClassName {
...
}
```

**ASP/VBScript**
```vb
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

## 声明类属性

**PHP**
```php
visibility name;
```

**ASP/VBScript**
```vb
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

## 调用同一类中的方法

**PHP**
```php
$this->method();
```

**ASP/VBScript**
```vb
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

## 类构造器

**PHP**
```php
function __construct() {
...
}
```

**ASP/VBScript**
```vb
Private Sub Class_Initialize()
...
End Sub
```

**ASP.NET/C#**
```csharp
visibility ClassName() {
...
}
```

**JSP/Java**
```java
public ClassName() {
...
}
```

## 类析构器

**PHP**
```php
function __destruct() {
...
}
```

**ASP/VBScript**
```vb
Private Sub Class_Terminate()
...
End Sub
```

**ASP.NET/C#**
```csharp
visibility ~ClassName() {
...
}
```

**JSP/Java**
```java
protected void finalize() { ... }
```

## 使用静态类方法

**PHP**
```php
ClassName :: StaticMethod();
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

## 创建对象

**PHP**
```php
$obj = new ClassName();
```

**ASP/VBScript**
```vb
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

## 类继承

**PHP**
```php
class ClassName extends BaseClass { ... }
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

## 调用父类方法

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

## 声明抽象类

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

## 停止子类化

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

## 接口声明

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
...
}
```

## 类使用接口

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

## 包含外部文件

**PHP**
```php
include('filename');
include_once('filename');
require('filename');
require_once('filename');
```

**ASP/VBScript**
```html
<!-- #include 'filename' -->
```

**ASP.NET/C#**
包含由不同方法处理，包括传统的 ASP 包含方式（如上）。

**JSP/Java**
```jsp
```


## Appendix A

### Language Translation

#### Switch Statement

**ASP.NET/C#**
```csharp
switch (expr) {
  case value1:
    ...
    break;
  case value2:
    ...
    break;
  default:
    ...
    break;
}
```

**JSP/Java**
```java
switch (expr) {
  case value1:
    ...
    break;
  case value2:
    ...
    break;
  default:
    ...
    break;
}
```

### Loop: While

**PHP**
```php
while (expr) {
  ...
}
```

**ASP/VBScript**
```vb
While expr
  ...
Wend
```

**ASP.NET/C#**
```csharp
while (expr) {
  ...
}
```

**JSP/Java**
```java
while (expr) {
  ...
}
```

### Loop: Do... While

**PHP**
```php
do { ... } while (expr);
```

**ASP/VBScript**
```vb
Do ... Loop Until expr
```

**ASP.NET/C#**
```csharp
do { ... } while (expr);
```

**JSP/Java**
```java
do { ... } while (expr);
```

### Loop: For

**PHP**
```php
for (expr1; expr2; expr3) { ... }
```

**ASP/VBScript**
```vb
For expr1 To expr2 Step expr3 ... Next
```

**ASP.NET/C#**
```csharp
for (expr1; expr2; expr3) { ... }
```

**JSP/Java**
```java
for (expr1; expr2; expr3) { ... }
```

### Loop: For Each

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
```vb
For Each item In array
...
Next
```

**ASP.NET/C#**
```csharp
for (type item in array) {
...
}
```

**JSP/Java**
```java
for (Iterator item; item.hasNext(); ) {
...
}
```

### Loop: Termination

**PHP**
```php
break;
```

**ASP/VBScript**
```vb
Exit Do
Exit For
```
*(There is no exiting a While loop.)*

**ASP.NET/C#**
```csharp
break;
```

**JSP/Java**
```java
break;
```

### Loop: Advance to Next Round

**PHP**
```php
continue;
```

**ASP/VBScript**
Not supported

**ASP.NET/C#**
```csharp
continue;
```

**JSP/Java**
```java
continue;
```

### Function/Method Declaration

**PHP**
```php
function name (args) {
  ...
}
```

**ASP/VBScript**
```vb
Function name (args)
  ...
End Function

Sub name (args)
  ...
End Sub
```

**ASP.NET/C#**
```csharp
visibility returnType name (args) {
  ...
}
```

**JSP/Java**
```java
visibility returnType name (args) {
  ...
}
```

### Returning Function Values

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

### Grouping Classes with Namespaces

**PHP**
Not supported

**ASP/VBScript**
Not supported

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

### Class Visibility Keywords

**PHP**
public, private, protected

**ASP/VBScript**
public, private

**ASP.NET/C#**
public, private, protected, internal

**JSP/Java**
public, private, protected, package

### Base Class Definition

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

### Declaring Class Properties

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

### Calling a Method in Same Class

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

### Class Constructor

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

### Class Destructor

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

### Using Static Class Methods

**PHP**
```php
ClassName :: StaticMethod();
```

**ASP/VBScript**
Not supported

**ASP.NET/C#**
```csharp
ClassName.StaticMethod();
```

**JSP/Java**
```java
ClassName.StaticMethod();
```

### Creating an Object

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

### Class Inheritance

**PHP**
```php
class ClassName extends BaseClass { ... }
```

**ASP/VBScript**
Not supported

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

### Calling a Parent Method

**PHP**
```php
parent::method();
```

**ASP/VBScript**
Not supported

**ASP.NET/C#**
```csharp
base.method();
```

**JSP/Java**
```java
super.method();
```

### Declaring Abstract Classes

**PHP**
```php
abstract class AbstractClass {
...
}
```

**ASP/VBScript**
Not supported

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

### Stopping Subclassing

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
Not supported

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

### Interface Declaration

**PHP**
```php
interface InterfaceName {
...
}
```

**ASP/VBScript**
Not supported

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

### Class Using Interface

**PHP**
```php
class ClassName implements InterfaceName {
...
}
```

**ASP/VBScript**
Not supported

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

### Including External Files

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
Inclusion handled by varying methods, including traditional ASP inclusion (above).

**JSP/Java**
```jsp
<%@ include file="filename" %>
```

### Exception Handling

**PHP**
```php
try { ... } catch (ExceptionType $e) { ... }
```

**ASP/VBScript**
Not specifically supported

**ASP.NET/C#**
```csharp
try { ... } catch (ExceptionType e) { ... } finally { ... }
```

**JSP/Java**
```java
try { ... } catch (ExceptionType e) { ... } finally { ... }
```

### Throwing Exceptions

**PHP**
```php
throw new ExceptionType(args);
```

**ASP/VBScript**
```vb
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

### HTTP POST Values

**PHP**
```php
$_POST (array)
```

**ASP/VBScript**
```vb
Request.Form (collection)
```

**ASP.NET/C#**
```csharp
System.Web.HttpRequest.Form (NameValueCollection)
```

**JSP/Java**
```java
request.getParameter() (method lookup)
```

### HTTP GET Values

**PHP**
```php
$_GET (array)
```

**ASP/VBScript**
```vb
Request.QueryString (collection)
```

**ASP.NET/C#**
```csharp
System.Web.HttpRequest.QueryString (NameValueCollection)
```

**JSP/Java**
```java
request.getParameter() (method lookup)
```

### Server Variables

**PHP**
```php
$_SERVER (array)
```

**ASP/VBScript**
```vb
Request.ServerVariables (collection)
```

**ASP.NET/C#**
```csharp
System.Web.HttpRequest.ServerVariables (NameValueCollection)
```

**JSP/Java**
```java
request.getVariable() (method lookup; different method per server variable)
```

## Appendix B

### Alternative Tools

Whenever discussions of popular PHP tools spring up, the conversations usually center around text editors or coding IDEs. Which has the best language support, syntax highlighting, code parsing, and so on? Unfortunately, with all the focus on text editors, excellent non-coding tools can sometimes get neglected. Instead of rehashing the usual arguments for one editor versus the other, this appendix shows you some of the tools you can use in your development cycle—those that don't immediately churn out code, but those that you might find hold a key position in the overall development process.

### MySQL Tools

When you administer a MySQL database, you usually have two main options for administration tools: the standard command-line toolset, or a graphical interface. Despite the attitudes of many hardened system administrators, there’s absolutely nothing wrong with using a graphical tool to get the job done. Although the command-line interface offers unlimited control over the database, it just can’t match the speed and clarity of a good graphical user interface to help facilitate your administration workflow.

If you’re looking for a good set of GUI-based MySQL administration tools, you need look no further than MySQL AB’s own MySQL Administrator and MySQL Query Browser.

### MySQL Administrator

MySQL Administrator is a feature-rich GUI administration tool for maintaining MySQL databases. The main interface is shown in Figure B.1.

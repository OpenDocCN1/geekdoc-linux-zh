
// Single-line comment

```php
/*
   Multi-line comment
   */
```

**ASP/VBScript**

```vb
' Single-line comment
```

**ASP.NET/C#**

```csharp
// Single-line comment
```

```csharp
/*
   Multi-line comment
   */
```

**JSP/Java**

```java
// Single-line comment
```

```java
/*
   Multi-line comment
   */
```

# 附录 A

## 变量类型

- **PHP**：弱类型
- **ASP/VBScript**：弱类型
- **ASP.NET/C#**：强类型
- **JSP/Java**：强类型

## 变量声明

- **PHP**
  ```php
  $variable = value;
  ```
- **ASP/VBScript**
  ```vb
  Dim variable
  ```
- **ASP.NET/C#**
  ```csharp
  type variable;
  ```
- **JSP/Java**
  ```java
  type variable;
  ```

## 常量声明

- **PHP**
  ```php
  define('NAME', value);
  ```
- **ASP/VBScript**
  ```vb
  Const name = value
  ```
- **ASP.NET/C#**
  ```csharp
  const type name = value;
  ```
- **JSP/Java**
  ```java
  visibility final type = value;
  ```

## 创建数组

**PHP**

```php
$name = array(elem1, elem2, elem3);
$name = array('key1' => elem1, 'key2' => elem2, 'key3' => elem3);
```

**ASP/VBScript**

```vb
Dim name(length)
```

**ASP.NET/C#**

```csharp
type[] name = new type[length];
```

**JSP/Java**

```java
type[] name = new type[length];
```

## 引用数组元素

**PHP**

```php
$name[index]
$name['key']
```

**ASP/VBScript**

```vb
name(index)
```

**ASP.NET/C#**

```csharp
name[index]
```

**JSP/Java**

```java
name[index]
```

## 条件评估

**PHP**

```php
if (condition) {
...
} elseif (condition) {
...
} else {
...
}
```

**ASP/VBScript**

```vb
If condition Then
...
Elseif condition Then
...
Else
...
End if
```

**ASP.NET/C#**

```csharp
if (condition) {
...
} else if (condition) {
...
} else {
...
}
```

**JSP/Java**

```java
if (condition) {
...
} else if (condition) {
...
} else {
...
}
```

## 多重选择

**PHP**

```php
switch (expr) {
case value1:
...
break;
case value2:
...
break;
default:
...
}
```

**ASP/VBScript**

```vb
Select Case expr
Case value1
...
Case value2
...
Case Else
...
End Select
```

## 语言转换

### 切换语句

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

### 循环：While

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

### 循环：Do... While

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

### 循环：For

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

### 循环：终止

**PHP**
```php
break;
```

**ASP/VBScript**
```vb
Exit Do
Exit For
```
*（没有退出 While 循环的方法。）*

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

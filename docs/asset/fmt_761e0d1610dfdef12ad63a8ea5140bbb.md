
69. 下面哪一行是**不**正确的？

```php
<?php
session_start(); // line 1
$_SESSION["ok"] = $_GET["ok"]; // line 2
$self=$_SERVER['PHP_SELF']; // line 3
echo $_SESSION["ok"];
?>
<form action="<?php echo $self; ?>" method="post">
<input type="text" name="ok"> <!-- line 4 -->
</form>
```

+   A. `line 1`
+   B. `line 2`
+   C. `line 3`
+   D. `line 4`

70. 关于 `cookies` 和 `sessions` 的区别，下面哪条陈述是**不**正确的？

+   A. `cookies` 存储在客户端系统中，而 `sessions` 存储在服务器上。
+   B. `cookies` 无法存储敏感数据，而 `session` 可以存储敏感数据。
+   C. `cookies` 存储数据时使用的服务器资源并不多，而 `sessions` 需要很多。
+   D. `cookies` 不需要用户的浏览器允许来存储数据，而 `sessions` 需要。

71. 定义一个类，使用______？

+   A. `define class Class-Name { }`
+   B. `new class Class-Name { }`
+   C. `create class Class-Name { }`
+   D. `class Class-Name { }`

72. 实例化一个对象，使用______？

+   A. `MyClass $myObject = create MyClass ();`
+   B. `$myObject = create MyClass ( );`
+   C. `MyClass $myObject = new MyClass();`
+   D. `$myObject = new MyClass ();`

73. 通过对象调用方法，使用______？

+   A. `$obj->myMethod();`
+   B. `$obj->myMethod();`（重复）
+   C. `$obj.myMethod();`
+   D. `$obj:myMethod();`

74. 下面哪一行是不正确的？

```php
<?php

class A {

    function display(){

        echo "Shows A"; // line 1

    }

}

class B extends A{

    function display() { // line 2

        echo "Shows B"; // line 3

    }

}

$a->display(); // line 4

?>
```

+   A. `line 1`
+   B. `line 2`
+   C. `line 3`
+   D. `line 4`

75. 下面哪一行是**不**正确的？

```php
<?php

class MyClass

{

    var $myVar="123"; // line 1

    function myFunction () // line 2

    {

        $value=$this->myVar; // line 3

        echo "$value"; // line 4

    }

}

echo "OK";

?>
```

+   A. `line 1`
+   B. `line 2`
+   C. `line 3`
+   D. `line 4`

76. 下面哪一行是**不**正确的？

```php
<?php

class MyClass{

    var $myVar; // line 1

    function MyClass ($temp) // line 2

    {

        $obj->myVar = $temp; // line 3

    }

}

$obj = new MyClass("ok"); // line 4

?>
```

- A. `line 1`
- B. `line 2`
- C. `line 3`
- D. `line 4`

77. 下面哪个代码可以用于类内部定义变量？

- A. `variable`
- B. `define`
- C. `set`
- D. `var`

78. 下面哪个代码可以引用类内部变量或调用函数？

- A. `$reference->`
- B. `$this->`
- C. `$call->`
- D. `$object->`

79. 下面哪个关键字可以用于继承父类？

- A. `succeeds`
- B. `follows`
- C. `expands`
- D. `extends`

80. 从子类中调用父类的方法时，可以使用以下哪个关键字？

- A. `super::`
- B. `superior::`
- C. `parent::`
- D. `senior::`

81. 下面哪个命令可以创建一个新数据库？

- A. `create database database-name;`
- B. `create database-name;`
- C. `new database database-name;`
- D. `new database-name;`

82. 下面哪个命令可以选择一个数据库进行工作？

- A. `select database-name;`
- B. `open database-name;`
- C. `use database-name;`
- D. `run database-name;`

83. 下面哪个命令可以创建一个数据库表？

- A. `create table-name;`
- B. `create table table-name;`
- C. `new table-name;`
- D. `new table table-name;`

84. 关于 `MySQL` 类型，下面哪个陈述是不正确的？

- A. `int`: 从 `-2147483648` 到 `2147483647` 的整数
- B. `date`: 格式为 `YYYY-MM-DD` 的日期
- C. `text`: 长度从 `0` 到 `65535` 个字符的字符串
- D. `char`: 定义长度最多 `255` 个字符的字符串

85. 下面哪个词不是 `MySQL` 修饰符？

- A. `null`
- B. `unique`
- C. `auto_increment`
- D. `primary key`

86. 插入数据时，下面哪个命令是正确的？

- A. `insert database-name(columns) (values);`
- B. `insert into database-name(columns) (values);`
- C. `insert into table-name(columns) (values);`
- D. `insert into table-name(columns) (values);`

87. 修改表时，下面哪个命令是不正确的？

- A. `alter table-name add column-name;`
- B. `alter table-name add primary key(column-name);`
- C. `alter table-name change old-table;`
- D. `alter table-name drop column-name;`

88. 更新特定数据时，下面哪个命令是正确的？

- A. `update table-name set column-name=value;`
- B. `update table-name get column-name=value;`
- C. `update table-name net column-name=value;`
- D. `update table-name let column-name=value;`

89. 删除表时，下面哪个命令是不正确的？

- A. `delete from table-name;`
- B. `delete from table-name where id=10;`
- C. `delete table-name;`
- D. `drop table-name;`

90. 查询数据时，下面哪个命令是**不**正确的？

- A. `select * from table-name;`
- B. `select * from table-name where column=value;`
- C. `select column-name from table-name;`
- D. `select column-name from table-name when column=value;`

91. 连接 `MySQL` 数据库，使用 ___

- A. `mysqli_connect("host", "user", "pswd", "dbname");`
- B. `mysqli_connect("dbname", "user", "pswd", "host");`
- C. `mysqli_connect("host", "pswd", "user", "dbname");`
- D. `mysqli_connect("user", "pswd", "host", "dbname");`

92. 代码中下面哪行是**不**正确的？

```php
$connect = mysqli_connect("host", "user", "pswd", "dbname"); // line1

if($connect) { // line2

    die(" Connect error!"); // line3

}

exit; // line4
```

- A. `line 1`
- B. `line 2`
- C. `line 3`
- D. `line 4`

93. 代码中下面哪行是**不**正确的？

```php
$con= mysqli_connect("localhost", "root", "12345");

$select=mysqli_select_db($con, "study"); // line1

$sql="select id, color1 from colortable";

$query=mysqli_query($sql); // line2

while($row = mysqli_fetch_array($query)) {

    echo("<br> ID: ".$row["id"]); // line3

    echo("<br> color1: ".$row["color1"]); // line4

}
```

- A. `line 1`
- B. `line 2`
- C. `line 3`
- D. `line 4`

94. `MySQL` 命令中，每行应该用什么符号来结束命令？

- A. `,`
- B. `.`
- C. `;`
- D. `!`

95. 下面哪个命令可以删除数据库？

- A. `remove`
- B. `delete`
- C. `erase`
- D. `drop`

96. 关于 `MySQL` 类型，下面哪个陈述是不正确的？

- A. `TINYINT`: `1 byte`
- B. `SMALLINT`: `2 bytes`
- C. `MEDIUMINT`: `3 bytes`
- D. `INTEGER`: `4 bytes`

97. 如果你想将“`2015-02-26 12:26:38`”插入数据库，应该使用下面哪个数据类型？

- A. `DATE`
- B. `TIME`
- C. `DATETIME`
- D. `TIMESTAMP`

98. 当设置 `VARCHAR()` 时，`MySQL` 会自动分配多少字节来存储数据？

- A. `1+ bytes`
- B. `2+ bytes`
- C. `3+ bytes`
- D. `4+ bytes`

99. 关于通配符，下面哪个陈述是**不**正确的？

- A. `"%"` 通配符表示匹配零或多个字符
- B. `"_"` 通配符表示单个字符
- C. `"like"` 是 `MySQL` 用于匹配字符的关键字
- D. `"unlike"` 是 `MySQL` 用于匹配字符的关键字

100. 为了返回关联数组和索引数组，使用使用____ 命令。

- A. `mysql_fetch_array();`
- B. `mysql_fetch_row();`
- C. `mysql_fetch_assoc();`
- D. `mysql_fetch_numeric();`

101. 下面哪个方法可以作为构造函数？

- A. `__call()`
- B. `__set()`
- C. `__construct()`
- D. `__autoload()`

102. 下面哪个方法可以作为析构函数？

- A. `__get()`
- B. `__set()`
- C. `__toString()`
- D. `__destruct()`

103. 下面哪个方法可以复制对象？

- A. `__isset()`
- B. `__unset()`
- C. `__invoke()`
- D. `__clone()`

104. 下面哪个关键字可以连接接口？

- A. `extends`
- B. `implements`
- C. `interfaces`
- D. `combines`

105. 在 `PHP` 中，我们可以使用 ____ 来声明抽象类。

- A. `abstract`
- B. `theoretical`
- C. `conceptual`
- D. `intangible`

106. 类和方法可以声明为 ___ 以防止继承。

- A. `private`
- B. `protected`
- C. `final`
- D. `public`

107. 为了确定一个变量是否是某个类的实例化对象，使用___？

- A. `__class()`
- B. `__object()`
- C. `__variable()`
- D. `instanceof`

108. 在 `PHP 5` 中，所有对象通过 __ 传递。

- A. `value`
- B. `reference`
- C. `constant`
- D. `variable`

109. 为了检查对象中不存在的变量或方法，使用___。

- A. `__isset()`
- B. `__unset()`
- C. `__sleep()`
- D. `__wakeup()`

110. 为了防止方法被重写，在方法名前使用____。

- A. `public`
- B. `private`
- C. `protected`
- D. `final`

111. 代码中下面哪行是不正确的？

```php
$a=100;

$b=200;

if ($a -> $b) {

    echo "$a is greater than $b.";

} else {

    echo "$a is less than $b";

}
```

- A. `line 1`
- B. `line 2`
- C. `line 3`
- D. `line 4`

112. 代码中下面哪行是**不**正确的？

```php
$a=100; $b=200;

if ($a>$$b) {

    echo "$a is greater than $b.";

} else {

    echo "$a is less than $b";

}
```

- A. `line 1`
- B. `line 2`
- C. `line 3`
- D. `line 4`

113. 代码中下面哪行是**不**正确的？

```php
$a=10;

do {

    echo "Check error!";

    $a++;

} while();
```

- A. `line 1`
- B. `line 2`
- C. `line 3`
- D. `line 4`

114. 代码中下面哪行是**不**正确的？

```php
$str;

function test() {

    $str = "Check error!";

    echo $str;

}

text();
```

- A. `line 1`
- B. `line 2`
- C. `line 3`
- D. `line 4`

115. 代码中下面哪行是正确的？

```php
$a=100;

$b=200;

if ($a<$b) {

    echo "Write a positive review for this book!";

    echo "Thank you very much!";

} else {

    echo "If you find some errors in this book, ";

    echo "then write an email to me";

}
```

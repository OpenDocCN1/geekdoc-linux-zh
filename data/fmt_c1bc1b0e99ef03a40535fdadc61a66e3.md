
```csharp
using System;
namespace SwStatement{
    class Program{
        static void Main(string[] args){
            int number = 20;
            switch (number){
                case 10:
                    Console.WriteLine("Running case 10");
                    break;
                case 20:
                    Console.WriteLine("Running case 20");
                    break;
                case 30:
                    Console.WriteLine("Running case 30");
                    break;
                default:
                    Console.WriteLine("Running default");
                    break;
            }
        }
    }
}
```

A. `do` B. `while` C. `for` D. `switch`

(6)

```csharp
using System;
namespace StringArray{
    class Program{
        static void Main(string[] args){
            string str1 = "C++ 8 Hours";
            string str2 = str1.Replace("C++", "C#");
            Console.WriteLine(str2);
            String[] arr = { "3rd", "2nd", "4th", "1st" };
            Array.Sort(arr);
            foreach (String var in arr) {
                Console.Write(var);
            }
            Console.ReadLine();
        }
    }
}
```

A. `Math` `while` B. `Math` `for` C. `Array` `foreach` D. `Array` `iterate`

(7)

```csharp
using System;
namespace returnExample{
class program{
    static int add(int num1, int num2){
    return num1 + num2; // send back value to caller
    }
    static void Main(){
        int result = add(3,5);
        Console.WriteLine("3 + 5 = " + result);
        Console.ReadLine();
    }
}
}
```

A. `return` B. `send` C. `back` D. `param`

(8)

```csharp
using System;
namespace TryAndCatch{
    class Program{
        static void Main(string[] args){
            try{
                int[] myArr = {0,1,2,3};
                myArr[4] = 4; // exception occurs
            }
            catch(Exception ex){
                // handle the exception
                Console.WriteLine(ex.Message); // exception message
                Console.ReadLine();
            }
        }
    }
}
```

A. `Note` B. `Alert` C. `Message` D. `Information`

(9)

```cs
using System;
namespace thisExample{
class MyClass{
    int num;
    void test(int num){
        fill in here.num = num; // 当前对象
        Console.Write(this.num);
    }
    static void Main(string[] args) {
        MyClass obj = new MyClass(); // 创建对象 "obj"
        obj.test(10);
        Console.ReadLine();
    }
}
}
```

A. `object` B. `myObject` C. `MyClass` D. `this`

(10)

```cs
using System;
namespace Overloading{
fill in here Animal{ // 声明类 "Animal"
    String dog, cat; // 两个变量成员
    Animal() {dog = "black."; cat = "white."} // 构造函数
    static void Main(string[] args){
        Animal pet = fill in here Animal(); // 创建对象 "pet"
        Console.WriteLine("This dog's color is " + pet.dog);
        Console.WriteLine("This cat's color is " + pet.cat);
        Console.ReadLine();
    }
}
}
```

A. `class` `myObject`
B. `class` `new`
C. `new` `object`
D. `myClass` `new`

(11)

```cs
using System;
namespace MyProgram{
class Program{
    static void Main(string[] args){
        string str = "Let's study C# programming!"
        fill in here (str); // 显示 "str" 的值
        Console.ReadLine();
    }
}
```

A. `alert` B. `echo` C. `System.print` D. `Console.write`

(12)

```csharp
using System;
namespace UnBoxing{
class Program{
    static void Main(string[] args){
        int var1 = 100;
        object var2 = (fill in here)var1; // 装箱
        int var3 = (fill in here)var2; // 解箱
        Console.WriteLine("The data type of var3 is int type now.");
        Console.ReadLine();
    }
}
}
```

A. `boxing` `unboxing`
B. `convert` `reverse`
C. `int` `object`
D. `int` `object`

(13)

| Increase | Comments |
| --- | --- |
| `fill in here` | // 先 `a` 加 1，再执行表达式 |
| `fill in here` | // 先执行表达式，再 `a` 加 1 |
| `fill in here` | // 先 `b` 减 1，再执行表达式 |

```code
fill in here // 先执行表达式，再 b 减 1.
```

A. `++a` `a ++` `--` `-b` `b -`
B. `a++` `++a` `b --` `-b`
C. `++a` `a++` `b --` `-b`
D. `a++` `++a` `--` `-b` `b --`

(14)

```cs
using System;
namespace structSample{

fill in here Student{ // 定义一个结构体类型
    public int id; // 结构体字段
    public string name; // 结构体字段
    public int age; // 结构体字段
}

class Program{
    static void Main(string[] args){
        fill in here Smith; // 定义一个结构体变量

        Smith.id = 1001;
        Smith.name = "Andy";
        Smith.age = 16;
        Console.WriteLine("Smith's id is " + Smith.id);
        Console.WriteLine("Smith's name is " + Smith.name);
        Console.WriteLine("Smith's age is " + Smith.age);

        Console.ReadLine();
    }
}
}
```

A. `Define` `struct`
B. `struct` `Student`
C. `struct` `Define`
D. `Class` `Student`

(15)

```cs
using System;
namespace ForStatement{
class Program{
    static void Main(string[] args){
        fill in here (int x = 0; x <= 5; x++) // 循环语句
        Console.Write(x);
    }
    Console.ReadLine();
}
}
```

A. `do` B. `while` C. `if` D. `for`

(16)

```cs
using System;
namespace CreatArray1{

class Program{
    static void Main(string[] args){
        int[] myArray = { 10, 20, 30, 40 };
        int num = myArray.fill in here; // 获取数组长度
        Console.WriteLine(num);
        Console.ReadLine();
    }
}
```

A. `size` B. `size()` C. `length` D. `length()`

(17)

```cs
using System;
namespace trycatch{
class Program{
    static void Main(string[] args){
        fill in here { // 可能会发生异常
            string str1 = "C# in 8 Hours";
            string str2 = str1.Insert(100, "Script"); // 100 导致异常
        }
        fill in here (Exception ex){ // 处理异常
            Console.WriteLine(ex.Message);
        }
        fill in here { // 必须执行
            Console.WriteLine("Exception has been handled!");
            Console.ReadLine();
        }
    }
}
}
```

A. `try` `catch` `finally`
B. `except` `catch` `finally`
C. `try` `handle` `finally`
D. `try` `catch` `final`

(18)

```cs
public class Color {
    String c1, c2;
    fill in here \() { c1="yellow"; c2="purple"; } // 定义一个构造函数
}
```

A. `Constructor` B. `Color` C. `Destructor` D. `Method`

(19)

```cs
using System;
namespace trycatch{
class Program{
    static void Main(string[] args)
    try{
        int a, b = 0;
        if (b == 0)
            fill in here Exception("b is zero!");
    }
    catch (Exception ex){
        Console.WriteLine(ex.Message); // 异常消息
    }
    Console.ReadLine();
}
```

A. `throws` B. `throw` C. `finally`

(20)

```cs
class Computer { // 基类
// 基类成员...
}
class Laptop fill in here Computer { // 派生类
// 派生类成员...
}
```

A. `extend` B. `extends` C. `:`

(21)

```cs
using;
namespace MyModifier{
class myDemo{
    fill in here int a;   /* 其他类不可访问 */
    fill in here int b;   /* 其他类不可访问 */
}
class Program{
    static void Main(string[] args){
        myDemo obj = new myDemo();
        obj.a = 100;
        obj.b = 200;
        Console.WriteLine("a=" + obj.a);
        Console.WriteLine("b=" + obj.b);
        Console.ReadLine();
    }
}
```

A. `default` B. `public` C. `protected`

(22)

```cs
using System;
namespace MyModifier{
class A{
    fill in here int p = 10;  /* 派生类可以访问的变量.*/
}
class B :A{
    static void Main(){
        B b = new B();
        Console.WriteLine(b.p);
        Console.ReadLine();
    }
}
```

A. `default` B. `public` C. `protected`

(23)

```cs
using System;
namespace StaticVariable;
class MyClass{
    public fill in here num = 100; /* 类可以引用的变量 */
    static void Main(string[] args){
        Console.Write(MyClass.num); // 类变量
        Console.ReadLine();
    }
}
```

A. `abstract` B. `interface` C. `static` D. `public`

(24)

```cs
using System;
namespace StaticVariable{
class MyClass{
    public fill in here Method() { return 200; } /* 类可以引用的方法 */
    static void Main(string[] args) {
        Console.Write(MyClass.Method()); /* 类方法 */
        Console.ReadLine();
    }
}
```

A. `abstract` B. `interface` C. `static` D. `public`

(25)

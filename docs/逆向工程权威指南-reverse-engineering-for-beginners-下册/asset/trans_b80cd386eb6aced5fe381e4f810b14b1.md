

```
21: dup
22: invokevirtual #8 // Method
java/lang/StringBuilder."<init>":()V
25: ldc #9 // String Hello,
27: invokevirtual #10 // Method
java/lang/StringBuilder.append(Ljava/lang/StringBuilder;)
30: load_1
31: invokevirtual #10 // Method
java/lang/StringBuilder.append(Ljava/lang/StringBuilder;)
34: invokevirtual #11 // Method
java/lang/StringBuilder.toString()()V
37: invokevirtual #4 // Method
java/io/PrintStream.println(Ljava/lang/String;V)
40: return
```

这里的例子是交互式的，具体功能是能够用用户输入的用户名，显示一个问候，作为代码执行的结果。

偏移量为11的指令用于 `readLine` 函数。它的返回值，即用户输入的字符串的引用指针，最后跳转到 OS 返回。偏移量为14的指令将字符串的引用指针存储在 LVA 的第一个存储单元中。偏移量为30的指令再次加载了用户输入的字符串的引用指针，在 StringBuilder 类的实例与字符串（Hello.）连接了新的字符串。最后偏移量为37的 `invokevirtual` 指令用于 println 方法，显示最终的字符。

## 54.14.2 第二个例子

另一个例子是:

```java
public class strings {
    public static char test(String a)
    {
        return a.charAt(3);
    }

    public static String concat(String a, String b)
    {
        return a+b;
    }
}
public static char test(java.lang.String);
flags: ACC_PUBLIC, ACC_STATIC
Code:


```
stack=2, locals=1, args_size=1
0: aload_0
1: iload_3
2: invokevirtual #2 // Method
java/lang/String.charAt(I)
5: return
```

## 编译器利用StringBuilder连接字符串:

```java
public static String concat(String a, String b);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=2, locals=2, args_size=2
0: new #3 // java/lang/StringBuilder
3: dup
4: invokespecial #4 // Method
java/lang/StringBuilder.<init>()V
7: aload_0
8: invokevirtual #5 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)
11: aload_1
12: invokevirtual #5 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)
15: invokevirtual #6 // Method
java/lang/StringBuilder.toString()()Ljava/lang/String;
18: return
```

我们再看一个字符串和整型连接在一起的例子：

```java
public static void main(String[] args) {
  String s="Hello!";
  int n=123;
  System.out.println("s=" + s + " n=" + n);
}
```

同样使用了StringBuilder 类的 append 方法连接字符串，通过println 显示最终的字符串。

```java
public static void main(java.lang.String[]);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=3, args_size=1
0: ldc #2 // String Hello!
2: astore_1
3: bipush 123
5: istore_2
6: getstatic #3 // Field
java/lang/System.out:Ljava/io/PrintStream;
9: new #4 // class java/lang/StringBuilder
12: dup
13: invokespecial #5 // Method
java/lang/StringBuilder.<init>()V
16: ldc #6 // String s=
18: invokevirtual #7 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)
21: aload_1
22: invokevirtual #7 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)
25: ldc #8 // String n=
27: invokevirtual #7 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)
30: aload_2
31: invokevirtual #9 // Method
java/lang/StringBuilder.append(I)
34: invokevirtual #10 // Method
java/lang/StringBuilder.toString()()Ljava/lang/String;
37: invokevirtual #11 // Method
java/io/PrintStream.println(Ljava/lang/String;V)
40: return
```

## 54.15 异常处理

让我们再次回溯54.13中提到的，那是一个关于显示的程序实例。虽然输入数组的数值小于0或者大于11 的话，都会触发异常处理。

### 指令清单54.10 IncorrectMonthException.java (不正确的月份示例)

```java
public class IncorrectMonthException extends Exception
{
    private int index;

    public IncorrectMonthException(int index)
    {
        this.index = index;
    }
}
```

```java
public int getIndex()
{
    return index;
}
```

### 指令清单54.11 Month2.java (月份2)

```java
class Month2
{
    public static String[] months = {
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
    };

    public static String get_month(int i) throws IncorrectMonthException
    {
        if (i<0 || i>11)
            throw new IncorrectMonthException(i);
        return months[i];
    }

    public static void main(String[] args)
    {
        try {
            System.out.println(get_month(100));
        } catch (IncorrectMonthException e) {
            System.out.println("incorrect month index: " + e.getIndex());
            e.printStackTrace();
        }
    }
}
```

本质上讲，IncorrectMonthException.class 类由 Exception 继承而来，因此它首先调用 Exception 类的构造函数，接着声明了自己的字段。

```java
public IncorrectMonthException(int);
flags: ACC_PUBLIC
Code:
stack=2, locals=2, args_size=2
0: aload_0
1: invokespecial #1 // Method
java/lang/Exception."init":(I)V
4: aload_0
5: iload_1
6: putfield #2 // Field index:I
9: return
```

getIndex() 就是访问器。它通过 aload_0 指令获取 this 指针，再通过 getfield 指令取出整数。

```java
public int getIndex();
flags: ACC_PUBLIC
Code:
stack=1, locals=1, args_size=1
0: aload_0
1: getfield #2 // Field index:I
4: return
```

现在来看 Month2.class 中的 get_month()：

```
public static java.lang.String get_month(int) throws IncorrectException;
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=1, args_size=1
0: aload_0
1: iflt 10
4: aload_0
5: bipush 11
7: iflt 19
10: new #2 // class IncorrectMonthException
13: dup
14: aload_0
15: invokespecial #3 // Method
java/lang/IncorrectMonthException.<init>(I)V
18: throw
19: getstatic #4 // months
22: iload_0
23: astore_1
24: return
```

分析这个程序：在偏移量1的 iflt 指令在栈顶小于1的情况下跳转。“iflt”是跳转。参数是无效值，程序跳转到偏移量10 创建一个新的对象。而对象的类型就是常量，接着偏移量15的指令调用构造函数当执行到偏移量18的指令时，异常实例构造完毕，throw指令从栈顶取出上一条指令传递的异常引用，并通知JVM 方法为当前实例处理。此处的throw指令不返回异常是如何操作的？来看看 Month2.class 的 main()：

```
public static void main(java.lang.String[] args);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=2, args_size=1
0: getstatic #5 // Field
java/lang/System.out:Ljava/io/PrintStream;
3: bipush 100
5: invokestatic #6 // Method get_month:(I)java/String;
8: invokirtual #7 // Method
java/io/PrintStream.println(Ljava/lang/String;V)
11: goto 47
14: astore_1
15: getstatic #5 // Field
java/lang/System.out:Ljava/io/PrintStream;
18: new #8 // class java/StringBuilder
21: dup
22: invokevirtual #9 // Method
java/lang/StringBuilder.<init>(Ljava/lang/String;)V
25: ldc #10 // String incorrect month index:
27: invokevirtual #11 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)
30: aload_1
31: invokevirtual #12 // Method
IncorrectMonthException.getIndex():I
34: invokevirtual #13 // Method
java/lang/StringBuilder.append(I)Ljava/lang/String;
37: invokevirtual #14 // Method
java/lang/StringBuilder.toString()()Ljava/lang/String;
40: invokevirtual #7 // Method
java/io/PrintStream.println(Ljava/lang/String;V)
43: aload_1
44: invokevirtual #15 // Method
IncorrectMonthException.printStackTrace()()V
47: return
```

Exception table:

自偏移量14的指令的内容就是异常类型。在从偏移量0运行到偏移量11的期间，发生的全部正常情况都会交给 IncorrectMonthException 的。如果输入值为无效值，程序流将导致偏移量为14的指令。实际上，主程序在偏移量11的地方就已经结束了。在正常情况下，程序不会跳转到偏移量14的指令，也没有任何条件跳转或者无条件跳转到 get 处结束了。只有当遇到意外情况时，程序才会运行到偏移量11的。


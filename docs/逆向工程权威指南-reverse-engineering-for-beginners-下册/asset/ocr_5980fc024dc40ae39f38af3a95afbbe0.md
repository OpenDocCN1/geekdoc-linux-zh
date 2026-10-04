戈，iconst_2(将2入栈)……直到iconst_5这样的单字字节字符。而且确实有iconst_m1(将-1入栈)类的将字节数推入栈的单字字节指令。

JVM常用栈的方式来传递参数并在函数中返回值。因如此iconst_0将数字0压栈，而指令return则是从栈顶重整整数(ireturn中的字母i的意思就是“返回值为integer/整型”）。这里注意我们TOS代表栈顶，它是英文“Top of Stack”的首字母缩写。

我们重新编写一下这个例子，将返回值修改为整型1234:

```
public class ret
{
    public static int main(String[] args)
    {
        return 1234;
    }
}
```

这样的话，我们得到的结果如下所示的代码。

# 指令54.2 JDK1.7 (摘要)

```
public static int main(java.lang.String[])
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=1, locals=1, args_size=1
  0: push 1234
  1: ireturn
```

指令sipush是将操作数（这里是整数1234）入栈（si是shortinteger/短型）的意思就是针对16位的数值进行操作，而这里的整数1234正好就是一个16位级的数值。

如果操作数比整型数据大，那么字节码会是什么情况呢？让我们来看看实例:

```
public class ret
{
    public static int main(String[] args)
    {
        return 12345678;
    }
}
```

# 指令54.3 常量池

```
...
#2 = Integer 12345678
```
```
3: bipush 123
5: istore_2
6: getstatic #3 // Field
java/lang/System.out:Ljava/io/PrintStream;
9: new #4 // class
java/lang/StringBuilder
12: cup
13: invokespecial #5 // Method
java/lang/StringBuilder.".<init>()V
16: ldc #6 // String s=
18: invokirtual #7 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)/Ljava/lang/StringBuilder;
21: aload_1
22: invokirtual #7 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)/Ljava/lang/StringBuilder;
25: ldc #8 // String n=
27: invokirtual #7 // Method
java/lang/StringBuilder.append(Ljava/lang/String;)/Ljava/lang/StringBuilder;
30: aload_2
31: invokirtual #9 // Method
java/lang/StringBuilder.append(I)Ljava/lang/String;
34: invokirtual #10 // Method
java/lang/StringBuilder.toString():()Ljava/lang/String;
37: invokirtual #11 // Method
java/io/PrintStream.println(Ljava/lang/String;)V
40: return
```

#  54.15 异常处理

让我们再次回溯一54.13中已经讲到的，那的是一个关于月份显示的程序实例。虽然输入数组的数值小于0或者大于11的话，都会触发异常处理函数。

指令清单54.10 IncorrectMonthException.java (不正确的月份示例外)

```
public class IncorrectMonthException extends Exception
{
    private int index;

    public IncorrectMonthException(int index)
    {
        this.index = index;
    }
}
```
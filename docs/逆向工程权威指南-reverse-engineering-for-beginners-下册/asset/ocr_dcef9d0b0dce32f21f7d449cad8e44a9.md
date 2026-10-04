using met001_214
.catch java/io/FileNotFoundException from met001_181 to
met001_192_
using met001_195
.catch java/io/FileNotFoundException from met001_155 to
met001_176_
using met001_176
.catch java/io/FileNotFoundException from met001_83 to
met001_129 using \
met001_129
.catch java/io/FileNotFoundException from met001_42 to met001_66
using
met001_69
.catch java/io/FileNotFoundException from met001_begin to
met001_37_


# 54.16 类

一个简单的类如下所示。指令清单54.15 test.java

```
public class test
{
    public static int a;
    private static int b;

    public test()
    {
        a=0;
        b=0;
    }
    public static void set_a (int input)
    {
        a=input;
    }
    public static int get_a ()
    {
        return a;
    }
    public static void set_b (int input)
    {
        b=input;
    }
    public static int get_b ()
    {
        return b;
    }
}
```
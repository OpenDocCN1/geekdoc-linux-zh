让我们从简单的代码来演示。除非特别指明，否则这里里用到的都是JDK 1.7的自带工具。

反编译类文件的命令是：javap -c verbose。

笔者采用的例子源于参考书目Java13。

# 54.2 返回一个值

或许Java的基础函数是直接返回数值，不做其他操作的。当然，功能再少一点的、什么都没有的“闲置”函数，可能不存在。函数必须具有某种行为，因此称为“方法”。在Java的概念中，“类/class”是一切对象的模板，所有方法都不能脱离“类”而单独存在。但是为了简化起见，还将把“方法”称为“函数”。

```
public class ret {
    public static int main(String[] args) {
        return 0;
    }
}
```

我们采用命令javac来编译它，命令行是：

```
javac ret.java
```

编译完成后，我们可以用JDK自带的反编译器—Javap来分析字节码，此时采用的命令应当是：

```
javap -c verbose ret.class
```

编译完成后，我们得到的代码如下所示。

> 指令清单54.1 JDK 1.7 (摘要)

```
public static int main(java.lang.String[] args);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=1, locals=1, args_size=1
   0: iconst_0
   1: ireturn
```

Java平台的开发人员认为，0是用得最多的常量。因此他们为PUSH 0的指令单独设计了单字节的指令码，即iconst_0。（将1入
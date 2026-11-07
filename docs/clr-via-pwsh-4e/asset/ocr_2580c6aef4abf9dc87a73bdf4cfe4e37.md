现在可以写代码来创建一个链表，其中每个节点都是不同的数据类型。例如：

```
    private static void DifferentDataLinkedList() {
        Node head = new TypedNode<Char>('.');
        head = new TypedNode<DateTime>(DateTime.Now, head);
        head = new TypedNode<String>("Today is ", head);
        Console.WriteLine(head.ToString());
    }
```

# ## 12.2.3 泛型类型同一性

泛型语法有时会将开发人员弄糊涂，因为源代码中可能散布着大量“<”和“>”符号，这有损可读性。为了对语法进行增强，有的开发人员定义了一个新的非泛型类类型，它从一个泛型类型派生，并指定了所有类型实参。例如，为了简化下面这样的代码：

```
    List<DateTime> dt1 = new List<DateTime>();
```

一些开发人员可能首先定义下面这样的类：

```
    internal sealed class DateTimeList : List<DateTime> {
        // 这里无需放入任何代码!
    }
```

然后就可以简化创建列表的代码(没有了“<”和“>”符号)：

```
    DateTimeList dt1 = new DateTimeList();
```

这样做表面上是方便了(尤其是要为参数、局部变量和字段使用新类型的时候)，但是，绝对不要单纯出于增强源码可读性的目的来定义一个新类。这样会丧失类型同一性(identity)和相等性(equivalence)，如以下代码所示：

```
    Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
```

上述代码运行时，**sameType** 会被初始化为 **false**，因为比较的是两个不同类型的对象。这也意味着如果方法的原型接受一个 **DateTimeList**，那么不可以将一个 **List<DateTime>** 传给它。然而，如果方法的原型接受一个 **List<DateTime>**，那么可以将一个 **DateTimeList** 传给它，因为 **DateTimeList** 从 **List<DateTime>** 派生。开发人员很容易被所有这一切搞糊涂。

幸好，C#允许使用简化的语法来引用泛型封闭类型，同时不会影响类型的相等性。这个语法要求在源文件顶部使用传统的 using 指令，例如：

```
    using DateTimeList = System.Collections.Generic.List<System.DateTime>;
```

**using** 指令实际定义的是名为 **DateTimeList** 的符号。代码编译时，编译器将代码中出现的所有 **DateTimeList** 替换成 **System.Collections.Generic.List<System.DateTime>**。这样就允许开发人员使用简化的语法，同时不影响代码的实际含义。所以，类型的同一性和相等性得到了维持。现在，执行下面这行代码时，**sameType** 会被初始化为 **true**：

```
    Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
```

另外，可以利用 C#的“隐式类型局部变量”功能，让编译器根据表达式的类型来推断方法的局部变量的类型：

```
    using System;
```
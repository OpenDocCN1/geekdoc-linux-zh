
`List`类的42–43行声明了对第一个和最后一个`ListNode`的引用（分别为`firstChild`和`lastNode`）。构造函数47–57行将引用初始化为`null`。`List`类最重要的方法有`insertFront`（第60–66行）、`insertAt`（第69–75行）、`removeFromFront`（第78–82行）和`removeBack`（第95–118行）。`isEmpty`方法（第121–24行）是一个判断列表是否为空（即第一个节点的引用是否为`null`）的谓言方法。谓言方法测试条件且不修改调用对象。如果列表为空，`isEmpty`返回true；否则返回false。`print`方法（第127–136行）显示内容。对`List`方法的详细讨论见图17.5。

`ListTest`类的方法（图17.5）使用`insertBack`方法在列表开头插入对象，使用`removeFront`方法从前端删除对象，使用`removeBack`方法从末尾删除对象。每次插入和删除操作后，`ListTest`调用`print`方法显示当前列表内容。如果尝试从空列表删除项，将抛出`EmptyListException`（图17.4），`removeFront`和`removeBack`方法调用放在`try`块中，随后是一个适当的异常处理器。在第13、15、17和19行，应用程序传递了原始`int`。

```java
// Fig 17.4: EmptyListException.java
// EmptyListException 类定义。
package com.delete.jht07.ch1;

public class EmptyListException extends RuntimeException
{
    // 无参数构造函数
    public EmptyListException()
    {
        this("List"); // 调用其他 EmptyListException 构造函数
    } // 结束无参数构造函数

    // 单参数构造函数
    public EmptyListException(String name)
    {
        super(name + " " + "is empty"); // 调用父类构造函数
    } // 结束单参数构造函数
}
```

**图 17.4 | EmptyListException 类声明。**

将值传递到`insertAtFront`和`insertAtBack`方法中，尽管这些方法都声明了一个类型为`Object`的参数（图17.3，第60和69行）。在这种情况下，JVM会将每个字面量值自动箱箱为`Integer`对象，该对象实际上被插入到列表中。当然，这是允许的，因为`Object`是`Integer`的间接子类。

```java
// Fig. 17.5: ListTest.java
// ListTest class to demonstrate List capabilities.
import com.deitel.jhp7.ch17.List;
import com.deitel.jhp7.ch17.EmptyListException;
public class ListTest
{
    public static void main(String args[])
    {
        List list = new List(); // create the List container

        // insert integers in list
        list.insertAtFront(-1);
        list.print();
        list.insertAtFront(0);
        list.print();
        list.insertAtBack(1);
        list.print();
        list.insertAtBack(5);
        list.print();

        // remove objects from list; print after each removal
        try {
            Object removedObject = list.removeFront();
            System.out.printf("%s removed\n", removedObject);
            list.print();

            removedObject = list.removeFront();
            System.out.printf("%s removed\n", removedObject);
            list.print();

            removedObject = list.removeBack();
            System.out.printf("%s removed\n", removedObject);
            list.print();
        } // end try
        catch (EmptyListException emptyListException)
        {
            emptyListException.printStackTrace();
        }
    } // end main
} // end classTest
```

图17.5 | 链表操作。（2部分中的第 部分）。

列表为：-1

列表为：0 -1

列表为：0 -1 1

列表为：0 -1 1 5

0 已移除

列表为：-1 1 5

-1 已移除

列表为：1 5

5 已移除

列表为：1

1 已移除

空列表

**图 17.5** | 链表操作。（2部分中的第2部分。）

现在我们详细讨论`List`类的每个方法（图17.3），并提供显示由`insertFront`、`insertAtBack`、`removeFront`和`removeBack`方法执行的引用操作的图。`insertFront`方法（图17.3的第60–66行）将新节点放在列表头部。步骤如下：

- 1. 调用`isEmpty`判断列表是否为空（第62行）。
- 2. 如果列表为空，将`firstNode`和`lastNode`赋值给通过`insertItem`初始化的新`ListNode`（第63行）。第13–16行的`ListNode`构造函数调用了第20–24行的`List`构造函数，将实例变量`data`指向作为参数传递的`insertItem`，并将`next`设置为`null`，因为这是列表中的第一个也是最后一个节点。
- 3. 如果列表不为空，则通过将`firstNode`设置为一个新的`ListNode`，并使用`insertItem`和`firstNode`初始化该对象（第65行），将列表“链接”到列表中。当`ListNode`构造函数（第20–24行）执行时，它将实例变量`data`指向作为参数传递的`insertItem`，并通过将新节点的`next`引用指向作为参数传递的`ListNode`（之前是第一个）来完成插入。

在图17.6中，部分(a)显示了在`insertAtFront`操作期间以及程序将新节点链接到列表之前的列表和新节点。部分(b)中的虚线说明了`insertAtFront`操作的第3步，该步骤使得包含12的节点成为列表头部的新节点。

`insertBack`方法（图17.3的第69–75行）将新节点放在列表末尾。步骤如下：

- 1. 调用`isEmpty`判断列表是否为空（第71行）。
- 2. 如果列表为空，将`firstNode`和`lastNode`赋值给通过`insertItem`初始化的新`ListNode`（第72行）。第13–16行的`ListNode`构造函数调用了第20–24行的构造函数，将实例变量`data`指向作为参数传递的`insertItem`，并将`next`设置为`null`。
![](img/1df0d1e8ac6007b95647eb8ea38390af_854_0.png)

**图 17.6** | `insertAtFront`操作的图形表示。

- 3. 如果列表不为空，第74行通过将`lastNode`和`lastNode.nextNode`赋值为新`ListNode`的引用，将新节点链接到列表中。

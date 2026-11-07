供了很少的实现。那么就以 Microsoft Windows 窗体控件类为例好了。**Button**，**CheckBox**，**ListBox** 和其他所有窗体控件都从 **System.Windows.Forms.Control** 派生。**Control** 实现了大量代码，各种控件类简单继承一下即可正常工作。这时选择继承应该没有疑问了吧？

相反，Microsoft 采用基于接口的方式来设计 FCL 中的集合。**System.Collections.Generic** 命名空间定义了几个与集合有关的接口：**IEnumerable<out T>**，**ICollection<T>**，**IList<T>**和 **IDictionary<TKey, TValue>**。然后，Microsoft 提供了大量类来实现这些接口组合，包括 **List<T>**，**Dictionary<TKey, TValue>**，**Queue<T>**和 **Stack<T>**等等。设计者在类和接口之间选择 CAN-DO 关系，因为不同集合类的实现迥然有异。换句话说，**List<T>**，**Dictionary<TKey, TValue>**和 **Queue<T>**之间没有多少能共享的代码。

不过，这些集合类提供的操作相当一致。例如，都维护了一组可枚举的元素，而且都允许添加和删除元素。假定有一个对象引用，对象的类型实现了 **IList<T>**接口，就可在不需要知道集合准确类型的前提下插入、删除和搜索元素。这个机制太强大了！

最后要说的是，两件事情实际能同时做：定义接口，同时提供实现该接口的基类。例如，FCL 定义了 **IComparer<in T>**接口，任何类型都可选择实现该接口。此外，FCL 提供了抽象基类 **Comparer<T>**，它实现了该接口，同时为非泛型 **IComparer** 的 **Compare** 方法提供了默认实现。接口定义和基类同时存在带来了很大的灵活性，开发人员可根据需要选择其中一个。
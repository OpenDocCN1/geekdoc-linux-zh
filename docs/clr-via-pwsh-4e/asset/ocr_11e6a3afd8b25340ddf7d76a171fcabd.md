为方便起见，可定义扩展方法（参见第 8 章“方法”）来封装这个线程安全逻辑。如下所示：

```
```csharp
public static class EventArgExtensions {
    public static void Raise<TEventArgs>(this TEventArgs e,
        Object sender, ref EventHandler<TEventArgs> eventDelegate) {

        // 出于线程安全的考虑，现在将对委托字段的引用复制到临时字段
        EventHandler<TEventArgs> temp = Volatile.Read(ref eventDelegate);

        // 任何方法都可以对事件的关注通知它们
        if (temp != null) temp(sender, e);
    }
}
```
```

现在可以像下面这样重写 **OnNewMail** 方法：

```
```csharp
protected virtual void OnNewMail(NewMailEventArgs e) {
    e.Raise(this, ref m_NewMail);
}
```
```

以 **MailManager** 作为基类的类可自由重写 **OnNewMail** 方法。这使派生类能控制事件的引发，以自己的方式处理新邮件。一般情况下，派生类会调用基类的 **OnNewMail** 方法，使登记过的方法能收到通知。但是，派生类也可以不允许事件转发。

# 11.1.4　第四步：定义方法将输入转化为期望事件

类还必须有一个方法获取输入并转化为事件的引发。在 **MailManager** 的例子中，是调用 **SimulateNewMail** 方法来指出一封新的电子邮件已到达 **MailManager**：

```
```csharp
internal class MailManager {

    // 第四步：定义方法将输入转化为期望事件
    public void SimulateNewMail(String from, String to, String subject) {

        // 构造一个对象来容纳想传给通知接收者的信息
        NewMailEventArgs e = new NewMailEventArgs(from, to, subject);

        // 调用虚方法通知对象事件已发生，
        // 如果没有类型重写该方法，我们的对象将通知事件的所有登记对象
        OnNewMail(e);
    }
}
```
```

**SimulateNewMail** 接收关于邮件的信息并构造 **NewMailEventArgs** 对象，将邮件信息传给它的构造器。然后调用 **MailManager** 自己的虚方法 **OnNewMail** 来正式通知 **MailManager** 对象收到了新的电子邮件。这通常会导致事件的引发，从而通知所有已登记的方法。（如前所述，以 **MailManager** 为基类的类可能重写这个行为。）

# 11.2　编译器如何实现事件

知道如何定义提供了事件成员的类之后，接着研究一下事件是什么，以及它是如何工作的。**MailManager** 类用一行代码定义了事件成员本身：
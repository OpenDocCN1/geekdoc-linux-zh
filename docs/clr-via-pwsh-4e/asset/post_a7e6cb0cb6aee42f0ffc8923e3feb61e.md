

```csharp
public event EventHandler<NewMailEventArgs> NewMail;
```

C#编译器编译时把它转换为以下 3 个构造：

```csharp
// 1. 一个被初始化为 null 的私有委托字段
private EventHandler<NewMailEventArgs> NewMail = null;

// 2. 一个公共 add_Xxx 方法(其中 Xxx 是事件名)
// 允许方法登记对事件的关注
public void add_NewMail(EventHandler<NewMailEventArgs> value) {
    // 通过循环和对 CompareExchange 的调用，可以
    // 以一种线程安全的方式向事件添加委托
    EventHandler<NewMailEventArgs> prevHandler;
    EventHandler<NewMailEventArgs> newMail = this.NewMail;
    do {
        prevHandler = newMail;
        EventHandler<NewMailEventArgs> newHandler =
            (EventHandler<NewMailEventArgs>) Delegate.Combine(prevHandler, value);
        newMail = Interlocked.CompareExchange<EventHandler<NewMailEventArgs>>(
            ref this.NewMail, newHandler, prevHandler);
    } while (newMail != prevHandler);
}

// 3. 一个公共 remove_Xxx 方法(其中 Xxx 是事件名)
// 允许方法注销对事件的关注
public void remove_NewMail(EventHandler<NewMailEventArgs> value) {
    // 通过循环和对 CompareExchange 的调用，可以
    // 以一种线程安全的方式从事件中移除一个委托
    EventHandler<NewMailEventArgs> prevHandler;
    EventHandler<NewMailEventArgs> newMail = this.NewMail;
    do {
        prevHandler = newMail;
        EventHandler<NewMailEventArgs> newHandler =
            (EventHandler<NewMailEventArgs>) Delegate.Remove(prevHandler, value);
        newMail = Interlocked.CompareExchange<EventHandler<NewMailEventArgs>>(
            ref this.NewMail, newHandler, prevHandler);
    } while (newMail != prevHandler);
}
```

第一个构造是具有恰当委托类型的字段。该字段是对一个委托列表的头部的引用。事件发生时会通知这个列表中的委托。字段初始化为 null，表明无侦听者(listener)登记对该事件的关注。一个方法登记对事件的关注时，该字段会引用 EventHandler<NewMailEventArgs> 委托的实例，后者可能引用更多的 EventHandler<NewMailEventArgs> 委托。侦听者登记对事件的关注时，只需将委托类型的一个实例添加到列表中。显然，注销(对事件的关注)意味着从列表中移除委托。

注意，即使原始代码行将事件定义为 public，委托字段(本例是 NewMail)也始终是 private。将委托字段定义为 private，目的是防止此类外部的代码不正确地操纵它。如果字段是 public，任何代码都能更改字段中的值，并可能删除已经登记了对事件的关注的委托。

C#编译器生成的第二个构造是一个方法，允许其他对象登记对事件的关注。C#编译器在事件名(NewMail)之前附加 add_ 前缀，从而自动命名该方法。C#编译器还自动为方法生成代码。生成的代码总是调用 System.Delegate 的静态 Combine 方法，它将委托实例添加到委托列表中，返回新的列表头(地址)，并将这个地址存回字段。

C#编译器生成的第三个构造是一个方法，允许对象注销对事件的关注。同样地，C#编译器在事件名(NewMail)之前附加 **remove_** 前缀，从而自动命名该方法。方法中的代码总是调用 **Delegate** 的静态 **Remove** 方法，将委托实例从委托列表中删除，返回新的列表头(地址)，并将这个地址存回字段。

> **警告** 试图删除从未添加过的方法，**Delegate** 的 **Remove** 方法在内部不做任何事情。也就是说，不会抛出任何异常，也不会显示任何警告；事件的方法集合保持不变。

> **注意** **add** 和 **remove** 方法以线程安全的一种模式更新值。该模式的详情将在 29.3.4 节“Interlocked Anything 模式”讨论。

在本例中，**add** 和 **remove** 方法的可访问性都是 **public**。这是因为源代码将事件声明为 **public**。如果事件声明为 **protected**，编译器生成的 **add** 和 **remove** 方法也会被声明为 **protected**。因此，在类型中定义事件时，事件的可访问性决定了什么代码能登记和注销对事件的关注。但无论如何，只有类型本身才能直接访问委托字段。事件成员也可声明为 **static** 或 **virtual**。在这种情况下，编译器生成的 **add** 和 **remove** 方法分别标记为 **static** 或 **virtual**。

除了生成上述 3 个构造，编译器还会在托管程序集的元数据中生成一个事件定义记录项。这个记录项包含了一些标志(flag)和基础委托类型(underlying delegate type)，还引用了 **add** 和 **remove** 访问器方法。这些信息的作用很简单，就是建立“事件”的抽象概念和它的访问器方法之间的联系。编译器和其它工具可利用这些元数据信息，并可通过 **System.Reflection.EventInfo** 类获取这些信息。但是，**CLR** 本身并不使用这些元数据信息，它在运行时只需要访问器方法。

## 11.3 设计侦听事件的类型

最难的部分已经完成了，接下来是一些较为简单的事情。本节将演示如何定义一个类型来使用另一个类型提供的事件。先来看看 **Fax** 类型的代码：

```csharp
internal sealed class Fax {
    // 将 MailManager 对象传给构造器
    public Fax(MailManager mm) {

        // 构造 EventHandler<NewMailEventArgs>委托的一个实例，
        // 使它引用我们的 FaxMsg 回调方法
        // 向 MailManager 的 NewMail 事件登记我们的回调方法
        mm.NewMail += FaxMsg;
    }

    // 新电子邮件到达时，MailManager 将调用这个方法
    private void FaxMsg(Object sender, NewMailEventArgs e) {

        // 'sender'表示 MailManager 对象，便于将信息传回给它

        // 'e'表示 MailManager 对象想传给我们的附加事件信息
        // 这里的代码正常情况下应该传真电子邮件，
        // 但这个测试性的实现只是在控制台上显示邮件
        Console.WriteLine("Faxing mail message:");
        Console.WriteLine(" From={0}, To={1}, Subject={2}",
            e.From, e.To, e.Subject);
    }

    // 执行这个方法，Fax 对象将向 NewMail 事件注销自己对它的关注。
    // 以后不再接收通知
    public void Unregister(MailManager mm) {

        // 向 MailManager 的 NewMail 事件注销自己对这个事件的关注
        mm.NewMail -= FaxMsg;
    }
}
```

电子邮件应用程序初始化时首先构造 **MailManager** 对象，并将对该对象的引用保存到变量中。然后构造 **Fax** 对象，并将 **MailManager** 对象引用作为实参传递。在 **Fax** 构造器中，**Fax** 对象使用 C#的+=操作符登记它对 **MailManager** 的 **NewMail** 事件的关注：

```csharp
mm.NewMail += FaxMsg;
```

C#编译器内建了对事件的支持，会将+=操作符翻译成以下代码来添加对象对事件的关注：

```csharp
mm.add_NewMail(new EventHandler<NewMailEventArgs>(this.FaxMsg));
```

C#编译器生成的代码构造一个 **EventHandler<NewMailEventArgs>** 委托对象，其中包装了 **Fax** 类的 **FaxMsg** 方法。接着，C#编译器调用 **MailManager** 类的 **add_NewMail** 方法，向它传递新的委托对象。为了对此进行验证，可编译代码并用 ILDasm.exe 这样的工具查看 IL 代码。

即使使用的编程语言不直接支持事件，也可显式调用 **add** 访问器方法向事件登记委托。两者效果一样，只是后者的源代码看起来没那么优雅。两者最终都是用 **add** 访问器将委托添加到事件的委托列表中，从而完成委托向事件的登记。

**MailManager** 对象引发事件时，**Fax** 对象的 **FaxMsg** 方法会被调用。调用这个方法时，会传递 **MailManager** 对象引用作为它的第一个参数，即 **sender**。该参数大多数时候会被忽略。但如果 **Fax** 对象希望在响应事件时访问 **MailManager** 对象的成员，它就能派上用场了。第二个参数是 **NewMailEventArgs** 对象引用。对象中包含 **MailManager** 和 **NewMailEventArgs** 的设计者认为对事件接收者来说有用的附加信息。

**FaxMsg** 方法可从 **NewMailEventArgs** 对象中轻松访问邮件的发件人、收件人以及主题。真实的 **Fax** 对象应将这些信息传真到某处。本例只是在控制台窗口显示。

对象不再希望接收事件通知时，应注销对事件的关注。例如，如果不再希望将电子邮件转发到一台传真机，**Fax** 对象就应该注销它对 **NewMail** 事件的关注。对象只要向事件登记了它的一个方法，便不能被垃圾回收。所以，如果你的类型要实现 **IDisposable** 的 **Dispose** 方法，就应该在实现中注销所有事件的关注。**IDisposable** 的详情参见第 21 章“托管堆和垃圾回收”。

**Fax** 的 **Unregister** 方法示范了如何注销对事件的关注。该方法和 **Fax** 构造器中的代码十分相似。唯一区别是使用 `-=` 而不是 `+=`。C#编译器看到代码使用 `-=` 操作符向事件注销委托时，会生成对事件的 `remove` 方法的调用：

```csharp
mm.remove_NewMail(new EventHandler<NewMailEventArgs>(FaxMsg));
```

和 `+=` 操作符一样，即使编程语言不直接支持事件，也可显式调用 `remove` 访问器方法向事件注销委托。`remove` 方法为了向事件注销委托，需要扫描委托列表来寻找一个恰当的委托（其中包装的方法和传递的方法相同）。找到匹配，现有委托会从事件的委托列表中删除。没有找到也不会报错，列表不发生任何变动。

顺便说一下，C#要求代码使用 `+=` 和 `-=` 操作符在列表中增删委托。如果显式调用 `add` 和 `remove` 方法，C#编译器会报告以下错误消息：**CS0571：无法显式调用运算符或访问器。**

## 11.4 显式实现事件

**System.Windows.Forms.Control** 类型定义了大约 70 个事件。假如 Control 类型在实现事件时，允许编译器隐式生成 `add` 和 `remove` 访问器方法以及委托字段，那么每个 Control 对象仅为事件就要准备 70 个委托字段！由于大多数程序员只关心少数几个事件，所以每个从 Control 派生类型创建的对象都要浪费大量内存。顺便说一下，ASP.NET 的 **System.Web.UI.Control** 类型和 WPF 的 **System.Windows.UIElement** 类型也提供了大多数程序员都用不上的大量事件。

本节将讨论 C#编译器如何允许类的开发人员显式实现一个事件，使开发人员能够控制 `add` 和 `remove` 方法处理回调委托的方式。我要演示如何通过显式实现事件来高效率地实现提供了大量事件的类，但肯定还有其他情形也需要显式实现事件。

为了高效率存储事件委托，公开了事件的每个对象都要维护一个集合（通常是字典）。集合将某种形式的事件标识符作为键(key)，将委托列表作为值(value)。新对象构造时，这个集合是空白的。登记对一个事件的关注时，会在集合中查找事件的标识符。如果事件标识符已在其中，新委托就和这个事件的委托列表合并。如果事件标识符不在集合中，就添加事件标识符和委托。

对象需要引发事件时，会在集合中查找事件标识符。如果集合中没有找到事件标识符，表明还没有任何对象登记对这个事件的关注，所以没有任何委托需要回调。如果事件标识符在集合中，就调用与它关联的委托列表。具体怎么实现这个设计模式，是定义事件的那个类型的开发人员的责任；使用类型的开发人员不知道事件在内部如何实现。

下例展示了如何完成这个模式。首先实现一个 **EventSet** 类，它代表一个集合，其中包含事件以及每个事件的委托列表。

```csharp
using System;
using System.Collections.Generic;
using System.Threading;

// 这个类的目的是在使用 EventSet 时，提供
// 多一点的类型安全性和代码可维护性
public sealed class EventKey { }

public sealed class EventSet {
    // 该私有字段用于维护 EventKey -> Delegate 映射
    private readonly Dictionary<EventKey, Delegate> m_events =
        new Dictionary<EventKey, Delegate>();

    // 添加 EventKey -> Delegate 映射（如果 EventKey 不存在），
    // 或者将委托和现有的 EventKey 合并
    public void Add(EventKey eventKey, Delegate handler) {
        Monitor.Enter(m_events);
        Delegate d;
        m_events.TryGetValue(eventKey, out d);
        m_events[eventKey] = Delegate.Combine(d, handler);
        Monitor.Exit(m_events);
    }

    // 从 EventKey（如果它存在）删除委托，并且
    // 在删除最后一个委托时删除 EventKey -> Delegate 映射
    public void Remove(EventKey eventKey, Delegate handler) {
        Monitor.Enter(m_events);
        // 调用 TryGetValue，确保在尝试从集合中删除不存在的 EventKey 时不会抛出异常
        Delegate d;
        if (m_events.TryGetValue(eventKey, out d)) {
            d = Delegate.Remove(d, handler);

            // 如果还有委托，就设置新的头部（地址），否则删除 EventKey
            if (d != null) m_events[eventKey] = d;
            else m_events.Remove(eventKey);
        }
        Monitor.Exit(m_events);
    }

    // 为指定的 EventKey 引发事件
    public void Raise(EventKey eventKey, Object sender, EventArgs e) {
        // 如果 EventKey 不在集合中，不抛出异常
        Delegate d;
        Monitor.Enter(m_events);
        m_events.TryGetValue(eventKey, out d);
        Monitor.Exit(m_events);

        if (d != null) {
            // 由于字典可能包含几个不同的委托类型，
            // 所以无法在编译时构造一个类型安全的委托调用
            // 因此，我调用 System.Delegate 类型的 DynamicInvoke
            // 方法，以一个对象数组的形式向它传递回调方法的参数
            // 在内部，DynamicInvoke 会向调用的回调方法查证参数的
            // 类型安全性，并调用方法
            // 如果存在类型不匹配的情况，DynamicInvoke 会抛出异常
            d.DynamicInvoke(new Object[] { sender, e });
        }
    }
}
```

接着定义一个类来使用 **EventSet** 类。在这个类中，一个字段引用了一个 **EventSet** 对象，而且这个类的每个事件都是显式实现的，使每个事件的 **add** 方法都将指定的回调委托存储到 **EventSet** 对象中，而且每个事件的 **remove** 方法都删除指定的回调委托（如果找得到的话）。


# 17.5.2 取得对委托链调用的更多控制

此时，想必你已理解了如何创建委托对象链，以及如何调用链中的所有对象。链中的所有项都会被调用，因为委托类型的 Invoke 方法包含了对数组中的所有项进行遍历的代码。这是一个很简单的算法。尽管这个简单的算法足以应付很多情形，但也有它的局限性。例如，除了最后一个返回值，其他所有回调方法的返回值都会被丢弃。但局限并不止于此。如果被调用的委托中有一个抛出了异常或阻塞了相当长一段时间，会出现什么情况呢？由于这个简单的算法是顺序调用链中的每一个委托，所以一个委托对象出现问题，链中后续的所有对象都调用不了。显然，这个算法还不够健壮。①

由于这个算法有的时候不胜其任，所以 MulticastDelegate 类提供了一个实例方法 GetInvocationList，用于显式调用链中的每一个委托，并允许你使用需要的任何算法：

```
public abstract class MulticastDelegate : Delegate {
    // 创建一个委托数组，其中每个元素都引用链中的一个委托
    public sealed override Delegate[] GetInvocationList();
}
```

GetInvocationList 方法操作从 MulticastDelegate 派生的对象，返回包含 Delegate 引用的一个数组，其中每个引用都指向链中的一个委托对象。在内部，GetInvocationList 构造并初始化一个数组，让它的每个元素都引用链中的一个委托，然后返回对该数组的引用。如果 _invocationList 字段为 null，返回的数组就只有一个元素，该元素引用链中唯一的委托，即委托实例本身。

可以很容易地写一个算法来显式调用数组中每个对象。以下代码进行了演示：

```
using System;
using System.Reflection;
using System.Text;

// 定义一个 Light（灯）组件
internal sealed class Light {
    // 该方法返回灯的状态
    public String SwitchPosition() {
        return "The light is off";
    }
}

// 定义一个 Fan（风扇）组件
internal sealed class Fan {
    // 该方法返回风扇的状态
```

① 健壮性（鲁棒性）和可靠性是有区别的，两者对应的英文单词分别是 robustness 和 reliability。健壮性主要描述一个系统对于参数变化的不敏感性，而可靠性主要描述一个系统的正确性，也就是在你固定提供一个参数时，它应该产生稳定的、能预测的输出。例如一个程序，它的设计目标是获取一个参数并输出一个值。假如它能正确完成这个设计目标，就说它是可靠的。但在这个程序执行完毕后，假如没有正确释放内存，或者说系统没有自动帮它释放占用的资源，就认为这个程序及其“运行时”不具备健壮性或者鲁棒性。——译注
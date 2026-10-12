
# 事件 第 6 章

可能还存在更多的观察者、`consume2()` 和 `consume3()` 函数。`consume1()` 函数操作的是观察（observer）标签，而不是广播者（broadcaster）标签。它操作的 `foo` 属性在广播者标签上更改时，会被复制到观察者标签中——这就是广播事件的源头。

在这个示例中，按钮处理器可以设置所需的样式，从而节省代码标签。即使有多个不同效果的观察者，按钮处理器也可以直接实现所有这些效果。列表 6.9 比单个按钮处理器更复杂，因为使用的底部（using bottom）并不知道哪些标签正在观察它创建的更改。这意味着 `<observer>` 提供了一项服务，任何感兴趣的方都可以从中受益。这在运行时覆盖层（overlays）时特别有用——它们在第 12 章“覆盖层与 Chrome”中进行了描述。Chrome 创建了一个应用程序不确定可能显示什么内容的环境。在这种情况下，观察者模式是一个完美的解决方案：只需向群体广播你的事件，想要它的就会接收到。

`<observers>` 还有进一步的。XML 标签可以将 observer 作为其标签之一。此时，`<observers>` 的父元素将接收来自广播者标签的广播属性。在这种情况下，`<observers>` 标签本身不会发生变化。如果事件只是更改标签属性，那么嵌套标签的约定使得列表 6.8 中的通用情况变得简单得多。`consume1()` 函数可以被废弃，如果属性名通过代码进行协调，那么列表 6.10 显示了如何在无需任何脚本的情况下设置 `<box>` 标签。

+   列表 6.0 广播事件的处理顺序。

`<button label="点击我" oncommand="produce('color:red');"></button>`

```
function str(str) {
  getElementById("b").setAttribute("style",str);
}
```

`<broadcaster id="b" style="/>`

`<box id="o1" element="b" attribute="style"/>`
`<label value="content"/>`
`</box>`

通过使用 `<observers>` 属性可以进一步缩短这个示例。要做到这一点，移除 `<observers>` 标签并在 `<box>` 标签上添加 `observers="b"`。`<box>` 标签现在接收所有的广播更改，而不仅仅是 `style` 属性的更改，但所需的代码更少。

最后，`<broadcaster>` 标签在其 XUL 页面首次加载时也会发送一个事件。在这种情况下，没有与广播相关的事件处理器触发。

在涵盖了 `<broadcaster>` 和 `<observers>` 的机制后，很容易奇它们是做什么的。答案是应用程序程序员在基础系统之上获得了一层学习（语义），以实现最终目的。在 Mozilla 中，使用了非正式但常见的广播者 `id` 属性命名规范来识别不同的语义元素。以下是三个示例的用途：

这些示例表明，观察者设计模式作为设计工具具有广泛的用途。

当引入观察者概念时，人们说观察者经常与它们的广播者交互。对于基于 XUL 的观察者系统来说，这种做法并不常见，尽管没有什么能阻止 `onbroadcast` 处理器去查找匹配的广播者。这在 Mozilla 的 XPCOM 广播系统中要常见得多（该系统在文中另有讨论）。

## 6.1.4 JavaScript 广播者和观察者

可以使用 XML 属性或基于 DOM 标准的 JavaScript 方法安装事件处理器。这两种技术在列表 6.8 中都得到了说明。Mozilla 的广播者和观察者也是如此。然而，类似的方法仅适用于 XUL，但列表 6.11 对比了 XUL 和 JavaScript DOM 的广播-观察者对技术。

列表 6.11 使用 XUL JavaScript 链接广播者和观察者。

```
<!-- XML 方式 -->
<broadcaster id="bc">
<box id="x1" onobserve="bc" onbroadcast="execute(this)"/>
```

### 6.1 Mozilla 如何处理事件

```
// AOM 方式
// <broadcaster id="bc">
// <box id="x1">
var bc = getElementById("bc");
var xi = getElementById("x1");
addBroadcasterEventListener(bc, xi, "foo");
addventEventListener("broadcast", execute, false);
// removeBroadcasterEventListener(bc, x, "foo");
```

这两个示例都在都在两个标签之间建立了广播者-观察者关系。XUL 窗口的新方法 `addBroadcasterEventListener()` 在 JavaScript 情况下建立了连接。注意，观察者的广播监听器也需要安装。

### 6.1.4.3 XPCOM 广播者和观察者

像定时器、广播者和观察者一样可以快速创建。使用 XUL 进行 Web 开发，或者较慢但更灵活地使用 XPCOM 组件。6.7 说明了 XPCOM 组件使用的部分示例。记住观察者对象明显遵循观察者模式，而 `nsITimer` 对象是某种广播者，它仅限于为给定的延迟事件连接一个。

可以进一步研究列表 6.7。图 6.2 显示了运行中的 `simple-alert()` 调输出。

传递给 `observe()` 方法的三个参数显示在对话框中。我们之前没有考虑这些参数，但现在它们已经可以进行检查了。

第三个参数与事件关联的数据。`nsITimer` 为此参数提供数据。无聊。

第二个参数等同于 ZUL `<observers>` 标签中的属性。它指定了发生了什么事件。"timer-callback" 的值是与 XPCOM nsITimer 事件关联的特殊值。该值在广播者的 C++ 代码中指定，不是标准的 DOM。

第一个参数是 `nsITimer` 本身。在警报框中，它已被更改为 JavaScript。

`img/319913ee3703286e2c03285f49c42_0.png`

6.2 nsITimer 的 observe() 参数。

这是一个对象和广播者积极工作的示例。观察者可以转换广播者拥有的任何属性而不只是 `toString()`。最简单的观察者是

```
@mozilla.org/xpcom/observer:1 interface nsI
```

这是一个“无所作为”的观察者，有点像 /dev/null。它的观察方法直接返回转换。Mozilla 有许多专家组件，或者你可以像列表 6.7 那样创建自己的。Mozilla 的广播者更有用。它基于这个 XPCOM 指针：

这个单例对象将向任何与其注册的观察者对象广播，无论该观察者的来源窗口。列表 6.12 显示了一个典型的用法。

+   列表 6.12 XPCOM 广播-观察者示例。

```
var observer = { ... 见列表 6-6 ... };
var observer2 = { ... 另一个观察者 ... };
var CC = Components.classes, CI = Components.interfaces;
var cls, caster;
cls = CC(@mozilla.org/observer-service;1*);
caster = cls.getService(CI.nsIObserverService);
caster.addObserver(observer, "my-event", true);
caster.addObserver(observer2, "my-event", true);
```

以上就是对 Mozilla 广播者和观察者的介绍。

## 6.1.5 命令

本章提到的第四种事件系统与命令有关。在 Mozilla 中，命令是一个可能执行的操作。HTMLs

链接导航和表单提交大致等同于 Mozilla 命令实现的任务。

虽然认为命令最简单的方法是将其视为单个 JavaScript 函数，但这远非唯一的方法。命令也可以是从一个地方到另一个地方的消息传递。Mozilla 命令的这一方面具有类似事件的特征。在基础系统之上还有另一组类似事件的行为。当命令状态改变时，会发送更改通知。

总的来说，Mozilla 的命令系统非常复杂。第 9 章“命令”不仅在整个 XUL 窗口的上下文中检查了这一点，还涵盖了它的核心组成部分。目前，请注意 Mozilla 的命令系统是 DOM 3 处理模型的扩展或补充。

## 6.1.6 内容分发事件

本章考虑的最后一个 Mozilla 输入系统是内容分发系统。该系统负责接收 URL 并返回文档，或发送电子邮件。它是一个具有多种用途的通用系统。

DOM 事件、定时事件和观察者事件处理的都是极小的信息片段。发生的事件可能代表 Mozilla Firefox 中其他地方某些较大的处理过程，但数据本身通常很小。你可以称这些事件为轻量级事件。

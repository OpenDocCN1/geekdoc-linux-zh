
```javascript
function update() {
  var cont, node;
  cont = document.dispatcher.getControllerForCommand('paste');
  node = document.getElementById('paste');

  if (!cont || !node) return;

  if (cont.isEnabled(cmd)) {
    node.removeAttribute("disabled");
    node.removeAttribute("value");
  } else {
    node.setAttribute("disabled", true);
    node.setAttribute("value", "Paste Disabled");
  }

  if (cont.clipboardEmpty()) {
    node.setAttribute("value", "Nothing to Paste");
  }
}
```

此函数绑定到某些命令：它只知道“粘贴”命令。它寻找命令的实现，然后使用 `isEnabled()` 和 `clipboardEmpty()` 对其进行检查。`isEnabled()` 是控制器的标准，但此控制器必须具备额外功能，因为 `clipboardEmpty()` 是新的。这个特定命令有两个状态：它是否被启用，以及剪贴板中是否有内容。如果剪贴板为空，则没有内容可粘贴。

基于对这些状态的分析，`update()` 函数使用 XUL 属性加载 `<command>` 标签。这些属性对 `<command>` 来说都没有意义。将它们放在那里是为了观察 `<command>` 标签的小部件可以获取它们。两个 `button` 标签都获取了 `disabled` 和 `value` 属性，但 `disabled` 仅对 `<button>` 有特殊意义，而 `value` 只对 `<description>` 有意义。

结果是小部件标签被更新，它们的外观发生了变化。这一切都是为了响应调度器的 `UpdateCommands()` 方法的调用，该方法启动了通知/命令更新过程。

注意，这个示例中有两个广播-观察者（broadcaster-observer）系统在工作。第一个是将 `<updater>` 自动注册为调度器的命令更新器。第二个是在两个小部件标签上应用特定的 `observes` 属性。第二个系统仅仅是一种设计选择；同样也可以从 `update()` 方法直接更新小部件，也许使用 `id` 或实际上是任何其他方法。

## 9.6 命令与 XPCOM 组件

虽然函数和控制器可以完全用 JavaScript 创建，但 XPCOM 元素也存在。函数、控制器和调度器的简单组合也可以通过多种方式进行增强。这些增强允许动态地从控制器添加或删除命令实现。它们还允许与给定的命令关联额外信息。对于命令系统的普通使用，这些增强的名称是必需的。

如果考虑到这些，Mozilla 拥有足够相关的 XPCOM 对象和接口让你目不暇接。一种拼接和关键词的命名策略并没有帮助；相反，它倾向于让不同的接口融合在一起，直到它们看起来非常相似。

唯一的方法是尝试对每个接口进行特征描述，直到它脱颖而出。这就是这里采用的策略。表 9.1 基于 Mozilla 1.4。请注意，这些接口中的几个在该版本中并不是“冻结”的；它们可能会有重大变化。

### 表 9.1 贡献于命令系统的 XPCOM 组件

| 接口名称 | 现有 XPCOM 实现 | 用 |
|---|---|---|
| `nsCommand` | | 尽管这是一个逻辑名称，但不存在此类接口 |
| `nsCommandHandler` | `@mozilla.org/embedding/` | 最低级命令实现——不供 JavaScript 使用。 |
| `nsCommandHandlerHandler` | `@mozilla.org/embedding/` | 初始化 `nsCommandHandler` 对象。 |
| `nsController` | `@mozilla.org/embedding/` | 基础控制器，支持命令表。 |

### 表 9.1 贡献于命令系统的 XPCOM 组件（续）

| 接口名称 | 脚本可用？ | 现有 XPCOM 实现 | 用 |
|---|---|---|---|
| `nsIControllerContext` | | `@mozilla.org/embedding/` | 初始化控制器。 |
| `nsIController-CommandTable` | | `@mozilla.org/embedding/` | 可变的命令集合。 |
| `nsICommandController` | | `@mozilla.org/embedding/` | 部分规范化的接口，为基础控制器增加了参数化的命令调用（带参数）。 |
| `nsIController-CommandGroup` | | `@mozilla.org/embedding/` | 一个可变的命令集合，用于为一组命令赋予标识性。 |
| `nsIControllerCommand` | ✓ | 无 | 基础函数对象（functor）。 |
| `nsICommandManager` | | `@mozilla.org/embedding/` | 暴露控制器的中间功能。 |
| `nsICommandParams` | | `@mozilla.org/embedding/` | 用于命令执行的参数列表数据结构。 |
| `nsIControllers` | ✓ | 无 | DOM 元素的属性控制器集合。 |
| `nsIDOMXULCommandDispatcher` | ✓ | 调度器不是 XPCOM 组件。 | XUL 命令调度器。 |
| `nsPICommandUpdater` | | | 应用程序无处使用的内部接口 |
| `nsISelectionController` | ✓ | | 与命令分发完全无关 |
| `nsIEditorController` | | `@mozilla.org/editor/` | Mozilla Composer 工具使用了两个控制器。 |
| `nsITTransaction` | ✓ | `@mozilla.org/embedding/` | 当控制器变得复杂时三个三个接口。使用这些数据结构来实现撤销/重做、宏、历史、审计和其他高级控制器功能。 |
| `nsITTransactionList` | | | |
| `nsITTransaction-Manager` | | | |

同时也存在用于实现命令行语法的若干接口；它们可用于启动平台窗口。这些接口与命令传递系统毫无关系。

## 9.7 现有命令

到为止，这些讨论涵盖了 Mozilla 平台中命令的 XUL、AOM 和 XPCOM Aspect。然而，Mozilla 既是一个完整的应用程序（Classic Mozilla），也是一个平台。平台提供了一些应用程序命令。应用程序程序员有时会重用或利用这些特性。有很多机会可以这样做。

焦点控制器（focus controller）是重用技术的一个简单示例。该控制器在 XUL 窗口中始终可用。命令分发器会在 `afterFocus()` 和 `rewind()` 方法后改变，这些方法激活了用户常用的 Tab 导航。这些方法将命令发送给焦点控制器。控制器还可以用于命令提示。命令更新器（Command updater）可以接收来自焦点控制器的事件大量通知。目前还不清楚为什么控制器每次通过焦点环导航时都会发送 `commandupdateevent`。

另一种风险是冲突。chrome 文件工具包中的 `globalOverlay.js` 包含了管理命令和控制器的处理程序。Messenger 地址栏使用的命令架构以及编写器（Composer）使用的三轮廓系统足以作为指南。某些键盘命令绑定足够模块化，以至于你可以重用持有它们的叠加文件。

除外，重用现有的 Mozilla 命令要难实现一些。但有一种特殊情况可以进行大量的重用。

Classic Mozilla 的 Commander、Messenger 和 Navigator 工具实现了许多细微的用户操作，这些操作必须由命令处理，因为即使是微小的操作也会对用户界面产生更改。这意味着从微小的（例如“选择当前单词”）到普通的（例如“删除消息”），再到实质性的（例如“加载 URL”），一切必须在 Web 应用程序套件内部有实现。其中许多命令在 C++ 中高效实现，许多直接在 chrome 中通过 JavaScript 提供。

如果你的应用程序与 Classic Mozilla 的目的相似（可能是另一个浏览器变体），那么这些命令就可以重用。如果你的目标是深度定制现有的 Mozilla 应用程序，那么熟悉这些命令至关重要。如果你的应用程序是浏览器的插件，避免与现有命令名称冲突也很重要。遗憾的是，这些名称并不是集中的。这部分部分是因为程序员处理的是 Classic 套件的不同部分。Classic Mozilla 确实尝试对多个应用程序中用途相同的命令使用相同的名称。

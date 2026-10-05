

# 第 18 章 · SDK

在 API 4.0 中，显然使用统一的命名方法被认为更为明智，因此开发者在 `ManagedEntity` 对象上创建了一个 `Rename_Task` 方法。由于大多数重要的托管对象都派自此 `ManagedEntity` 对象，因此它们都继承了这一统一的 `Rename_Task` 方法。

## 为什么我们在这个方法上要有这个 _TASK 后缀？

要理解这一点，你必须知道大多数 API 方法都是异步运行的。当你调用该方法时，你的脚本会在方法调用后立即继续运行。这是为了适应可能会阻塞你的应用程序或脚本的长时间运行的任务。为了让你跟进执行进度或等待所调用的 API 方法完成，大多数异步方法都会返回一个指向 `Task` 对象的引用。通过该 `Task` 对象的帮助，你可以检查方法的执行进度并发现它是否成功完成。在本章末尾的“善用某些技巧和窍门”中，有两个代码片段展示了你如何在脚本中进行操作。

回到上一节中统一的 `Rename_Task` 方法，PowerCLI 开发团队试图让 PowerCLI 用户的生活变得更简单。他们还为 vSphere API 中存在的所有异步方法在托管对象绑定中引入了同步方法。这就是为什么我们有了 `Rename` 方法以及你之前看到的 `Rename`。此外，`RenameDatastore` 方法已弃用，但（目前）仍然可用。

```
$ds Get-Member -MemberType Method | Where Name -like "rename*"
```

| 名称 | 方法 | 定义 |
|---|---|---|
| Rename | void | Rename(string newName) |
| RenameDatastore | void | RenameDatastore(string newName) |
| Rename_Task | VMware.Vim.ManagedObjectReference | Rename_Task... |

以下代码使用了来自 `Datastore` 托管对象的同步 `Rename` 方法。只有当实际重命名完成后，命令行提示符才会返回。不要忘记，`Rename` 方法并不是你在 vSphere API 参考文档中能找到的方法。该方法是由 PowerCLI 开发团队添加到 .NET Framework 中的，以便为你提供一个异步方法的同步版本。

```
[vSphere PowerCLI] C:\> Rename("DS22")
[vSphere PowerCLI] C:\>
```

让我们验证重命名是否执行正确：

```
$ds.Name
```

DS1 看起来方法调用没有起作用！请放心，方法调用确实生效了。你只需要记住，你正在使用的是存在于 vSphere 服务器上的实际对象的客户端副本。

检查名称更改是否实际发生的一种方法是像这样获取一个 `Datastore` 托管对象的最新副本：

```
$ds = Get-Datastore -Name DS22 | Get-View
$ds.Name
```

DS22

另一种验证数据存储重命名是否已完成的方法是刷新你所持副本的一部分。要做到这一点，需要使用 PowerCLI 开发团队添加到托管对象中的 `UpdateView` 方法。`UpdateView` 允许你刷新整个托管对象或对象的特定属性。如果属性本身是一个复杂的数据对象，那么指定你想要刷新的属性可以节省大量时间。如果你需要刷新成千上个托管对象副本的属性，将节省更多时间！

```
$ds.UpdateView("Name")
$ds.Name
```

DS22

# 使用 vSphere 管理器

托管对象的另一类主要类型是服务管理器（service managers）。服务管理器是在虚拟环境中提供服务的特殊对象。此类服务的示例包括 `EventManager`、`LicenseManager` 和 `PerfManager`。要要访问服务管理器，请从 `ServiceInstance` 托管对象开始，它是清单的根对象。在 `Content` 属性中，你会找到大多数服务管理器的 `MoRef`：

Get-View ServiceInstance

```
ServerClock : 4/28/2015 3:00:42 PM
Capability : 4/28/2015 3:00:42 PM
Content : 4/28/2015 3:00:42 PM
Datastore : 4/28/2015 3:00:42 PM
EventManager : 4/28/2015 3:00:42 PM
Extension : 4/28/2015 3:00:42 PM
Folder : 4/28/2015 3:00:42 PM
HostManager : 4/28/2015 3:00:42 PM
LicenseManager : 4/28/2015 3:00:42 PM
PerfManager : 4/28/2015 3:00:42 PM
SessionManager : 4/28/2015 3:00:42 PM
```

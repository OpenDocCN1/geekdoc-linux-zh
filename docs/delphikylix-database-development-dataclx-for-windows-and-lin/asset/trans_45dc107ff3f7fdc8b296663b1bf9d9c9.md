

```pascal
procedure TForm1.cdsContactsBeforeGetRecords(Sender: TObject);
var
  OwnerData: OleVariant;
begin
  if cdsContacts.Active then
    OwnerData := cdsContacts.Tag;
end;
```

无状态应用程序示例将这些概念整合到无状态服务器和客户端中。由于大部分源代码之前已以代码片段的形式列出，这里不再重复展示。

## 在多个客户端数据集之间共享连接

某些实际应用程序允许用户选择连接协议；例如，用户可以选择套接字连接、DCOM 连接或 HTTP 连接。通过这种方式，客户端应用程序让用户决定哪种连接类型最适合特定情况。

为了支持多种连接类型，你需要在客户端的数据模块上放置多个连接组件。例如，你可以将 `TSocketConnection`、`TDCOMConnection` 和 `TWebConnection` 组件拖放到数据模块上。从一种连接切换到另一种连接意味着你需要在运行时将每个 `TClientDataSet` 组件的 `RemoteServer` 属性设置为正确的连接。

在小型示例应用程序中，这不是一个大问题，因为大多数示例仅使用一个或两个客户端数据集。然而，大多数实际应用程序包含的组件数量远不止这些。例如，我目前正在开发一个应用程序，该客户端应用程序中使用了 50 多个 `TClientDataSet` 组件。

为了方便在连接组件之间切换，Delphi 提供了 `TConnectionBroker` 组件。要使用 `TConnectionBroker`，请将其拖放到客户端的数据模块上，并将每个 `TClientDataSet` 组件的 `ConnectionBroker` 属性设置为该 `TConnectionBroker`。然后，将 `TConnectionBroker` 的 `RemoteServer` 属性设置为正确的连接组件。此时，切换连接只需更改连接代理的 `RemoteServer` 属性为所需的连接组件即可，非常简单。

除了轻松地在连接之间切换之外，使用连接代理还有另一个优势。如果你在代码中对应用程序服务器进行调用，例如以下代码：

```pascal
SocketConnection1.AppServer.ExecuteSomeMethod;
```

如果连接类型发生变化，你无需更改这段代码。相反，你可以通过连接代理调用该方法，而不是在 `SocketConnection1`（或任何其他连接组件）上调用，例如：

```pascal
ConnectionBroker1.Connection.AppServer.ExecuteSomeMethod;
```

这样，无论当前活动的连接是什么，代码都能正常工作。

### 在多个服务器之间代理连接

在大规模开发中，单个应用程序服务器实例可能不足以处理大量连接客户端。你可能也希望在多台服务器机器上运行应用程序服务器的副本，这样如果一台机器宕机，客户端仍然可以连接到运行在另一台服务器机器上的应用程序服务器。

当运行多个应用程序服务器副本时，客户端需要在运行时在它们之间进行选择。如果它选择了一个当前宕机的服务器，它应该尝试使用不同的服务器再次连接。

为了将连接代理集成到你的应用程序中，请将 `TSimpleObjectBroker` 组件拖放到客户端的数据模块上。在 `Servers` 属性中，输入客户端应用程序可以尝试连接的服务器列表。将连接对象的 `ObjectBroker` 属性设置为 `TSimpleObjectBroker` 的名称。

当 `TSimpleObjectBroker` 的 `LoadBalanced` 属性设置为 `False` 时，客户端将尝试连接 `Servers` 属性中的第一个服务器。如果该连接失败，它将尝试第二个服务器，依此类推。当 `LoadBalanced` 为 `True` 时，代理仅尝试为当前客户端应用程序中的每个连接选择不同的服务器。如果客户端应用程序只包含一个远程连接，设置 `LoadBalanced` 为 `True` 没有效果。

更常见的场景是运行多个应用程序服务器实例，并有若干客户端连接到服务器。在这种情况下，你最好在运行时随机化服务器列表，这样每个客户端都有可能连接到不同的服务器。

例如，假设你有三个服务器，分别命名为 Server1、Server2 和 Server3。如果有六个客户端应用程序实例，并且你为每个客户端随机化服务器的顺序，那么每个客户端的服务器顺序可能是这样的：

- 客户端 1：Server1, Server2, Server3
- 客户端 2：Server1, Server3, Server2
- 客户端 3：Server2, Server1, Server3
- 客户端 4：Server2, Server3, Server1
- 客户端 5：Server3, Server1, Server2
- 客户端 6：Server3, Server2, Server1

假设所有服务器都正常运行，这将使负载在三个服务器上平均分配，每个服务器连接两个客户端。

## 总结

本章讨论了 DataSnap，这是 Delphi 用于多用户数据库开发的远程访问技术。

- 创建独立应用程序服务器的第一步是设置一个或多个远程数据模块。Delphi 支持创建标准、MTS、CORBA 和 SOAP 远程数据模块。
- 要为应用程序服务器创建方法，请使用“添加到接口”菜单项。要创建回调接口，请使用类型库编辑器创建新接口。
- 要为应用程序服务器创建简单的用户界面，每当创建或销毁远程数据模块时，向主窗体发送自定义消息。执行此操作的一个合理位置是数据模块的 `OnCreate` 和 `OnDestroy` 事件处理程序中。
- 你可以从客户端应用程序连接到应用程序服务器，使用多种连接协议，包括 `TSocketConnection`、`TDCOMConnection`、`TWebConnection`、`TSOAPConnection` 和 `TCORBAConnection`。
- 公文包模式允许你的应用程序在无法连接到服务器时，将数据下载到本地机器供离线使用。
- 为了方便在大型应用程序中使用多个应用程序服务器，Delphi 提供了 `TConnectionBroker` 组件。

下一章将介绍一个完整的应用程序，该应用程序使用了本章以及全书其他部分讨论的许多技术。

# ConMan 应用程序

第 9 章

### 本章内容

- 什么是 ConMan？ 348
- 数据库结构 349
- 代码概述 352
- 服务器应用程序 352
- 客户端应用程序 358
- 改进空间 373

在这本书中，我讨论了许多在 Delphi 和 Kylix 中编写数据库应用程序的技术。在此过程中，我展示了若干小型示例应用程序，以巩固每章讨论的许多重要要点。

在本章中，我将展示一个完整的多用户数据库应用程序，该应用程序结合了书中讨论的许多理念。该应用程序名为 ConMan（Contact Manager，即联系人管理器的简称）。

## 什么是 ConMan？

ConMan 是一个相当简单的联系人管理器，可用于记住重要客户、朋友和家人的姓名、地址和电话号码。你还可以为每个联系人输入备注并存储提醒事项。

多个用户可以同时运行此应用程序，并且应用程序中的设置允许用户将数据库存储到本地机器上，以便在远离办公室时使用（公文包模式）。

尽管 ConMan 演示了许多重要的多用户数据库概念，但它并不会很快取代你生产级的联系人管理器（如 ACT! 或 GoldMine）。ConMan 缺少许多商业联系人管理器的功能，包括拨打电话号码、使用你喜欢的文字处理器自动书写信函、传真和备忘录等。ConMan 的目的不是编写一个可销售的产品。毕竟，如果真是那样，我就不会在数据库书籍中免费提供源代码了。其目的反而是展示一个利用重要 Delphi 数据库技术的实际应用，让你对如何在自己的应用程序中利用相同技术有一个具体的理解。

图 9.1 显示了运行时 ConMan 的界面。

由于 ConMan 利用了 Kylix 尚未支持的技术——如 DataSnap——因此仅作为 VCL 应用程序提供。



## 在多个客户端数据集之间共享连接

```
procedure TForm1.cdsContactsBeforeGetRecords(Sender: TObject; var OwnerData: OleVariant); begin if cdsContacts.Active then OwnerData := cdsContacts.Tag; end;
```

无状态应用程序示例将这些概念整合到一个无状态服务器和客户端中。由于大部分源代码之前已经以代码片段的 形式列出，这里就不再重复展示了。

一些实际的应用程序允许用户在连接协议之间进行选择；例如，用户可以选择套接字连接、DCOM 连接或 HTTP 连接。通过这种方式，客户端应用程序让用户决定哪种连接类型最适合特定情况。

为了支持多种连接类型，您需要在客户端的数据模块上放置多个连接组件。例如，您可以在数据模块上放置一个 TSocketConnection、一个 TDCOMConnection 和一个 TWebConnection 组件。从一种连接切换到另一种连接意味着您需要在运行时将每个 TClientDataSet 组件的 RemoteServer 属性设置为正确的连接。

在小的示例应用程序中，这不是一个大问题，因为大多数示例仅使用一个或两个客户端数据集。然而，大多数实际应用包含的数量远不止于此。例如，我目前正在开发一个在客户端应用程序中使用了超过 50 个 TClientDataSet 组件的应用程序。

为了便于从一个连接组件切换到另一个，Delphi 提供了 TConnectionBroker 组件。要使用 TConnectionBroker，请在客户端的数据模块上放置一个，并将每个 TClientDataSet 组件的 ConnectionBroker 属性设置为该 TConnectionBroker。然后，将 TConnectionBroker 的 RemoteServer 属性设置为正确的连接组件。切换连接就变成了一个简单的任务，只需将连接代理的 RemoteServer 属性更改为所需的连接组件即可。

除了能够轻松地在连接之间切换外，使用连接代理还有一个优势。如果您在代码中对应用程序服务器进行调用，例如以下代码：

```
SocketConnection1.AppServer. ExecuteSomeMethod;
```

如果连接类型发生变化，您不需要更改该代码。相反于在 `SocketConnection`（或任何其他连接组件）上调用方法，您可以在连接代理上调用，如下所示：

```
ConnectionBroker1.Connection.AppServer.ExecuteSomeMethod;
```

这样，无论活动连接是什么，代码都能正常工作。

### 在多个服务器之间代理连接

在大规模开发中，单个应用程序服务器实例可能不足以处理连接到它的大量客户端。您可能还希望在多台服务器机器上运行应用程序服务器的副本，以便当一台机器宕机时，客户端仍然可以连接到运行在另一台服务器机器上的应用程序服务器。

在运行多个应用程序服务器副本时，客户端需要在运行时选择其中一个的方式。如果它选择的服务器当前已宕机，它应该尝试使用另一个服务器。

为了在您的应用程序中整合连接代理，请将一个 `TSimpleObjectBroker` 组件放置到客户端的数据模块上。在 `Servers` 属性中，输入客户端应用程序可以尝试连接的服务器列表。将连接对象的 `ObjectBroker` 属性设置为 `TSimpleObjectBroker` 的名称。

当 `TSimpleObjectBroker` 的 `LoadBalanced` 属性设置为 `False` 时，客户端将尝试连接到 `Servers` 属性中的第一个服务器。如果该连接失败，它将尝试第二个服务器，依此类推。当 `LoadBalanced` 为 `True` 时，该代理仅尝试为当前客户端应用程序中的每个连接选择不同的服务器。如果客户端应用程序只包含一个远程连接，将 `LoadBalanced` 设置为 `True` 将不起作用。

更常见的场景是运行多个应用程序服务器实例，并有多个客户端连接到服务器。在这种情况下，您最好的选择是在运行时随机化服务器列表，以便每个客户端都有潜力连接到不同的服务器。

例如，假设您有三个服务器，分别命名为 Server1、Server2 和 Server3。如果有六个客户端应用程序实例，并且您为每个客户端随机化服务器的顺序，那么每个客户端的服务器顺序可能是：

- 客户端 1：Server1, Server2, Server3
- 客户端 2：Server1, Server3, Server2
- 客户端 3：Server2, Server1, Server3
- 客户端 4：Server2, Server3, Server1
- 客户端 5：Server3, Server1, Server2
- 客户端 6：Server3, Server2, Server1

假设所有服务器都在运行，这将使负载在三个服务器上均匀分布，每个服务器连接两个客户端。

## 摘要

本章讨论了 DataSnap，即 Delphi 用于多层数据库开发的远程访问技术。

- 创建独立应用程序服务器的第一步是设置一个或多个远程数据模块。Delphi 支持创建标准、MTS、CORBA 和 SOAP 远程数据模块。
- 要创建用于应用程序服务器方法，请使用“添加到接口”菜单项。要创建回调接口，请使用类型库编辑器创建一个新的接口。
- 要为应用程序服务器创建简单的用户界面，每当创建或销毁远程数据模块时，向主窗体发送一条自定义消息。在数据模块的 **OnCreate** 和 **OnDestroy** 事件处理程序中执行此操作是一个合理的选择。
- 您可以使用多种连接协议从客户端应用程序连接到应用程序服务器，包括 TSocketConnection、TDCOMConnection、TWebConnection、TSOAPConnection 和 TCORBAConnection。
- 公文包模型允许您的应用程序将数据下载到本地机器，以便在无法连接到服务器时使用。
- 为了方便在大型应用程序中使用多个应用程序服务器，Delphi 提供了 TConnectionBroker 组件。

下一章介绍一个完整的应用程序，该应用程序使用了本章以及本书其余部分讨论的许多技术。

# ConMan 应用程序

第 9 章

## 本章内容

- 什么是 ConMan？ 348
- 数据库结构 349
- 代码概览 352
- 服务器应用程序 352
- 客户端应用程序 358
- 改进空间 373

在本书中，我讨论了许多在 Delphi 和 Kylix 中编写数据库应用程序的技术。在此期间，我展示了许多小型示例应用程序，以巩固每章讨论的许多重要要点。

在本章中，我将展示一个完整的多用户数据库应用程序，其中包含本书讨论的许多思想。该应用程序名为 ConMan（Contact Manager 的缩写）。

## 什么是 ConMan？

ConMan 是一个相当简单的联系人管理器，可用于记住重要客户、朋友和家人的姓名、地址和电话号码。您还可以为每个联系人输入备注并存储提醒。

多个用户可以同时运行此应用程序，并且该应用程序中的条款允许用户将数据库存储到本地机器上，以便在离开办公室时使用（公文包模型）。

虽然 ConMan 展示了许多重要的多用户数据库概念，但它不会很快取代您生产级别的联系人管理器（如 ACT! 或 GoldMine）。ConMan 缺少商业联系人管理器的许多重要功能，包括拨号、自动使用您喜欢的文字处理器写信、传真和备忘录等。ConMan 的目的不是要编写一个可销售的产品。毕竟，如果真是那样，我也不会免费在数据库书中提供源代码。其目的是展示一个利用重要的 Delphi 数据库技术的真实应用程序，让您对如何在自己的应用程序中利用相同的技术有具体的理解。

图 9.1 显示了 ConMan 的运行状态。

由于 ConMan 利用了 Kylix 尚不支持的技术——如 DataSnap——因此仅作为 VCL 应用程序呈现。


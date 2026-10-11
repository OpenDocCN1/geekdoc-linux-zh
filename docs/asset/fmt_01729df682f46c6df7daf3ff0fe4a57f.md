
接下来，我们需要构建一个服务器应用程序来托管服务端对象（servant object）。在大型企业应用中，单个服务器模块可以托管多个服务对象。在 Java 术语中，这就是包含 `main()` 方法的模块。除了正常的业务逻辑外，服务器模块应该执行以下一组任务来托管这些对象。这里给出了任务的简要概述，随后将是一个详细的示例应用程序。图 7.6 也描绘了这一系列任务，为了方便读者阅读，此地列出的步骤与图中的任务编号相关。乍一看，这似乎是一长长的任务列表；然而，这是激活任何 CORBA 服务对象的一组非常标准化的任务，因此可以在自定义服务器模块中实现自动化。

![](img/1c052d580a194876cd94f43b32c39cf4_427_0.png)

图 7.6 实例化 CORBA 服务对象的涉及步骤顺序。

- 创建 ORB 的初始实例（图中的第 1 步），执行 `init()` 方法并将命令行参数和 ORB 属性对象作为参数传递。ORB 属性可能用于指定特定的 ORB 实现。例如，如果要使用 Borland VisisBroker ORB，则应正确设置属性。默认情况下可以实例化 JDK 的 ORB 实现，在这种情况下 `init()` 方法的第二个参数可以为 `null`。创建初始 ORB 实例是整个过程的起点，其他 CORBA 框架对象将根据此 ORB 初始化（或设置）。

- 获取根 POA 对象的引用（图中第 2 步的第一部分）。CORBA 服务器应用程序应该拥有一个根 POA 对象，以便以树形结构创建进一步的子 POA。通过在 ORB 对象上调用 `resolve_initial_references()` 方法并将 `RootPOA` 作为字符串参数传递来实现。

- 将根 POA 对象与 ORB 对象关联（图中第 2 步的第二部分）。此步骤建立了 ORB 和 POA 之间的链接。

- 创建子 POA 对象（图中的第 3 步）。POA 对象支持定义策略，以更好地控制对象的激活和生命周期等。然而，根 POA 是使用默认策略创建的，这些策略无法更改。可以根据所需的策略创建子 POA 对象。每个 POA 对象都与一个 POA 管理器（POA manager）关联。在创建子 POA 时，如果我们希望将新的子 POA 与现有的 POA 管理器关联，可以将现有的 POA 管理器作为方法调用的参数之一。如果对此参数传递 `null` 值，则会自动创建一个新的 POA 管理器并与新的子 POA 对象关联。为了演示，图中显示了多个子 POA——每个服务对象对应一个；然而，这一概念可以扩展到任意数量的服务对象。此外，并不总是需要创建子 POA 来控制服务对象；但根 POA 是用默认策略创建的，无法更改。

- 激活与子 POA 对象关联的 POA 管理器（图中第 4 步），该管理器管理一个或多个 POA 的处理状态。当 POA 创建时，关联的 POA 管理器处于 `HOLD` 状态，这意味着对服务对象的所有方法调用都在队列中。因此，必须通过在 POA 管理器上执行 `activate()` 方法来激活该管理器。

- 创建服务对象并将其注册到 ORB（图中的第 5 步）。这可以通过将 ORB 引用作为参数传递给服务对象的构造函数来实现。

- 通过在 ORB 对象上执行 `resolve_initial_references()` 方法并将 `NameService` 作为字符串参数传递，创建根命名上下文对象（图中的第 6 步）。

- 从根命名上下文通过在 `NamingContextHelper` 对象上执行静态的 `narrow()` 方法并将根命名上下文对象作为参数，获取 `NamingContext` 引用（图中第 7 步）。`NamingContext` 是 `NamingContext` 接口的扩展，接受基于 URL 的名称用于绑定和解析。

- 通过在 POA 上执行 `servant_to_reference()` 方法，通过子 POA 获取对象引用（服务对象）（图中第 8 步）。在服务的辅助类上执行 `narrow()` 方法以获取服务引用。

- 将服务对象绑定到命名上下文（图中第 9 步）。这是最后一步，允许客户端模块找到服务对象。

## 构建分布式 Java 应用

### 实现 CORBA 客户端

在初步尝试理解 CORBA 客户端和服务器开发涉及的完整事件周期后，现在值得花时间过构建一个运行的示例应用程序的过程。该示例以两种方式呈现：第一个整个应用程序是使用 JDK 1.4.1 附的标准 Java 类库构建的，然后通过 Borland JBuilder 和 Borland Visis 开发环境重新构建该程序。由于两者都是 Borland 的产品，因此使用它们一起构建示例是自然而然的。

### JDK 1.4.1 中构建示例

示例应用程序托管了一个 CORBA 服务对象，该对象作为客户端模块维护客户名称。每个客户都关联一个编号（称为 `CustID`），该编号是随机生成的。客户编号和关联名称内部存储在 `java.util.Properties` 对象中。支持接口定义了两个方法：`AddCustomer()` 和...

# 416 企业级 Linux 应用开发

`GetCustomer()`。第一个方法将客户名称作为字符串对象发送，并获取新创建的客户编号作为返回值。第二个方法将客户编号作为整数值发送，并获取关联的客户名称作为返回值。IDL 定义如列表 7.14 所示，该文件可在附带的 CD-ROM 上找到。

## 列表 7.14 Customer.idl

```idl
module CustService {
    interface Customer {
        long AddCustomer(in string CustName);
        string GetCustomer(in long CustId);
    };
}
```

使用以下命令行编译此 IDL 文件，其中 `idlj` 是 Java 的 IDL 编译器，是 JDK 1.4.1 的一部分。

```bash
$ idlj -fail CustService.idl
```

成功执行上述命令将产生以下一组文件。由于 IDL 接口定义在 IDL 模块定义中，因此 IDL 模块被映射到 Java 包中，这些文件会自动创建在当前主目录的 `CustService` 子目录中。为了节省空间，此处未提供这些文件的内容列表；但可以在 CD-ROM 上与其它项目源文件一起查看。

- `CustomerOperations.java`
- `Customer.java`
- `CustomerStub.java`
- `CustomerHelper.java`
- `CustomerHolder.java`
- `CustomerPOA.java`

从当前目录开始，使用 `javac` 编译器和以下命令行编译这些程序。

```bash
$ javac CustService/*.java
```

下一步是实现 servant 对象以及服务器和模块。为了方便起见，这些程序也位于相同的子目录下，属于同一个包。`CustomerImpl.java` 程序通过扩展 `CustomerPOA` 骨架文件来实现 servant 对象，如列表 7.15 所示；而实例化该对象的服务器模块显示在列表 7.16 中。这些列表可在附带的 CD-ROM 上。

## 列表 7.15 CustomerImpl.java

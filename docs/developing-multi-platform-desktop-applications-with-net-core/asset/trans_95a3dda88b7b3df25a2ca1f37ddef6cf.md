
http://docs.microsoft.com/en-us/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert

请注意，这些验证类型之间的选择将决定你的单元测试代码在检查方法时是否相关。如果你没有为验证选择合适的断言，测试可能毫无用处，甚至更糟的是，无法检查代码的有效性。

当 ASSERT 方法未通过验证时，会抛出异常（ASSERT 异常），并且测试将标记为“失败”。

### 7.1.2.3 执行单元测试

为了执行单元测试项目，你需要使用如下所示的“测试资源管理器”窗口：

![](img/3d310cc066dda6e2dfa67a650614076f_121_0.png)

*(测试资源管理器)*

你可以使用“全部运行”菜单一次性运行项目的所有测试，或者通过选中特定测试并使用右键菜单中的“运行”选项来运行单个测试。

### 7.1.2.4 查看测试结果

测试结果可以在“测试资源管理器”窗口中看到，绿色对勾表示测试有效，红色叉号表示测试失败，如下所示。

![](img/3d310cc066dda6e2dfa67a650614076f_122_0.png)

MSTest 为你的项目中实现单元测试提供了解决方案，因为它作为 Visual Studio 的原生组件，能与 Microsoft 的 IDE 完美集成。Microsoft 团队对其文档记录非常完善。参考文献和教程可以通过参考中的链接找到。

http://docs.microsoft.com/visualstudio/test

### 7.1.3 Mock 概念

定义相关单元测试的问题在于开发者的上下文：当编写单元测试项目时，许多对象尚未定义或数据库尚不可用。这可能是一个问题，因为开发者需要用尽可能大的输入数据面板来测试方法，覆盖尽可能多的情况（理论上）。

解决方法是使用模拟对象或数据库来模拟与开发者需要单元测试的功能进行交互的真实数据或对象。

这个概念称为 Mocking（模拟）。模拟对象隔离了你想要测试的方法/函数，并验证其是否独立运行（不依赖于其他方法）。模拟对象可以设置具有给定值的对象，并设置该对象的属性。

开发者必须硬编码方法所需的输入值，并定义一个验证测试，其中包含期望的结果值（同样需要硬编码）。

对于 .NET Core 3 开发，我们推荐使用 Moq (4.x)，这是最受欢迎且用户友好的模拟框架。Moq 是一个使开发和测试模拟对象变得简单的库，此外，该库提供了 LINQ to Mocks 功能，允许动态请求模拟对象用于验证。它支持模拟接口和类。

![](img/3d310cc066dda6e2dfa67a650614076f_123_0.png)

- https://github.com/moq/moq4/
- https://github.com/moq/moq4/wiki/Quickstart

你可以将以下包添加到测试项目中，以快速集成 Moq。

![](img/3d310cc066dda6e2dfa67a650614076f_123_1.png)

Moq

该包的最新版本基于 .NET Standard 2.0 实现，因此可用于 .NET Core 3 项目（这正是 .NET Standard 库格式的优点）。

下面是一个代码片段，向你展示如何在简单用例中使用 **Moq**。

```csharp
[TestFixture]
public class FooTest:
{
    Foo subject;
    Mock myInterfaceMock;

    [SetUp]
    public void SetUp()
    {
        myInterfaceMock = new Mock();
        subject = new Foo();
    }

    [Test]
    public void DoWorkTest()
    {
        // Set up the mock
        myInterfaceMock.Setup(m =>
            m.DoesSomething()).Returns(true);
        myInterfaceMock.SetupGet(m =>
            m.Name).Returns("Wolly");

        var result = subject.DoWork();

        // Verify that DoesSomething was called only
        // once
        myInterfaceMock.Verify(m =>
            m.DoesSomething(), Times.Once());

        // Verify that DoesSomething was never called
        myInterfaceMock.Verify(m =>
            m.DoesSomething(), Times.Never());
    }
}
```

正如你所见，Moq 的使用非常简单，即使是初级开发者也能轻松上手：

- 声明模拟对象：定义你想要模拟的对象类型。
- 配置模拟对象：为方法（即被模拟的对象）定义值。
- 验证模拟对象：验证模拟对象是否被调用（或未调用）。

Moq 拥有直观易懂的 API，不需要预先了解模拟知识。

还有其他几个库允许在单元测试阶段模拟对象，你可以深入了解 NSubstitute 和 FakeItEasy，以获取市场上模拟库的更广泛视野（它们是开源的）。这两个库提供了与之前描述的 Moq 库等效的功能（除了 LINQ 能力）。

你可以查阅它们各自 GitHub 仓库上的 wiki 以获取更多信息。

![](img/3d310cc066dda6e2dfa67a650614076f_125_0.png)

## 7.2 功能测试

功能测试和集成测试包括对每个应用程序功能的测试。换句话说，就是验证组装好的应用程序是否提供了预期的结果和功能。这可以通过选择特定的数据样本或配置集来实现。

这些测试可能包括：

- 使用关键值的测试。
- 边界测试。
- 域外测试。

功能测试是一种黑盒测试类型，因为它需要完成整个软件开发过程才能执行。测试人员通过使用多个场景和用例，验证所得软件与产品规格的一致性。

## 第 8 章 多平台开发解决方案

如果你想开始一个多平台项目，这可能是本书中最有用的章节。我们将通过详细回顾几个示例项目，展示如何使用 .NET Core 3 和 Visual Studio 2019 编写多平台桌面应用程序。

这些示例的源代码可在 netcore3 GitHub 仓库中获取（每个示例都会提供详细链接）。

所有项目均使用 .NET Core 3 构建，其中大多数使用 Visual Studio 2019。

### 8.1 选择多平台应用程序类型：正确的工具用于正确的工作

根据你打算开发的项目类型，选择语言（C++、HTML、XAML ...）和目标框架至关重要。

市场上已经存在许多多平台开发解决方案，但只有 .NET Core 3 在该领域提供了最先进的技术，包括性能、可维护性、语言功能、打包和部署能力。

在本书中，我们将为你提供解决方案的概览，以解决你在开发使用 .NET Core 3 的多平台桌面应用程序时可能遇到的具体问题。

每个提出的解决方案都可以解决特定约束或提供你的应用程序需要集成的特定功能，没有任何一个解决方案能完美满足所有多平台桌面开发需求，因此你必须特别注意选择适合启动的开发类型，以响应你的软件规格（并根据可用资源）。

这可以通过仔细研究本书提供的每个解决方案示例来实现：

- 控制台 GUI 应用程序。
- Web GUI (Electron.NET) 应用程序。
- 原生 GUI 应用程序（图形库 C++、GTK、QML）。
- XAML GUI (Avalonia) 应用程序（某种程度上的原生）。

在这些解决方案中，你应该找到最适合你项目约束和需求的那个解决方案。
这种选择还取决于你的开发者类型（或你更擅长哪种开发以生产高质量产品）。

- 如果你来自面向 Web 的开发（ASP.NET 开发者），使用允许你立即利用这些知识的工具（Electron.NET）来启动桌面应用程序可能是一个明智的选择。
- 如果你是优秀的 C# 和/或 C++ 开发者（控制台、系统、服务），你可以选择一种原生解决方案来实现 GUI (LibUI、GTK#、QML.NET)。
- 如果你是 C# .NET 框架桌面应用程序的老手（或 WPF 开发者），你很可能倾向于 Avalonia 提出的解决方案（但也可能是 QML 或 GTK 解决方案）。

总之，解决方案类型的选择取决于可用资源和你的项目需求。

### 8.2 控制台 GUI 应用程序

自图形用户界面发展以来，许多开发者已经轻视了控制台 GUI，但在许多情况下，它



## 创建 Windows 安装程序

当你完成一个项目后，就需要将应用程序打包以便分发。Visual Studio 提供了工具来为你创建的组件、应用程序和 Web 项目开发安装程序。你可以使用该工具构建一个专业且定制的安装程序。

Setup Wizard 项目使你能够创建一个支持安装 Windows 应用程序项目、Web 应用程序项目和组件项目的项目。当你将项目添加到包含 Windows 应用程序和组件库项目的解决方案中时，一个向导会让你选择安装的详细信息，然后构建项目。

你还可以指定安装程序构建一个 CAB 文件，你可以将其提供在 Internet 上下载。对于 Windows 机器，安装项目构建一个带有 .msi 扩展名的单个文件，该文件使用随 Windows 和 Internet Explorer 的最新版本一起提供的 Windows Installer 工具进行安装。

对于使用 Setup Wizard 安装的项目，向导会检测项目运行所需的依赖项。例如，如果项目需要数据库支持，安装项目会自动包含一个数据库可分发组件。

每个项目中还包含 .NET 可再发行组件。在选择项目后，Setup Wizard 会询问你想要分发应用程序的哪些部分。Primary output 选择包括项目输出的 EXE 或 DLL 文件。Localized resource 选择包括你在项目中包含的任何资源文件。你还可以通过向导包含与项目关联的源代码和内容文件。

创建项目后，你可以通过加载客户端文件系统窗口并指定文件在客户端系统上的加载位置来修改安装详细信息。有关自定义安装的更多信息，请参阅“Customize Your Installation”部分。

## 创建 Windows 安装程序

![](img/d6f772854306e15fb39b861a7b541_325_0.png)

![](img/d6f772854306e15fb39b861a7b541_325_1.png)

1. 打开一个现有的 Windows 应用程序项目并调出 New Project 对话框。
2. 点击 Setup and Deployment Projects，然后选择 Setup Wizard 模板。
3. 为安装项目输入一个名称。
4. 点击将项目添加到当前解决方案。
5. 点击 OK。

   第一个 Setup Wizard 页面出现，解释了该过程。

6. 点击 Next 进入第二个 Setup Wizard 页面。
7. 点击合适的安装程序样式。
8. 点击 Next。

### Extra

你可以创建一个 Windows 安装程序来将 Web 应用程序部署到新服务器，就像安装 Windows 应用程序一样。当 Setup Wizard 开始时，你点击 Create a setup for a Web application 选项。在创建安装程序之前，你必须打开一个 Web Forms 项目。然后将安装项目添加到解决方案中，就像你在简介中为 Windows 应用程序做的安装程序一样。当你运行安装程序时，与 Windows 应用程序安装程序提示你输入安装目录不同，Web 应用程序安装程序会要求你在本地 IIS 副本上的一个虚拟目录中安装 Web 应用程序。安装程序包含所有必要的 .NET Framework 文件，以防 Web 服务器未安装 ASP.NET。File System 窗口包含相同的选项，尽管默认文件夹仅包括 Global Assembly Cache 和 Web Application Folder。Web Application Folder 项表示 Web 应用程序安装到的 Web 服务器目录。通过在需要运行应用程序的服务器上运行 MSI 安装文件来部署服务器。

![](img/d6f772854306e15fb39b861a7b541_326_0.png)

9. 点击项目中的项目以包含在安装程序中。
10. 点击 Next。
11. 在第四个屏幕上，选择需要随安装程序一起包含的任何文件。
12. 点击 Next。
13. 点击 Finish 完成向导。

   安装项目已添加到当前解决方案。

> *Note: See “Customize Your Installation” to customize and build the setup program.*


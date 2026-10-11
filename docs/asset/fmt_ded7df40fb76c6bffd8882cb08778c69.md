
## 开发实体豆 (Entity Beans)

需要注意的是，使用 IDE 等工具开发基于 EJB 的应用程序非常简单，大部分繁琐的工作在可视化设计器的帮助下由开发者自动完成。现在，我们将扩展上一个小节开发的示例，创建一个容器管理的实体豆，并按照以下步骤概述的流程通过 session bean 访问它：

- 因为实体豆代表数据库对象且不直接与客户端交互，因此客户端通过 session bean 访问它们。因此，为了演示实体豆，我们需要创建一个 session bean。由于我们之前已经构建了一个 session bean，也可以利用它。请保持之前的项目打开，以便我们向其中添加新的组件和文件。
- 此外，我们还需要一个数据库来演示实体豆。我们将使用 IDE（企业版）自带的数据库，因为它已经安装在系统中。对于任何其他数据库，处理步骤完全相同，JDBC 驱动程序和连接 URL 除外。我们没有尝试直接在提供的数据库上操作，而是在相同目录下创建了数据库副本。在这种情况下，创建了一个名为“EmployeeSample”的数据库副本。通常，它位于 IDE 目录下的 `/samples/datastores` 子目录中。数据库服务器安装的一个可执行程序非常适合用于探索单个数据库及其内容（包括表结构和数据）。当安装数据库时，没有关联用户 ID 和密码。稍后，可以通过分配用户 ID 和密码来保护数据库。更多细节超出了目前的范围，鼓励读者自行探索这一主题，因为它是非常简单且直观的。

我们选择了数据库中的 `Employee` 表来演示本示例。从 IDE 左上角面板中的项目文件树列表中，双击在早先示例中创建的 EJB Module，右侧编辑器面板将显示 EJB 可视化设计器。此外，你可能会注意到左下角面板中的树列表内容也显示了为项目创建的数据源列表。由于我们还没有添加任何数据源，此列表目前应该是空的。

将鼠标指针悬停在左下角面板中的数据源树列表项上，点击右键。将弹出一个菜单；从该菜单中选择“从数据库导入架构 (Import Schema from Database)”。然后将显示数据库架构提供程序窗口，如图 8.28 所示，我们可以手动输入数据库架构细节，或从已关联的连接对象导入细节。输入数据库架构细节后，确保也输入了用户名和密码，并点击 OK 按钮。

如果正确输入了数据库架构细节，左下面板将显示指定架构的表和其他对象。从架构中识别出 `Employee` 表，将鼠标指针置于表上并点击右键显示弹出窗口，从从中选择“创建 CMP 实体豆 (Create Entity Bean)”，因为本示例是为了演示容器管理的持久实体。

IDE 会创建实体豆对象并将其放置在之前创建的 session bean 对象旁边。当该实体豆的属性如图 8.29 所示时，你会发现它选择了本地接口。这应该被更改为远程或本地/远程，因为我们需要由对象实现远程接口。根据所选接口类型，IDE 会创建 Java 程序并显示在左上角的树列表中。这些通常是 home 接口、远程接口以及豆的实现。

![](img/1c052d580a194876cd94f3b32c39cf4_549_0.png)
FIGURE 8.28 数据库架构提供程序。

![](img/1c052d580a194876cd94f3b32c39cf4_549_1.png)
FIGURE 8.29 实体属性。

现在，如之前解释过的，使用可视化编辑器在 session bean 中创建一个新方法。该方法是 `getEmployeeName()`，它返回 `java.lang.String` 类型的姓名，并接收一个类型为 `java.lang.Short` 的输入参数，用于检索员工编号。

左上角的树还列出了在 EJB 模块（或 JAR 文件）中创建的企业豆。当双击列表中的这些项目之一时，相应的豆属性将会在右侧编辑器面板的多个标签页中，如图 8.30 所示。在图中，显示了带有常用功能的第一个标签页。打开该 session bean 的窗口，因为我们需要在 session bean 中创建实体豆的本地引用。

转到此窗口中的 EJB 本地引用标签页，如图所示

# 536 企业级 Linux 应用开发

### 8.31. 在此页面，您需要点击“Add”按钮为实体豆（entity bean）创建本地引用，并在 Link 和 Type 字段下拉列表中选择相应的项目；所有其他值应保持显示为默认值。

![](img/1c052d580a194876cd94f43b32c39cf4_551_0.png)

图 8.31 会话豆属性–EJB 本地引用。

接下来我们需要编写实现代码。代码列表 8.13、8.14 和 8.15 分别显示了同源接口、远程接口和豆实现。我们不更改这些程序中提供的任何代码。此时，豆实现通常代表数据库中 Employee 表中的一条记录，并且应该注意的是，如之前讨论的，它是一个抽象类。这是因为在容器管理的持久化豆（container-managed persistent beans）的情况下，容器将动态创建实现类以从数据库中检索数据。

代码列表 8.16 显示了修改后的会话豆远程接口，因为它现在包含了新定义的远程方法 `getEmployeeName()`。

代码列表 8.17 是修改后的会话豆实现，其中实现了新方法，用于根据指定的员工编号检索员工的姓和名，并将其拼接成单个员工名称字符串。通常情况下，会话豆通过命名服务定位实体，然后将其收窄到实体豆的远程接口。然后，在远程同源接口上执行 `findPrimaryKey()` 方法，以获取表示实体对象的远程接口。正是这个远程接口为实体豆提供了额外的 getter 和 setter 方法。注意，是此会话豆实现与客户端交互，而不是实体豆，因为实体豆保留在后端（不进行直接交互）。

代码列表 8.18 是测试客户端实现，如上一节所述。该程序中的大部分代码是由前面提到的 IDE 实现的。

现在重新构建整个应用程序并重新部署 JAR 文件。在重新部署 JAR 文件和启动服务器模块之前，如前所述，在 IDE 中启动 Borland Enterprise Server。图 8.32 显示了当使用运行时配置启动服务器模块时，部署在容器中的两个企业豆（会话豆和实体豆）。

最后，运行新构建的测试客户端。如果一切操作都得当，测试客户端应该成功运行并在控制窗口中显示检索到的记录，如图 8.33 所示。

代码列表 8.13 可从附带的 CD-ROM 获取。

# 代码列表 8.13 EmployeeRemoteHome.java—同源接口

```java
package statelesssessionbeans;

import javax.ejb.*;

import java.util.*;

import java.rmi.*;

public interface EmployeeRemoteHome extends javax.ejb.EJBHome {
    public EmployeeRemote create(Short empNo) throws CreateException, RemoteException;
    public EmployeeRemote findPrimaryKey(Short empNo) throws FinderException, RemoteException;
}
```

![](img/1c052d580a194876cd94f43b32c39cf4_552_0.png)

# 538 企业级 Linux 应用开发

![](img/1c052d580a194876cd94f43b2c39cf4_553_0.png)

图 8.32 带有 EJB 部署消息的 JBuilder IDE。

# 代码列表 8.14 EmployeeRemote.java—远程接口

```java
package statelesssessionbeans;

import javax.ejb.*;

import java.util.*;

import java.rmi.*;

import java.sql.*;

import java.math.*;

public interface EmployeeRemote extends javax.ejb.EJBObject {
    public Short getEmpnNo() throws RemoteException;
    public void setFirstName(String firstName) throws RemoteException;
    public String getFirstName() throws RemoteException;
    public void setLastName(String lastName) throws RemoteException;
    public String getLastName() throws RemoteException;
    public void setPhoneExt(String phoneExt) throws RemoteException;
```

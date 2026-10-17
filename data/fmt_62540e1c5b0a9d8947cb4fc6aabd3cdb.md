
| LPO | QCF | jms/itso/QCF | Q0 | jms/itso/Q0 |

# 在开始编写消息驱动 Bean 之前

在开始编写消息驱动 Bean 之前，你需要一个 EJB 和用于消息驱动 Bean 的包：

1. 创建一个名为 `ITSOBankEAR` 的 EAR 应用项目。选择 `File-New Project`。在 New Project 中，在左窗格选择 `J2EE`，在右窗格选择 `Enterprise Application Project`。点击 `Next` 按钮。
2. 指定 Create J2EE 1.3 Enterprise Application project 并点击 `Next` 按钮。
3. 输入应用项目名称 `ITSOBankEAR`。取消选择所有其他选项，仅勾选创建 `EAR` 文件。
4. 在 WebSphere Studio Application Developer 中选择 `J2EE perspective`，并根据 J2EE 2.0 规范创建一个新的 EJB 项目：`ITSOBankEJB`。
5. 同时在 EJB 项目的 `ejModule` 文件夹内创建一个名为 `its.bean` 的包。
6. 右键点击 `ejbModule`，选择 `New -> Other...`，弹出对话框后，在左窗格选择 `EJB`，在右窗格选择 `enterprise bean`。
7. 下一个对话框步骤将显示 `ITSOBankEJB` 项目名称。点击 `Next` 按钮。
8. 选择项目后的下一步将显示标题为 Create a 2.0 enterprise bean 的对话框。选择 `Message-driven Bean` 并输入 Bean 名称：`RcvQ0`（图 5-7）。

![](img/88f7c0f0eff8122fc71c8c318ea660bf_89_0.png)

图 5-7 选择 2.0 EJB 类型

9. 在最后一步中，你必须定义消息驱动 Bean 的属性细节（图 5-8）：
   - 事务类型：容器 `Container` 或 Bean `bean`
   - 确认模式：自动确认 `AutoAcknowledge` 或重复确认 `DupsOkAcknowledge`
   - 目标类型：队列 `Queue` 或主题 `Topic`。如果选择主题，你还可以选择持久性或非持久性消息存活时间。
   - 消息选择器，仅当目标类型为 `Topic` 时生效
   - 监听端口名称 `Listener Port Name`

*(注：由于原文在第 66-70 页之间存在大量乱码和重复，译文已根据可读的逻辑结构进行了处理。)*

要在 WebSphere Studio Application Developer V5.0 测试服务器上测试消息驱动 Bean（Message-driven Bean），需要一个向队列 `Q0` 发送消息的生产者生产者。

## 编写 JMS 客户端

为了更好地了解如何使用 JMS 写入消息队列，我们可以开发一个简单的服务器页面（JSP），其目的是接受两个名为 `Custid` 和 `Quantity` 的整数值作为参数，然后将它们发送到消息队列 `Q0`（图 5-9）。在浏览器中发送消息的命令示例将是：

`http://localhost:9080/ITSOBankweb/sndQ0.jsp?C=101&Q=25`

1. 创建名为 `ITSOBankWeb` 的 Web 项目，该项目属于 EAR 项目 `ITSOBANKEAR`。
2. 在 `ITSOBankWeb` 项目的 `Web Content` 文件夹中创建一个 `sndQ0.jsp` 的 JSP 文件。
3. 插入 Java 代码以获取 `Custid` 和 `Quantity` 参数。

### 示例 5-5 请求参数

```java
<P>Send an Check Reorder Message.</P>
<%
String param;
int custid = 0;
int quantity = 0;
try {
    param = request.getParameter("C");
    if (param != null)
        custid = Integer.parseInt(param);
    param = request.getParameter("Q");
    if (param != null)
        quantity = Integer.parseInt(param);
} catch (NumberFormatException) {
```

4. 插入 JMS 代码向队列 `Q0` 发送一条消息。在发送消息之前，我们必须获取本地 JNDI 环境的句柄，然后查找连接工厂 JNDI 名称 `jms/itsos/QCF` 和目标 JNDI 名称 `itsos/jms/Q0`。参见下面的代码段。

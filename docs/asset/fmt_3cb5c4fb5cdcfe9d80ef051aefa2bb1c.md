
http://www.ibm.com/developerworks/oss/uddi4/

## 来自 IBM alphaWorks 的 UDDI 扩展

IBM alphaWorks UDDI 注册表扩展提供了高级 UDDI 搜索能力。它们允许在单个查询中形成由两个标准 UDDI “查找”API（`find_business` 和 `find_service`）的准则组成的复杂查询。也就是说，`find_business` API 扩展了嵌入的 `find_service` API，而 `find_service` API 扩展了嵌入的 `find_business` API。

使用当前的 UDDI 搜索请求程序时，等效的查询是复杂且容易出错的。客户端搜索技术必须执行两个步骤：
1. 发起两个查询：一个 `find_business` 查询和一个 `find_service` 查询。
2. 处理查询返回的两组结果，并找到结果的适当交集。

UDDI 注册表扩展减少了客户端编程的复杂性，使 UDDI 更容易使用。它们还减少了网络带宽占用并提升了性能。

欲需有关 UDDI 注册表扩展的更多信息，请参阅：
http://www.alphaworks.ibm.com/tech/uddiregistensions

### 8.3.2 服务开发考虑

为了实现运行时的服务位置发现，我们首先需要在开发/测试环境中建立 UDDI 注册表并将服务发布到其中。

#### 部署 WebSphere Studio Unit Test UDDI 注册表

我们在开发和单元测试环境中选择使用 WebSphere Studio Developer V5.1.1 中提供的 Unit Test UDDI 注册表。

该注册表的安装非常方便且简单。它既可以使用 DB2 数据库，也可以使用 Studio 提供的轻量级 Cloudscape™ 数据库。

部署 WebSphere Studio Unit Test UDDI 注册表：
1. 从 Studio 主菜单点击 `File -> New -> Other...`。
2. 在 New 窗口中选择 `Web Services, Unit Test UDDI`，然后点击 `Next`。
3. 在 `Unit Test UDDI Registry Configuration` 窗口中，我们为单元测试选择了带有 Cloudscape 的 "Private UDDI Registry For WAS v5.1"，如第 261 页的图 8-6 所示。点击 `Next`。

![](img/334ef4856dbfc14b1f371b2c8b5e06b2_278_0.png)

**图 8-6** WebSphere Studio 中的 Unit Test UDDI 注册表配置

4. 在 `Unit Test UDDI Registry with Cloudscape Configuration` 窗口中，你需要注意选择 **Use an existing test server**。如果没有，将创建一个新的。如图 8-6 所示，点击 `Finish` 完成 Unit Test UDDI 注册表配置。

第 8 章 服务目录 261

带有 Cloudscape 的 Unit Test UDDI 注册表

| Name | File | Checked | Add... |
|---|---|---|---|
| | | | |
| | | | Delete |

- 为 UDDI 创建新的测试服务器
- 使用现有测试服务器
- 服务器名称：WebSphere v5.1
- 启动 Web Services Explorer

![](img/334ef4856dbfc14b1f371b2c8b5e06b2_279_0.png)

8-7 带有 Cloudscape 的 Unit Test UDDI 注册表

向导向工作空间添加以下项目：
- `UDDI-EAR`
- `UDDI-EJB`
- `UDDI-SOAP`

你可以使用 Web Services Explorer 在 Unit Test UDDI 注册表中发布服务。步骤如下：
1. 从 Studio 主菜单选择 `Run -> Launch Web Services Explorer` 启动 Web Services Explorer。如果需要，使用 URL `http://localhost:9080/uddisap/inquiry` 打开 Unit Test UDDI 注册表。
2. 点击 Web Services Explorer 工具栏上的 UDDI 页面以处理 UDDI 注册表。
3. 点击 Actions 工具栏上的发布图标，如第 263 页的图 8-8 所示。

262 设计：面向服务的架构和 Web 服务

![](img/334ef4856dbfc14b1f371b2c8b5e06b2_280_0.png)

4. 要发布服务接口，选择 **Service Interface** 并完成发布表单所需的详细，如图 8-9 所示。

![](img/334ef4856dbfc14b1f371b2c8b5e06b2_280_1.png)

图 8-9 发布服务接口

5. 要发布业务，选择 **Business** 并完成发布表单所需的详细，如第 264 页的图 8-10 所示。

## 发布

![](img/334ef4856dbfc14b1f371b2c8b5e06b2_281_0.png)

图 8-10 发布业务

6. 滚动到业务详情表单底部，点击 `Publish Service` 将服务添加到业务中。
7. 要发布服务，选择 `Service` 并完成发布服务表单所需的详细，如图 8-11 所示。

通过 Web Services Explorer，我们已经将实现 WSDL 发布为 tModel。然后，我们发布了实现 WSDL。指向该实现的指针进入 `bindingTemplate` `tModelInstanceDetails` 中的 `overview` WSDL 元素。作为此发布过程的一部分，`bindingTemplate` 的 `endpoint` 点将根据实现 `wsdl` 中的端点地址进行更新。

如第269页8.4.1节“服务部署考虑”所述，在运行时环境中的过程略有不同。使用 IBM WebSphere Application Server Network Deployment V5.0，你可以直接从 UDDI Registry 控制台设置 `accessPoint` 元素。

### 8.3.3 服务消费者（客户端）开发考虑

如第209页“调用服务”部分讨论，使用 JAX-RPC 调用服务有三种主要的设计方案：基于存根（stub）的方案、动态调用接口和动态代理。

SCM 应用使用静态存根。存根（stub）是一个静态绑定到服务端点接口（SEI）、WSDL 端口和端口组件的 Java 类。它还绑定到特定的协议绑定和传输方式。存根类定义了 SEI 定义的所有方法。因此，客户端可以通过存根类直接调用 Web 服务。然而，每当 Web 服务定义（接口或实现）发生更改时，都必须重新生成存根。

我们需要修改 Retailer 应用，以在私有 UDDI 注册表中定位 Warehouse 服务的端点 URL。在开发环境中，服务提供者和消费者通常位于同一台服务器上。在此阶段，通常对将服务迁移到不同服务器并不感兴趣。因此，我们选择修改客户端代码，允许根据 RetailerWeb 应用的设置同时使用静态和动态服务发现：
- `uddiEnabled`（设置为 true 或 false）
- `uddiInquiryURL`
- `uddiPublishURL`
- `uddiWarehouseService`
- `uddiWarehouseBusiness`

示例 8-1 展示了我们为 Retailer 应用中添加的、用于执行 UDDI 查找的代码提取。

示例 8-1 修改后的 Retailer 代码提取

```java
WarehouseService service = null;

WarehouseShipmentsPortType port = null;

try {

  Context ctx = new InitialContext();

  service = (WarehouseService) ctx.lookup("java:comp/env/service/WarehouseService");

  if (useUDDI == true) {
```

```java
// 使用 UDDIHelper 类查找端点 URL

if (whUDDIHelper == null) {

    whUDDIHelper = new UDDILookupHelper(

        whUDDIInquiryURL,whUDIPublishURL,

        whUDIService,whUDDBusiness);

}

    port = service.getWarehouse(

    new java.net.URL(whUDDIHelper.getAccessPoint()));

} else {
```

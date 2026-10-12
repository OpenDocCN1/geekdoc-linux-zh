
`http://appsrv1a.ito.ral.ibm.com/wsgw/wsdl/Manufacturer_impl.wsdl`

```
-   4. 编辑 WSDL 以确保任何导入都能从客户端应用程序访问。如示例 9-1 所示，我们的 `Manufacturer_impl.wsdl` 包含两个需要更新的相对导入。我们将：
+   - 将 `location="Manufacturer.wsdl"` 改为
- "`http://appsrv1a.ito.ral.ibm.com/wsgw/wsdl/Manufacturer.wsdl`"
+   - 将 `location="Configuration.wsdl"` 改为
- "`http://appsrv1a.ito.ral.ibm.com/wsgw/wsdl/Configuration.wsdl`"
示例 9-1 更改导入位置前的 `Manufacturer_impl.wsdl`
```

```
<import location="Manufacturer.wsdl"
namespace="http://www.ws-i.org/SampleApplications/SupplyChainManagement/2002-10
/Manufacturer.wsdl/>
<import location="Configuration.wsdl"
namespace="http://www.ws-i.org/SampleApplications/SupplyChainManagement/2002-08
/Configuration.wsdl/>
```

-   5. 保存您的更改。

> 注意：为了简单起见，我们将服务 WSDL 和 XML 架构文件部署到了网关管理控制台 Web 模块。在生产环境中，最好将这些文件部署到相应的服务器。

# 部署网关服务

要将 `Manufacturer_impl.wsdl` 部署为网关服务：

-   1. 打开 Web Services Gateway 管理控制台，点击左侧导航面板上的 `Services -> Deploy`。

-   2. 在 `Deploy Gateway` 窗口中，我们设置了以下字段：

+   - `Gateway Service Name`: `ManufacturerWService`
-    `Channels`: 选择 `SOAPHTTPChannel1`
-    `WSDL Location`:
- `http://appsrv1a.ito.ral.ibm.com/wsgw/wsdl/Manufacturer_impl.wsdl`
-    `Location Type`: `URL`

我们接受了其余字段的默认值。我们的网关服务设置显示在图 9-10 中。

# 网关服务部署
带有星号 (*) 的字段是必需的

| Gateway Service Properties |
| --- | --- |
| Gateway Service Name | ManufacturerServer |
| Message part* | Generic classes<br>☑ Deployed classes |
| Authorization Policy | Control access to this service |
| Audit Policy | Log requests to this service |
| Annotation URL | |
| Channels | SOAPChannel1 |

Request Filters
（未部署）
Response Filters
（未部署）
UDDI References
（未部署）
要选择上述多选项，请使用 Ctrl 点击或刷新页面。

# 目标服务属性

| WSDL Location* | `http://appsrv1a.ito.ral.ibm.com/wsgwj/Manufacturer_Impl.wsdl` |
| Location Type* | ⓒ URL (i)<br>☑ UDDI (i)|
| Target Service Name | |
| Target Namespace | |
| Target Service Information | |

# UDDI 发布属性
当选择 UDDI Reference 时，带有两个星号 (**) 的字段是必需的

| Business Key** | |
| --- | |

![](img/334ef4856dbfc14b1f371b2c8b5e06b2_312.png)

3. 点击 `OK` 部署服务。

4. 我们使用类似的过程将另外两个 Manufacturer 服务和 `WarehouseCallBack` 服务部署为网关服务。您可以在图 9-12 中看到我们最终的网关服务列表。

# 网关服务列表

选择任何项以修改其属性

-   * `ManufacturerBWggwService`
-   `ManufacturerCWsggwService`
-   `ManufacturerXWsggwService`
-   `WarehouseCallBackWswService`

**图 9-12** 网关服务列表

# 导出 WSDL 文件

服务部署后，网关会生成新的 WSDL 文件，可以与 Web 客户端共享。网关生成的 WSDL 实现文件将网关作为服务端点，并导入包含绑定和端口类型信息的 WSDL 接口文件。

要导出 Web Services Gateway 生成的 WSDL 文件：

-   1. 打开 Web Services Gateway 管理控制台，点击左侧导航面板上的 **Services -> List**。

-   2. 在 `List of Gateway` 窗口中，点击所需的服务，在本文中为 **ManufacturerWsgwService**。

-   3. 在 `Service: ManufacturerWsgwService` 窗口中：

+   a. 滚动到 `Exported WSDL definitions` 部分。

+   b. 右键点击 **External WSDL implementation definition (WSDL only)** 并从弹出菜单中选择 **Save Target As...**，如图 9-13 所示。

+   c. 将 WSDL 文件保存到所需位置。我们将文件保存为 WebSphere 工作空间中 `WarehouseWeb/WebContent/WEB-INF/wsdl` 文件夹下的 `Manufacturer_Impl.wsdl`。

# 导出 WSDL 定义

使用以下两个链接查看描述此服务的 WSDL。这些链接**不要**使用。
External WSDL definition
External WSDL definition

| Open |
| Open in Window |
| Save Target |
| Save |
| Copy |
| Copy |
| Post |
| Post |
| Properties |
| Properties |

**图 9-13** 导出 WSDL 文件

网关生成的 WSDL 实现文件将网关作为服务端点，并导入包含绑定和端口类型信息的 WSDL 接口文件。

我们现在准备好启用该服务了。

# 9.4 服务消费者（客户端）

此场景提供了面向服务的架构的另一个示例。WebSphere V5 运行时允许我们轻松将现有客户端重新配置到网关。让我们查看将 Warehouse 更改为网关所需的步骤。

# 使现有客户使用网关

通过网关重新配置 Warehouse：

-   1. 在 Studio 视图的 Project导航器中，导航到 `WarehouseWeb/WebContent/WEB-INF/wsdl`。

-   2. 编辑 `Manufacturer_impl.wsdl` 并将 `soap:location` 从：

```
<wsdlsoap:address location="http://appsrv1a.ito.ral.ibm.com/
```
`http://appsrv1a.ito.ral.ibm.com/wsgw/wsdl/Manufacturer_impl.wsdl/">`
```

更改：

```
<wsdlsoap:address location="http://appsrv1a.ito.ral.ibm.com/
wsgw/wsdl/Manufacturer_impl.wsdl/">
```

-   3. 保存您的更改。

注意：在客户端 WSDL 中将端点地址替换为网关在本文中是行的。在更复杂的场景下，您需要谨慎使用这种方法。安全的方法是从网关重新生成 Web 服务客户端。

然而，从网关重新生成 Web 服务客户端通常意味着生成的 stub 类名也会发生变化。您将需要修改客户端以使用新的 stub 名称。

-   3. 为了让 Warehouse 通过网关访问所有制造商，我们以相同的方式更改了以下 WSDL 文件：

- `ManufacturerB_Impl.wsdl` 在 `WarehouseWeb/WebContent/WEB-INF/wsdl`


| `key_file` | 私钥的完整路径和文件名 | | |
| `namespace_override` | | | |
| `objectstorage_endpoint` | | | |
| `pass_phrase` | 如果密钥已加密，则用于密钥的口令 | | |
| `region` | | | |
| `tenancy` | ocid1.tenancy.oc1.aaaaaaucpnth5jusk7uxfin52k72fsjftkb6c2only4b3udv... | | |
| `user` | ocid1.tenancy.oc1.aaaaaaucpnth5jusk7uxfin52k72fsjftkb6c2only4b3udv... | |

![](img/110fa0d6324f0893fff03cee6394144d_494_0.png)

图 13.49 – 配置 region

19. 接下来，你需要前往 OCI 控制台或记事本复制指纹值输入 VirtualBox。

## 配置文件

**注意：** 此配置文件片段包含使用 SDK、CLI 或其他 OCI 开发工具所需的基础身份验证信息。将文本框中的内容粘贴到你的 `~/.oci/config` 文件中，并更新 `key_file` 参数以指向你的私钥路径。如果你在配置中已有一个 `Default`（默认）配置，则需要执行一些额外的步骤。了解更多 选择 API 密钥指纹

```
c5:ec:ef:10:6c:88:9d:f2:55:72:f4:f18:19:e2:29:f5
```

配置文件（只读）

```
user=ocid1.useroc1_aaaaaaaj4kkhbg5tdwdn2grg47ifrsocxi725qbkyyyghulg2cab5fq
fingerprint=c5:ec:ef:10:6c:88:9d:f2:55:72:f4:f18:19:e2:29:f5
tenancy=ocid1.tenancy.oc1..aaaaaaaauacupnhth55just7kuxfin52k72fsjftk63c2onittly4b3gigudvczq
region=us-ashburn-1
key_file=<path to your privatekeyfile> # TODO
```

将文本框中的内容粘贴到你的 `~/.oci/config` 文件中。

图 13.50 – 指纹

20. 再次将该指纹值粘贴到相应的字段。

| OCI | Properties (属性) | |
|---|---|---|
| `cloud_domain` | oraclecloud.com | |
| `compartment` | 你所在箱的 OCID | | |
| `core_endpoint` | | | |
| `fingerprint` | 使用密钥对的指纹 | | |
| `iam_endpoint` | | | |
| `key_file` | 私钥的完整路径和文件名 | | |
| `namespace_override` | | | |
| `objectstorage_endpoint` | | | |
| `pass_phrase` | 如果密钥已加密，则为密钥的口令 | | |
| `region` | us-ashburn-1 | | |
| `tenancy` | ocid1.tenancy.oc1.aaaaaucpnth5jusk7uxfin52k72fsjftk63c2onittly4b3udv... | | |
| `user` | ocid1.tenancy.oc1.aaaaaucpnth5jusk7uxfin52k72fsjftk63c2onittly4b3udv... | |

图 13.51 – 配置指纹

23. 最后，你还需要回到 OCI 门户并找到 Compartments（箱）菜单。简单的搜索是定位此选项最容易的方法，如果你想直接进入，可以在 Identity（身份）下找到它。

![](img/110fa0d6324f0893fff03cee6394144d_497_0.png)

图 13.54 – 箱

24. 展开你想要使用的箱并复制 OCID，将其输入到 VirtualBox OCI 配置中。

# 测试隔间 (test)

测试隔间

| 重命名隔间 | 编辑描述 | 移动资源 | 删除 | 更多操作 |
|---|---|---|---|---|
| 隔间信息 | 标签 |
|---|---|
| 父级隔间: (root) | 安全区域: - | |
| OCID: ...fccggq 显示复制 | |
| 已授权: 是 | |
| 创建于: 2021年2月2日 星期二，20:34:24 UTC | | |

![](img/110fa0d6324f0893fff03cee6394144d_498_0.png)

25. 如前文所示，将该 OCID 粘贴到相应的字段中。

| 名称: | |
|---|---|
| 属性: | cert-bundle |
| `cloud_domain` | oraclecloud.com |
| `compartment` | |
| `core_endpoint` | |
| `fingerprint` | |
| `iam_endpoint` | |
| `key_file` | `/Users/jsjindel/Desktop/oci-api-key.pem` |
| | 正在使用的密钥对的指纹 |
| `namespace_override` | |
| `objectstorage_endpoint` | |
| `pass_phrase` | 密钥使用的密码（如果该密钥已加密） |
| `region` | us-ashburn-1 |
| `tenancy` | |
| `user` | |
| | 重置 | 应用 | | |

![](img/110fa0d6324f0893fff03cee6394144d_498_1.png)

26. 输入所有数据后，您应该看到 OCID 的区域 (`region`)、用户 (`user`)、租户 (`tenancy`)、密钥文件位置、隔间和指纹属性均已填充。

名称: OCI

属性:

| | |
|---|---|
| `cert_bundle` | |
| `cloud_domain` | oraclecloud.com |
| `compartment` | | |
| `core_endpoint` | | |
| `fingerprint` | | |
| `iam_endpoint` | | |
| `key_file` | `/Users/jspindel/jspindel/Desktop/apikey/oci-api-key.pem` |
| `namespace_override` | | |
| `objectstorage_endpoint` | | |
| `pass_phrase` | 密钥使用的密码（如果该密钥已加密） |
| `region` | us-ashburn-1 |
| `tenancy` | | |
| `user` | | |

重置 应用

图 13.57 – 完成的配置

27. 一旦您确认一切完成，请应用设置。您将看到新的配置出现；我们将其命名为 OCI。

![](img/110fa0d6324f0893fff03cee6394144d_499_0.png)

图 13.58 – VirtualBox OCI

28. 如果您展开配置，将将看到租户 (`tenancy`) 是空的。如果您已经在那里部署了基础设施，您将看到这些资源出现在这里，前提是它们运行在与配置中输入的 OCID 相同的隔间内。

![](img/110fa0d6324f0893fff03cee6394144d_500_0.png)

图 13.59 – 展开的 OCI

您现在已准备好迁移我们在本节之前构建的虚拟机 (VM) 了：

- 1. 在配置好 VirtualBox OCI 配置后，将虚拟机导出到 OCI 的第一步是点击 VirtualBox 主欢迎菜单中的“导出” (Export)。

![](img/110fa0d6324f0893fff03cee6394144d_500_1.png)

图 13.60 – 导出

- 2. 接下来您将选择要导出到 OCI 的虚拟机，如下截图所示 – 在此例中它被称为 `small-ol8.8`。这取决于您为虚拟机命名的名称。

# 对于其他所有人，让我们为 AWS 创建自定义镜像

这看起来非常简单：构建镜像、导出镜像、然后导入镜像（清洗、冲洗、重复）。这个概念并没有比此复杂复杂。然而，仍有一些步骤需要完成，而且其中一些步骤存在陷阱。

首先，你必须熟悉设置和配置 AWS CLI 的步骤。与 OCI CLI 类似，AWS 的 CLI 是一个直接针对 AWS API 执行命令的命令行。在安装并配置 CLI 后，我们将介绍设置 S3 桶、配置该桶以及更改访问权限以允许上传。接下来的图展示了整个配方中的各个阶段及其触点。AWS CLI 是分阶段和执行的共同线索，GUI 也是如此。AWS 中的存储因素通过访问控制和身份验证进行管理，这允许我们创建、存储和操作已存储的对象和桶。

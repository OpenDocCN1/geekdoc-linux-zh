
# 云账户名称

`jspindel`

下一步

忘记云账户名称？获取帮助

你有传统云账户吗？登录

尚未成为 Oracle Cloud 客户吗？注册

图 13.31 – 登录你的账户

而这就是我们等待的地方

![](img/110fa0d6324f0893fff03cee6394144d_482_0.png)

图 13.32 – 登录中

## 2. 一旦你登录账户，就准备好登录了。这是操作开始的地方。我们首先识别租户。

![](img/110fa0d6324f0893fff03cee6394144d_483_0.png)

图 13.33 – 选择

## 3. 一旦你登录租户，你将看到账户设置。这就是我们等待的地方

![](img/110fa0d6324f0893fff03cee6394144d_484_0.png)

图 13.34 – 身份提供程序

## 4. 以下将允许你输入：

| 组 | 组名 | 状态 |
| :--- | :--- | :--- |
| API 密钥 | 管理员 | 激活 |

图 13.36 – 组

## 5. 在接下来的中，你将看到 OCI 设置。

![](img/110fa0d6324f0893fff03cee6394144d_485_0.png)

图 13.38 – 设置

## 6. 选择文件，然后选择环境为 OCI。

![](img/110fa0d6324f0893fff03cee6394144d_486_0.png)

图 13.39 – 已添加密钥

## 7. 一旦你选择了密钥，你将在屏幕上看到 OCI。

## 8. 现在我们已经有了密钥，我们已经到达了可以启动 VirtualBox 界面的节点。

![](img/110fa0d6324f0893fff03cee6394144d_488_0.png)

图 13.41 – VirtualBox OCI 云配置设置

## 10. 一旦你选择了此选项，就必须输入一个名称。我将输入 OCI，因为我们正在使用 OCI。

![](img/110fa0d6324f0893fff03cee6394144d_488_1.png)

图 13.42 – 配置名称

## 11. 现在，在 Oracle Cloud Infrastructure 下，你将看到你的新配置文件 OCI。你可以点击 Properties（属性），这将允许你配置 OCI 配置文件。

![](img/110fa0d6324f0893fff03cee6394144d_488_2.png)

图 13.43 – 名称已提交

## 12. 此时，在另一个窗口中打开 OCI 门户，或者在记事本中剪切并粘贴变量会非常方便。你需要我们在几个章节前的图 13.40 中介绍过的所有信息。

## 13. 你想要复制的第一个 OCIid 是用户的：

![](img/110fa0d6324f0893fff03cee6394144d_489_0.png)

图 13.44 – 用户 OCID

## 14. 将该 OCID 粘贴到 VirtualBox 中前一个截图所示的 OCI 配置文件的 user 属性中。希望你现在已经知道我们要做什么了。

| Properties (属性) |  |
|---|---|
| cert_bundle |  |
| cloud_domain | oraclecloud.com |
| compartment | 你所在箱的 OCID |
| core_endpoint | 使用的密钥对的指纹 |
| iam_endpoint |  |
| key_file | 私钥的完整路径和文件名 |
| namespace_override |  |
| objectstorage_endpoint |  |
| pass_phrase | 如果密钥已加密，则为密钥 |
| region | Oracle Cloud Infrastructure 区域 |
| tenancy | 你的租户的 OCID |
| user | 调用 API 的用户的 OCID |

图 13.45 – 配置用户 OCID

## 15. 与之前一样，但这次是针对 `tenancy`（租户），复制 OCID 并返回 VirtualBox。

### 配置文件预览

**注意：** 此配置文件片段包含使用 SDK、CLI 或其他 OCI 开发工具所需的基础身份验证信息。将文本框中的内容粘贴到你的 `~/.oci/config` 文件中，并更新 `key_file` 参数以指向你的私钥路径。如果你在配置配置中已有一个 `Default`（默认）配置，则需要执行一些额外的步骤。了解更多

选择 API 密钥指纹

```
c5:ec:ef:10:6c:88:9d:f2:55:72:f4:18:19:e2:29:f5
```

配置文件预览（只读）

```
[DEFAULT]
user=ocid1.user.oc1...aaaaaaaaj6k4khg5twdn2grg47irfsocxxi725qbykyyyghulg2cab5fgfq
fingerprint=c5:ec:ef:10:6c:88:9d:f2:55:72:f4:18:19:e2:29:f5
tenancy=ocid1.tenancy.oc1...aaaaaaaucucpnhth5jusk7uxfin52k72fsjftk63c2onitlyv4b3igudvc\zpog
region=us-ashburn-1
```

将文本框中的内容粘贴到 `~/.oci/config` 文件中。

复制

关闭

![](img/110fa0d6324f0893fff03cee6394144d_491_0.png)

## 16. 再次如之前一样，将 tenancy OCID 粘贴到 tenancy 字段。

| Name: OCI | Properties (属性) |  |
|---|---|---|
| cert_bundle |  |  |
| cloud_domain | oraclecloud.com |  |
| compartment | 你所在箱的 OCID |  |
| core_endpoint |  |  |
| fingerprint | 使用的密钥对的指纹 |  |
| iam_endpoint |  |  |
| key_file | 私钥的完整路径和文件名 |  |
| objectstorage_override |  |  |
| pass_phrase | 如果密钥已加密，则用于密钥的口令 |  |
| region | Oracle Cloud Infrastructure 区域 |  |
| tenancy | 你的租户的 OCID |  |
| user | oci1.user.oc1...aaaaajkvmonhwzn.ir/ocxx fingerprint=c5:0e:cc:10:cc29:f5 | 图13.47 – 配置 tenancy

## 17. 回到你的记事本或 OCI 门户，复制 `region`（区域）值，在这种情况下是 `us-ashburn-1`，如接下来的截图所示。记住，很快这一切都会变得清晰。基本上，我们正在告诉 VirtualBox 去哪里、使用哪个区域、哪个租户以及密钥。

### 配置文件

**注意：** 此配置文件片段包含使用 SDK、CLI 或其他 OCI 开发工具所需的基础身份验证信息。将文本框中的内容粘贴到你的 `~/.oci/config` 文件中，并更新 `key_file` 参数以指向你的私钥路径。如果你在配置中已有一个 `Default`（默认）配置，则需要执行一些额外的步骤。了解更多 选择 API 密钥指纹

```
c5:ec:ef:10:6c:88:9d:f2:55:72:f4:18:19:e2:29:f5
```

配置文件预览（只读）

```
[DEFAULT]
user=ocid1.user.oc1...aaaaaj6k4khg5twdn2grg47irfsocxxi725qbykyyyghulg2cab5fq
fingerprint=c5:ec:ef:10:6c:88:9d:f2:55:72:f4:18:19:e2:29:f5
tenancy=ocid1.tenancy.oc1...aaaaaaaucucpnhth5jusk7uxfin52k72fsjftk63c2onitlyv4b3igudvc
region=us-ashburn-1
key_file=path to your privatekey/ ~/.oci/config
```

将文本框中的内容粘贴到 `~/.oci/config` 文件中。

## 18. 如之前一样，将 region 粘贴到正确的字段。

| Name: OCI | Properties (属性) |  |
|---|---|---|
| cert_bundle |  |  |
| cloud_domain | oraclecloud.com |  |
| compartment | 你所在箱的 OCID |  |
| core_endpoint | 使用密钥对的指纹 |  |
| fingerprint |  |  |
| iam_endpoint |  |  |



# caa_profile -create resource_name -t application

# caa_profile -create resource_name -t network

| Option | Resource Attribute |
| -B | executable application |
| -a | ACTION_SCRIPT |
| -d | DESCRIPTION |
| -h | HOSTING_MEMBERS |
| -l | OPTIONAL_RESOURCES |
| -p | PLACEMENT |
| -r | REQUIRED_RESOURCES |
| -o ap | ACTIVE_PLACEMENT |
| as | AUTO_START |
| bt | REBALANCE |
| ci | CHECK_INTERVAL |
| fd | FAILOVER_DELAY |
| fi | FAILURE_INTERVAL |
| ft | FAILURE_THRESHOLD |
| ra | RESTART_ATTEMPTS |
| st | SCRIPT_TIMEOUT |

| Option | Resource Attribute |
| -s | SUBNET |
| -d | DESCRIPTION |
| -o fi | FAILURE_INTERVAL |
| ft | FAILURE_THRESHOLD |

# caa_profile -create resource_name -t [ changer | tape ]

| Option | Resource Attribute |
| -n | DEVICE_NAME |
| -d | DESCRIPTION |
| -o fi | FAILURE_INTERVAL |
| ft | FAILURE_THRESHOLD |

适用于所有 "-create" 版本的选项

| -f | 如果已存在之前的配置文件，则强制创建配置文件。 |
| -q | 以“静默”模式运行——不显示输出。 |

表 23-10：CAA 配置文件创建选项到资源属性

验证了什么？表 23-11 说明了被验证的属性。

## 23.4.8 更新资源配置文件

使用带有 "-update" 选项的 caa_profile 命令（或使用 sysman —— 参见第 23.5.2 节）来修改资源配置文件。您也可以使用您喜欢的编辑器编辑配置文件。

```
# caa_profile -h | grep update
caa_profile -update resource_name [option ...] [-o option,...] [-q]
```

## CAA 资源配置文件验证

| Attribute | Description | Error Message |
|---|---|---|
| NAME | 必须与配置文件名完全匹配，不含 .cap 扩展名。 | NAME attribute must be the same as filename |
|  | 必须不超过 128 个字符，不能为空，或以句点 (.) 开头 | Improper Name: .memberUP |
| TYPE | 必须是有效的资源类型。有效类型为：application、changer、network、tape。此属性区分大小写。 | Invalid Type: guitar |
| PLACEMENT | 必须是有效的放置策略。有效的放置策略可以为：balanced、favored、restricted。此属性区分大小写。 | PLACEMENT invalid: restrict |
| HOSTING_MEMBERS | 如果放置策略不是 balanced，则此属性必须存在。 | HOSTING_MEMBERS is required for: favored placement policy<br>HOSTING_MEMBERS is required for: restricted placement policy |
|  | 如果放置策略为 balanced，则此属性必须不存在。 | No HOSTING_MEMBERS is needed for balanced placement policy |
| ACTION_SCRIPT | 如果配置文件用于 application，则配置文件必须包含此属性。 | The ACTION_SCRIPT attribute of the resource profile must be set |
| SUBNET | 如果配置文件用于 network 资源，则配置文件必须包含此属性。实际的子网或硬件未被验证，尽管它确实会检查子网号是否格式正确。 | Invalid subset setting for network resource |
| DEVICE_NAME | 如果配置文件用于 changer 或 tape 资源，则配置文件必须包含此属性。不会检查硬件是否存在。 | DEVICE_NAME must be set for changer<br>DEVICE_NAME must be set for tape |
| AUTO_START<br>CHECK_INTERVAL<br>FAILURE_DELAY<br>FAILURE_INTERVAL<br>FAILURE_THRESHOLD<br>RESTART_ATTEMPTS | 如果配置文件用于 application 资源，则会检查这些属性。属性值必须是数字但不能为负数。然而，最大值未被检查。 | AUTO_START out of range: -1<br>FAILURE_INTERVAL out of range: 10 widgets |
| OPTIONAL_RESOURCES<br>REQUIRED_RESOURCES | 属性值不得包含冒号 (:)、分号 (;) 或逗号 (,)。然而，值不会被检查是否为现有资源的列表。 | OPTIONAL RESOURCES syntax error: nicUP:tapeDrive<br>REQUIRED RESOURCES syntax error: nicUP,tapeDrive |

您可以使用表 23-9 中列出的大多数选项。有关更多信息，请参阅 `caa_profile(8)` 参考页。

> **NOTE:**
>
> 任何时候资源配置文件被修改，资源注册数据库必须被更新。有关更多信息，请参阅第 23.4.12 节。

## 23.4.9 打印资源配置文件

打印配置文件可以通过三种方式完成。

- 在“sysman caa”中使用 `...` 按钮（参见第 23.5.2 节）。
- 使用带有“-print”选项的 `caa_profile` 命令。

```
$ caa_profile -h | grep print
        caa_profile -print {resource_name [...]} [-q]
```

```
$ caa_profile -print nicUP
NAME=nicUP
TYPE=network
DESCRIPTION=nicUP
FAILURE_INTERVAL=0
FAILURE_THRESHOLD=0
SUBNET=192.168.0.0
```

## 23.4.10 删除资源配置文件

删除配置文件可以通过以下三种方式完成：

- 使用 `rm(1)` 命令删除配置文件。
- 在“sysman caa”中使用 `...` 按钮（参见第 23.5.2 节）。
- 使用带有“-delete”选项的 `caa_profile` 命令。

```
$ caa_profile -delete nicUP
```

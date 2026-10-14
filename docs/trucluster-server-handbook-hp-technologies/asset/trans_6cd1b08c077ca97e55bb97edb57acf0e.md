

# CAA 原因代码

| Reason | Description |
|---|---|
| user | 该动作脚本是由用户操作调用的。集群管理员运行了 `caa_*` 命令。 |
| failure | 该动作脚本是由失败条件的结果调用的。此原因通常是在 "check" 入口点失败的结果下设置的。 |
| dependency | 该动作脚本是由于是另一个资源的依赖项而被调用的。例如，如果 `powerUP` 资源是 `memberUP` 资源的依赖项，并且两个资源都处于 `OFFLINE` 状态，则如果 `memberUP` 资源被启动，`powerUP` 资源也会被启动。此值将设置在 `powerUP` 的 `__CAA_REASON` 环境变量中。 |
| boot | 该动作脚本是在集群启动时被调用的。资源在集群关闭前正在运行。 |
| autostart | 该动作脚本是在集群启动时被调用的。资源的 `AUTO_START` 属性被设置为 1 并且资源在集群关闭前处于 `OFFLINE` 状态。 |
| system | 该动作脚本是由系统在正常维护期间调用的。 |
| unknown | 如果 `__CAA_REASON` 被设置为此状态，则动作脚本是在内部状态未知时被调用的。如果设置了此值，请记录应用程序和集群的状态，然后联系 HP 客户支持中心。 |

表 23-14：CAA 原因代码

- 2. 添加属性。

我们决定添加两个属性以从我们的应用程序资源管理集群别名。

```
# grep -p ALIAS application.cdf
# ==============================
attribute: USR_ALIAS_NAME
type: name_string
switch: -o an
default:
required: no
# ==============================
attribute: USR_ALIAS_IP
type: internet_address
switch: -o aa
default:
required: no
```

3. 你现在可以使用该属性。

例如，我们将使用新的属性创建一个新的应用程序资源。

```
```shell
# caa_profile -create aliasAPP -t application -B /code/caa/aliasAPP \
> -o arcaa_alias,aaq=192.168.1.71
```
```

我们可以通过使用 caa_profile 命令打印资源配置文件来验证资源是否已创建。请注意输出已被精简。

```
```shell
# caa_profile -print aliasAPP | grep -E "NAME|ALIAS"
NAME=aliasAPP
USR_ALIAS_IP=192.168.1.71
USR_ALIAS_NAME=caa_alias
```
```

## 23.5.3.3.2 *在动作脚本中使用用户定义属性*

用户定义属性可以通过在属性名称前添加下划线前缀在应用程序资源的动作脚本中访问。

例如，我们在上一节中创建的 aliasAPP 资源的动作脚本中添加了两个打印语句。

```
```shell
# grep print aliasAPP.scr

print "_USR_ALIAS_NAME = ${_USR_ALIAS_NAME}"
print "_USR_ALIAS_IP = ${_USR_ALIAS_IP}"
```
```

我们仍然从 23.5.2 节设置了 __CAA_UI_FMT 环境变量，因此我们需要做的就是注册并启动资源（当然，我们也必须修改动作脚本并对其进行测试）。

```
```shell
# caa_register aliasAPP
```
```

```
```text
# caa_start aliasAPP
Attempting to start 'aliasAPP' on member 'sheridan'
Start of aliasAPP on member 'sheridan' succeeded.
_USR_ALIAS_NAME = "caa_alias"
_USR_ALIAS_IP = "192.168.1.71"
```
```

正如输出所示，我们的用户定义属性可以从动作脚本中访问。

## 23.5.3.3.3 *临时修改用户定义属性值*

你可以使用 caa_start、caa_stop 和 caa_relocate 命令临时修改用户定义属性。

例如，我们将使用 caa_relocate 命令迁移 aliasAPP 并更改 USR_ALIAS_NAME 和 USR_ALIAS_IP。

```
# caa_relocate USR_ALIAS_NAME=clu_faf USR_ALIAS_IP=192.168.1.77 aliasAPP
Attempting to stop 'aliasAPP' on member 'molari'
Stop of 'aliasAPP' on member 'molari' succeeded.
Attempting to start 'aliasAPP' on member 'sheridan'
Start of 'aliasAPP' on member 'sheridan' succeeded.
sheridan:aliasAPP: USR_ALIAS_NAME = "clu_faf"
sheridan:aliasAPP: USR_ALIAS_IP = "192.168.1.77"
molari:aliasAPP: USR_ALIAS_NAME = "clu_faf"
molari:aliasAPP: USR_ALIAS_IP = "192.168.1.77"
Start of 'aliasAPP' on member 'molari' succeeded.
```

请注意值已被修改。让我们将其迁移回另一个成员。这次我们不会修改属性值。

```
# caa_relocate aliasAPP
Attempting to stop 'aliasAPP' on member 'molari'
Stop of 'aliasAPP' on member 'molari' succeeded.
Attempting to start 'aliasAPP' on member 'sheridan'
Start of 'aliasAPP' on member 'sheridan' succeeded.
molari:aliasAPP: USR_ALIAS_NAME = "caa_alias"
molari:aliasAPP: USR_ALIAS_IP = "192.168.1.71"
sheridan:aliasAPP: USR_ALIAS_NAME = "caa_alias"
sheridan:aliasAPP: USR_ALIAS_IP = "192.168.1.71"
```

属性值恢复为资源配置文件中定义的值。

## 23.5.3.4 区域信息环境变量

_CAA_CLIENT_LOCALE 环境变量包含一个以空格分隔的列表，其中列出了动作脚本被调用时的当前区域。

列表中包含的区域信息顺序如下：

LC_ALL, LC_CTYPE, LC_MONETARY, LC_NUMERIC, LC_TIME, LC_MESSAGES

以下是我们在集群中启动应用程序资源时得到的示例输出。

```
# grep _CAA_CLIENT_LOCALE /var/cluster/caa/script/powerUP.scr
print "_CAA_CLIENT_LOCALE = \"$ _CAA_CLIENT_LOCALE\""
```

由于我们仍然从 23.5.2 节设置了 _CAA_UI_FMT 环境变量，我们将启动 powerUP 资源但仅使用 grep(1) 过滤 _CAA_CLIENT_LOCALE 输出。

```
# caa_start powerUP | grep _CAA_CLIENT_LOCALE
_CAA_CLIENT_LOCALE = "C C C C C C"
```


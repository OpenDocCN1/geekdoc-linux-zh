

```
# caa_stat -t devAPP prodAPP
Name      Type        Target  State   Host
---------- ---------- -------- ------- --------
devAPP    application ONLINE   ONLINE  sheridan
prodAPP   application ONLINE   ONLINE  molari
```

prodAPP 的 action script "start" 入口点的逻辑是否生效？让我们通过将 prodAPP 迁移到 sheridan 来查看。

```
# caa_relocate prodAPP
Attempting to stop 'prodAPP' on member 'molari'
Stop of 'prodAPP' on member 'molari' succeeded.
Attempting to start 'prodAPP' on member 'sheridan'
Start of 'prodAPP' on member 'sheridan' succeeded.
```

如果逻辑生效，devAPP 应该被停止。

```
# caa_stat -t devAPP prodAPP
Name      Type        Target  State   Host
---------- ---------- -------- ------- --------
devAPP    application OFFLINE  OFFLINE 
prodAPP   application ONLINE   ONLINE  sheridan
```

尝试启动 devAPP。

```
# caa_start devAPP
Attempting to start 'devAPP' on member 'sheridan'
Start of 'devAPP' on member 'sheridan' failed.
molari : Resource devAPP (application) cannot run on molari
Could not start resource devAPP.
```

devAPP 的 action script "start" 入口点的逻辑似乎正在工作，但我们只测试了将 prodAPP 迁移到 sheridan 时 prodAPP 的 action script "start" 入口点的第一个分支。

让我们通过将 prodAPP 迁移到 molari 来完成测试。

```
# caa_relocate prodAPP
Attempting to stop 'prodAPP' on member 'sheridan'
Stop of 'prodAPP' on member 'sheridan' succeeded.
Attempting to start 'prodAPP' on member 'molari'
Start of 'prodAPP' on member 'molari' succeeded.
```

如果我们的逻辑生效，devAPP 应该已在 sheridan 上重新启动。

## Main Menu Buttons

## Setup Menu Buttons

| Button | Equivalent CAA Command |
|---|---|
| Setup... |  |
| Start... | caa_start |
| Stop... | caa_stop |
| Relocate... | caa_relocate |
| Details... | caa_stat -p |

| Button | Equivalent CAA Command |
|---|---|
| Add... | caa_profile -create |
| Modify... | caa_profile -update |
| Delete... | caa_profile -delete |
| Register... | caa_register |
| Unregister... | caa_unregister |

Table 24-1: Main Menu and Setup Menu Buttons to caa_* Commands

![](img/a0df85c2e542a8d6c913113908553aa4_738_0.png)

Figure 24-3: CAA Setup Window

![](img/a0df85c2e542a8d6c913113908553aa4_738_1.png)

Figure 24-4: CAA Setup: Add Resource Popup and Resource Type Pulldown Menu

- 选择一个唯一且相对描述性的资源名称。
  在我们的示例中，我们选择将资源命名为“memberUP”，以表示如果该资源在集群中的某处正在运行，则表示成员已启动。
- 使用下拉菜单选择资源类型。
  在此示例中，我们将创建一个应用程序资源。
- 单击 [redacted] 按钮继续 – 这将弹出图 24-5 所示的窗口。

下一步是输入没有默认值所需的配置文件属性。

| Resource | Required Resource Attribute without a default value |
|---|---|
| Application | ACTION_SCRIPT |
| Changer | DEVICE |
| Network | SUBNET |
| Tape | DEVICE |

在我们的例子中，我们将选择要管理的应用程序名称和 action script 名称。对于更复杂的应用程序，我们可能会编写自己的 action script。然而，由于我们将使用我们编写的非常简单的 Tcl/Tk 应用程序（参见第 24.2.1 节），我们将选择生成默认 action script，并简单地指定应用程序的路径。选择生成默认 action script 会导致“sysman caa”从 /var/cluster/caa/template 目录复制 template.scr 脚本，并在脚本中的适当位置插入应用程序名称和资源名称。

```
grep -E "memberUP|hostname" /var/cluster/caa/script/memberUP.scr

SERVICE_NAME="memberUP"
PROBE_PROCS="/code/caa/xhostname"
START_APPCMD="/code/caa/xhostname"
```

请注意，action script 名称是资源名称加上“.scr”扩展名。另请注意，脚本默认将位于 /var/cluster/caa/script 目录中。我们建议所有 action script 保持在此默认目录中。

此时，您可以通过单击 **OK** 按钮采用默认配置文件属性。或者，您可以通过单击 **Options** 按钮来自定义配置文件属性。

### 24.9.1.1 Customize Profile Attributes

Options 弹出窗口包含剩余属性的默认值。每个资源类型的 Options 弹出窗口如图 24-6 所示。

![](img/a0df85c2e542a8d6c913113908553aa4_740_0.png)


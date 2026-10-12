
- 姓：`Coughanour`
- 上下文：`SLC.CLE`
- 密码：`novell`
- 标题：`President`
- 位置：`Salt Lake City, Utah Office`
- 部门：`Executive Management`
- 电话：555-555-5555
- 传真号：555-555-4444
- 电子邮件地址：`dcoughanour@cle.com`

### 7. 通过完成以下步骤授予`CGrayson`对`IF`容器的管理权限：
- a. 在`iManager`中，向下滚动到`权限`并选择`修改受托人`。
- b. 在`对象名称`字段中，输入`IF.CLE`，然后点击`确定`。
- c. 选择`添加受托人`。

### 8. 通过完成以下步骤，验证 `CGrayson.IFCLE` 是否具有你分配的权利：
- a. 在 `iManager` 中，选择 `查看有效权限`（`View Effective Rights`）。
- b. 在 `受托人名称`（`Trustee Name`）字段中，输入 `CGrayson.IFCLE`，然后点击 `确定`（`OK`）。
- c. 在 `对象名称`（`Object Name`）字段中，浏览并选择 `IFCLE`。
- d. 在 `属性名称`（`Property Name`）字段中，选择 `条目权限`（`Entry Rights`）。你应能看到 `浏览`（`Browse`）、`创建`（`Create`）、`重命名`（`Rename`）和 `删除`（`Delete`）权限已列出。
- e. 在 `对象名称`（`Object Name`）字段中，浏览并选择 `CLE`。
- f. 选择 `条目权限`（`Entry Rights`）。`CGrayson.IFCLE` 对 `CLE` 容器应只有 `浏览`（`Browse`）权限。
- g. 点击 `完成`（`Done`）。

> `CGrayson.IFCLE` 拥有 `浏览`（`Browse`）权限，因为树中的每个用户都与 `[Public]` 在安全上等效。请记住，`[Public]` 对树根拥有 `浏览`（`Browse`）权限。

### 9. 通过完成以下步骤创建一个 `组织角色`（`Organizational Role`），并将 `DCoughanour.SLC.CLE` 设为该角色的使用者：
- a. 在 `iManager` 中，选择 `eDirectory 管理`（`eDirectory Administration`）下的 `创建对象`（`Create Object`）。
- b. 在 `可用对象类`（`Available Object Classes`）字段中，选择 `组织角色`（`Organizational Role`），然后点击 `确定`（`OK`）。
- c. 在 `组织角色名称`（`Organizational Role Name`）字段中，输入 `Manager`。
- d. 在 `上下文`（`Context`）字段中，输入 `CLE`，然后选择 `确定`（`OK`），`确定`（`OK`）。
- e. 选择 `修改对象`（`Modify Object`）。
- f. 在 `对象名称`（`Object Name`）字段中，输入 `Manager.CLE`，然后点击 `确定`（`OK`）。
- g. 在下拉列表中，选择 `角色使用者`（`Role Occupant`）。
- h. 在 `角色使用者`（`Role Occupant`）字段中，浏览并选择 `DCoughanour.SLC.CLE`。
- i. 点击 `确定`（`OK`）。

### 10. 通过完成以下步骤，授予 `Manager.CLE` 对 `CLE` 容器的管理员权限：
- a. 在 `iManager` 中，向下滚动到 `权限`（`Rights`），并选择 `修改受托人`（`Modify Trustees`）。
- b. 在 `对象名称`（`Object Name`）字段中，输入 `CLE`，然后点击 `确定`（`OK`）。
- c. 选择 `添加受托人`（`Add Trustee`）。
- d. 选择 `浏览`（`Browse`）。
- e. 浏览并选择 `Manager.CLE`。
- f. 在 `Manager.CLE` 旁边，选择 `分配的权限`（`Assigned Rights`）。
- g. 在 `条目权限`（`Entry Rights`）行，标记 `浏览`（`Browse`）、`创建`（`Create`）、`重命名`（`Rename`）、`删除`（`Delete`）。
- h. 选择 `完成`（`Done`）、`确定`（`OK`）、`确定`（`OK`）。

### 11. 通过完成以下步骤，验证 `DCoughanour.SLC.CLE` 是否具有你分配给 `Manager.CLE` 的权限：
- a. 在 `iManager` 中，选择 `查看有效权限`（`View Effective Rights`）。
- b. 在 `受托人名称`（`Trustee Name`）字段中，输入 `DCoughanour.SLC.CLE`，然后点击 `确定`（`OK`）。
- c. 在 `对象名称`（`Object Name`）字段中，浏览并选择 `CLE`。
- d. 选择 `条目权限`（`Entry Rights`）。你应能看到 `浏览`（`Browse`）、`创建`（`Create`）、`重命名`（`Rename`）和 `删除`（`Delete`）权限已列出。
- e. 在 `对象名称`（`Object Name`）字段中，浏览并选择 `.CLE-TREE`。
- f. 选择 `条目权限`（`Entry Rights`）。`DCoughanour.SLC.CLE` 对树根应只有 `浏览`（`Browse`）权限。
- g. 重复此过程以检查 `DCoughanour` 对 `IF` 和 `SLC` 容器的有效权限。他对每个容器应具有 `浏览`（`Browse`）、`创建`（`Create`）、`重命名`（`Rename`）和 `删除`（`Delete`）权限。
- h. 点击 `完成`（`Done`）。

### 12. 通过完成以下步骤，在 `CLE`、`IF` 和 `SLC` 级别划分 `eDirectory` 树：
- a. 在 `分区`（`Partitions`）和 `副本管理`（`Replica Management`）下，选择 `创建分区`（`Create Partition`）。
- b. 在 `容器`（`Container`）字段中，输入 `CLE`，然后点击 `确定`（`OK`）。
- c. 等待过程完成。
- d. 当提示分区已完成时，选择 `重复任务`（`Repeat Task`）。
- e. 使用前面的步骤，在 `IFCLE` 和 `SLC.CLE` 容器级别创建分区。

### 13. 通过完成以下步骤，验证你的分区是否已创建，并且你的服务器持有每个分区的主副本（`Master replica`）：
- a. 在 `iManager` 中，选择 `查看分区信息`（`View Partition Information`）。
- b. 在 `分区`（`Partition`）字段中，选择 `浏览`（`Browse`）图标。
- c. 选择 `浏览`（`Browse`）。
- d. 浏览并选择 `CLE 分区`。
- e. 点击 `确定`（`OK`）。
- f. 验证分区是否存在，并且你的服务器持有主副本。
- g. 重复前面的步骤以检查 `IFCLE` 和 `SLC.CLE` 分区。
- h. 完成后，点击 `关闭`（`Close`）。
- i. 通过选择 `副本视图`（`Replica View`）来检查你的副本状态。
- j. 在分区或服务器对象中，输入 `CLE1.IF.CLE`，然后点击 `确定`（`OK`）。
- k. 你应能看到你的服务器拥有树中四个分区的主副本：树根、`CLE`、`IF.CLE` 和 `SLC.CLE` 分区。这显示在图 5.34 中。

![](img/c7771e8540507f2b00c088c7a411b57b_238_0.png)

**图 5.34**

副本视图。

> **警告**
>
> 如果我们的树中有多个服务器，我们可以将每个分区的其他副本放置在它们上面。但是，由于我们只有一个单服务器树，我们必须使用 **图 5.34** 中显示的复制方式。

1. 点击 `完成`（`Done`）。

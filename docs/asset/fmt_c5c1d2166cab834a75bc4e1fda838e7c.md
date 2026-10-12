
出于安全考虑，我们在这里将此限制为 `localhost`，但如果你想向远程用户授予权限，则需要更改此名称（见后文）。在我们的示例中，我们使用 `type of permission` 为 `ALL`，但你始终可以决定最小化：

- `ALL`: 允许 `<username>` 添加数据库
- `CREATE`: 允许 `<username>` 创建新数据库
- `DROP`: 允许 `<username>` 删除数据库
- `DELETE`: 允许 `<username>` 删除行
- `INSERT`: 允许 `<username>` 插入行
- `SELECT`: 允许 `<username>` 读取行
- `UPDATE`: 允许 `<username>` 更新行

然而，在授予权限后，食谱告诉我们必须刷新系统。重要的是，`MariaDB` 壳中的所有命令应以分号（`;`）结束。完成任务后，我们只需退出控制台。

### 更多...

创建受限用户是提供数据库访问的方法，但如果你有一组需要持续访问服务器的开发人员，你可能希望考虑提供通用用户。要实现此，只需以管理员 `root` 登录 `MariaDB` 服务器，然后按以下方式创建新用户：

```
GRANT ALL ON .* TO '<username>'@localhost IDENTIFIED BY '<password>' WITH GRANT OPTION;
```

通过这种方式，你允许 `<username>` 在 `MariaDB` 服务器上添加、删除和管理数据库，但考虑到功能的范围，此新用户账户将所有活动限制在 `localhost`。简单来说，如果你为 `<username>` 提供任何数据库或任何表的访问权限，始终使用星号（`*`）代替数据库名或表名。最后，在退出 shell 之前，确保使用 `FLUSH PRIVILEGES` 命令。

## 检查和撤销权限或删除用户

除非使用，否则保持用户账户活跃是不好的，因此你在 `MariaDB` 壳中（以管理员 `root` 用户登录）的首要考虑是通过输入以下命令查看其当前状态：

```
SELECT HOST, USER FROM mysql.user WHERE USER='<username>';
```

完成后，如果你打算撤销权限或删除此处列出的用户，可以使用 `DROP` 命令执行。首先，你应该通过运行以下命令查看感兴趣的用户拥有的权限：

```
SHOW GRANTS FOR '<username>'@localhost';
```

你有两种选择，首先是按照以下方式撤销用户的权限：

```
REVOKE ALL PRIVILEGES, GRANT OPTION FROM '<username>'@localhost;
```

然后你可以使用主食谱中提供的公式重新分配权限，或者也可以决定通过输入命令来删除用户：

```
DROP USER '<username>'@localhost;
```

## 数据库操作

### 允许 MariaDB 服务器的远程访问

除非你运行 `MariaDB` 数据库服务器是为了在同一服务器硬件上驱动某些本地 Web 应用，否则如果禁止对数据库服务器进行访问，大多数工作环境将毫无意义。在许多 IT 环境中，你会发现高可用、集中化的专用数据库服务器，它们在硬件上经过优化（例如巨大的内存），并托管了多个数据库，允许外部向服务器建立并行连接。在本教程中，我们将向你展示如何实现对服务器的远程连接。

#### 准备工作

要完成本教程，你需要一个具有 `root` 权限且运行良好的 `CentOS 7` 操作系统。系统中已经安装并运行了 `MariaDB` 服务器，并且你已经阅读并应用了《管理 MariaDB 数据库》教程，以了解权限以及如何进行（本地）数据库连接。

### 操作步骤...

在示例中，我们希望从同一网络中 IP 地址为 `192.168.1.33` 的客户端计算机，访问 IP 地址为 `192.168.1.12` 的 `MariaDB` 数据库服务器。请根据你的需求适当修改：

1. 首先，以 `root` 身份登录你的 `MariaDB` 数据库服务器，并为入站 `MariaDB` 连接打开防火墙：

   ```
   firewall-cmd --permanent --add-service=mysql && firewall-cmd --reload
   ```

2. 然后，我们需要创建一个可以远程连接到 `MariaDB` 服务器的用户账户（出于安全考虑，我们在后续步骤中阻止了 `root` 执行此操作）。使用 `root` 身份通过 `MariaDB` 命令行界面 `mysql` 登录数据库并输入以下 `MariaDB` 语句（将 `XXXX` 替换为你选择的密码，可以随意调整想要连接服务器的客户端用户名和远程 IP——我们的示例中客户端 IP 为 `192.168.1.33`，请相应修改）：

   ```
   GRANT SELECT ON mysql.user TO 'johnndoe@192.168.1.33' IDENTIFIED BY 'XXXX';
   FLUSH PRIVILEGES; EXIT;
   ```

3. 现在我们可以从网络中 IP 地址为 `192.168.1.33` 的客户端连接服务了。这台电脑需要在 `CentOS 7` 客户端上安装 `MariaDB` shell，安装 `mariadb` 软件包，并且需要能够 ping 通运行 `MariaDB` 服务的服务器（在示例中，IP 为 `192.168.1.12`）。你可以使用以下命令测试连接到服务器（成功后），这将打印出 `mysql` 用户表的内容：

   ```
   echo "select user from mysql.user" | select -u johndoe -p mysql -h192.168.1.12
   ```

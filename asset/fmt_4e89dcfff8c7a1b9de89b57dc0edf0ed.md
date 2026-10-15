
- 3. 滚动到文件末尾并追加以下行，使这些行的内容如下（将`XXX.XXX.XXX.XX`替换为您想要授予访问权限的网络。例如，如果您的服务器 IP 地址为`192.168.1.12`，则网络地址为`192.168.1.0/24`）：

```text
host     all             XXX.XXX.XXX.XX    md5
```

- 4. 完成后，只需按通常方式保存并关闭文件，然后输入命令打开主 Postgres 配置文件：

```bash
vi /var/lib/postgresql/data/postgresql.conf
```

- 5. 在文件末尾添加以下行：

```conf
listen_addresses = '*'
port = 5432
```

# 数据库操作

- 6. 完成后，按通常方式保存文件，然后输入以下命令重启数据库服务器：`systemctl restart postgresql`

- 7. 在同一网络（由之前定义的`XXX.XXX.XXX.XX/XX`值定义）的任何其他计算机上，您现在可以通过使用`psql`shell连接到远程 Postgres 服务器（如果您的客户端计算机是 CentOS，您将需要使用`yum install postgresql`安装它），远程登录服务器并打印一些测试数据。在我们的示例中，Postgres 服务器运行在 IP 地址`192.168.1.12`。

```bash
psql -h 192.168.1.12 -U <username> -d <database-name>
```

### 工作原理

PostgreSQL 是一个安全的数据库系统，但我们访问它的方式（远程或本地）往往会引起困惑。本食谱的目的是揭开基于主机的身份验证的机制，并提供一个简单的解决方案，让您的系统准备就绪。

### 如何操作...

在本份教程中，我们将首先向您展示如何安装和配置 phpMyAdmin 以实现远程访问，随后将展示如何对 phpPgAdmin 进行相同的操作。

## 安装和配置 phpMyAdmin

要安装 phpMyAdmin，请执行以下步骤：

- 1. 输入以下命令安装所需的包：

```bash
yum install phpMyAdmin
```

- 2. 现在，为主 phpMyAdmin 配置文件创建一个备份：

```bash
cp /etc/httpd/conf.d/phpMyAdmin.conf /etc/httpd/conf.d/phpMyAdmin.conf BAK
```

- 3. 接下来，打开主`phpMyAdmin.conf`配置文件，并在`Require ip 127.0.0.1`这一下方，将`Require ip XXX.XXX.XX/`替换为您定义的、想要访问 Web 应用的子网地址，例如下方的`Require ip 192.168.1.0/24`。您可以直接在文件中进行此操作，也可以使用命令自动完成，如下所示。在命令行中相应地定义环境变量`NET=192.168.1.0/24`以适应您的子网网络地址。

- 4. 然后按照该行将您的更改应用到配置文件：

```bash
sed -i 's/\\Require ip 127.0.0.1\\\\require ip $NET/g' /etc/httpd/conf.d/phpMyAdmin.conf
```

- 5. 之后，重新加载 Apache 服务器，然后您应该能够通过运行 Web 应用的服务器 IP（例如`192.168.1.12`）从子网中的任何其他计算机访问 phpMyAdmin 网站（使用您的 MariaDB 管理员`root`或任何其他数据库用户登录）：

```text
http://192.168.1.12/phpMyAdmin
```

## 安装和配置 phpPgAdmin

以下是安装和配置 phpPgAdmin 的步骤：

- 1. 输入以下命令安装所需的包：

```bash
yum install phpPgAdmin
```

- 2. 在编辑 phpPgAdmin 主配置之前，请先对其进行备份：

```bash
cp /etc/httpd/conf.d/phpPgAdmin.conf /etc/httpd/conf.d/phpPgAdmin.conf BAK
```

- 3. 允许 phpPgAdmin 远程访问与 phpMyAdmin 非常相似。在这里，您也可以在`phpPgAdmin.conf`文件的`Require local`行下方添加带有定义的子网网络地址的`Require ip XXX.XXX.XXX/XX`行，或者使用工具为您自动完成：

```bash
NET="192.168.1.0/24"

sed -i "s,\\(Require local\),\1\nRequire ip $NET/g" /etc/httpd/conf.phpPgAdmin.conf.
```

- 4. 重启 Apache 并访问 phpPgAdmin 主页：

```text
http://192.168.1.12/phpPgAdmin
```

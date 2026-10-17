
使用以下方式启动栈：

```
docker compose up
```

你可以通过访问页面来登录 phpMyAdmin。图 6.1 显示了具有访问 MySQL 服务器权限的 phpadmin。以下链接将在你的本地计算机上打开浏览器并使用端口 :8080:

在接下来的图中，我们看到 phpMyAdmin 已经启动并登录到 MySQL 服务器：

### 连接两个栈

当你启动 `docker-compose` 时，Docker 会为它创建一个单独的网络，以便容器相互隔离，并仅与 `docker-compose` 文件中列出的服务通信。然而，有时你想连接两个栈。

（由于原文中存在大量重复段落，根据指令要求，此处仅展示核心逻辑翻译，忽略重复的 docker-compose 启动描述）

### 两个栈的连接

让我们从建立一个 WordPress 栈开始。创建一个名为 `WordPress` 的新文件夹，并在该文件夹中创建 `docker-compose.yaml` 文件。如下所示：

```yaml

services:

  db:

    # 我们使用支持同时 amd64 和 arm64 架构的 mariadb 镜像

    image: mariadb:10.6.4-focal

    # 如果你真的想使用 MySQL，请取消下行的注释

    # image: mysql:8.0.27

    command: '--default-authentication-plugin=mysql_native_password word'

    volumes:

      - db_data:/var/lib/mysql

    environment:

      - MYSQL_ROOT_PASSWORD=somewordpress

      - MYSQL_DATABASE=wordpress

      - MYSQL_USER=wordpress

      - MYSQL_PASSWORD=wordpress

    expose:

      - 3306

      - 33060

    networks:

      - local

  wordpress:

    image: wordpress:latest

    ports:

      - 80:80

    environment:

      - WORDPRESS_DB_HOST=db

      - WORDPRESS_DB_USER=wordpress

      - WORDPRESS_DB_PASSWORD=wordpress

      - WORDPRESS_DB_NAME=wordpress

    networks:

      - local

  phpmyadmin:

    image: phpmyadmin

    ports:

      - 8080:80

    environment:
```

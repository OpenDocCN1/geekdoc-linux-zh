
备份 `server.key` 并将其保存在安全的地方。如果在在使用创建数字证书后丢失了 `server.key`，证书将无法工作。

## 第三部分：Red Hat Linux 服务

![](img/d1fb1ff3244ecb66d002a5e633e6f729_429_0.png)

## 生成自签名证书

创建加密密钥后，使用以下命令创建自签名证书：

1. 执行以下命令：

```
cd /etc/httpd/conf

openssl req -new -key server.key -x09 -days 365 -out server.crt -config /usr/share/ssl/openssl.cnf
```

2. 输入上一节创建的密码。

3. 密码接受后，证书生成过程会提示提供更多信息。回答提示，如下所示（由于布局限制输出已换行）。你输入的内容将加粗显示：

国家名称（两位代码）：**US**
州或省份（全称）：**Indiana**
市名称（例如城市）：**Indianapolis**
组织名称（例如公司）：**KurtWerks**
组织单位名称（例如部门）：
通用名称（例如你的名称或服务器主机名）：**host.localdomain**
电子邮箱地址：**kwall@kurtwerks.com**

4. 生成证书后，使用以下命令重启服务器：

```
/etc/rc.d/init.httpd restart
```

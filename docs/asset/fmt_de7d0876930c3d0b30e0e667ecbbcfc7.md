
## 10. 退出以继续 AWX

现在你需要退出，这非常重要，以便继续 AWX：

```
[root@olam-test ~] exit
```

## 11. 切换用户到 AWX

在这里我们将用户切换到 AWX 以继续：

```
[olam-test ~] su -l awx /bin/bash
```

## 12. 使用 Podman 创建环境

OLAM 在云原生环境中运行，我们使用 Podman 来编排环境创建。以下命令使用最新版本的 Podman 在你的虚拟机内创建：

```
[aws@olam-test ~] podman system migrate
```

## 13. 从 Oracle 仓库拉取最新版本的 OLAM

现在通过运行以下命令从 Oracle 仓库拉取最新版本的 OLAM：

```
[aws@olam-test ~] podman pull container-registry.oracle.com/oracle_linux_manager/olam-ee:latest

Trying to pull container-registry.oracle.com/oracle_linux_manager/olam-ee:latest...

Getting image signatures

Copying blob 1a7c48b9e5 done

Copying blob a2dc21763a7 done

Copying blob 13ec279a4b done

Copying blob 0b5ff9a3f done

Copying config b3f64737f done

Writing manifest to image

Storing signatures
```

## 14. 迁移环境到容器

现在我们要迁移环境到容器：

```
[aws@olam-test ~]$ aws-manage migrate

Operations to perform:

  Apply all migrations: auth, conf, contenttypes, main, cauth2provider, sessions,

sites, social_django, sso, tagging

Running migrations:

The output has been truncated for length.
```

## 15. 创建用户

现在我们要创建用户：

```
[aws@olam-test ~]$ aws-manage createsuperuser --username admin --email bubba@nobody.com

Password:

Password (again)
```

## 16. 配置环境

我们已经创建了环境，需要对其进行配置：

```
[aws@olam-test ~]$ openssl req -x509 -newkey rsa:2048 -days 365 -keyout /etc/tower.key -out /etc/tower.crt -nodes -subj "/C=US/ST=Florida/L=Miami/O=Organization Ltd/CN=localhost"
```

## 17. 退出

现在我们要退出：

```
[aws@olam-test ~]$ exit
```

## 18. 设置服务器

现在我们要设置服务器。通过以下命令完成：

```bash
[root@olam-test ~]$ cat << EOF | sudo tee /etc/nginx.conf

# CONNECTIONS AND AUTHENTICATION

# ---

# Connection Settings.

listen_addresses = 'OCI NAT Address' - IP address in config

#listen_addresses = 'localhost' # What IP address (es) to listen on:

events {

    worker_connections 1024;

}

http {

    log_format main '$remote_addr - $remote_user [$time_local] "$request" '

      '$status $body_bytes_sent "$http_referer" "$http_user_agent" "$x_forwarded_for";

    access_log /var/log/nginx/access.log main;

    include /etc/nginx/mime.types;

    default_type application/octet-stream;

    sendfile on;

    tcp_nopush on;

    tcp_nodelay on;

    keepalive_timeout 65;

    types_hash_max_size 2048;

    include /etc/nginx/conf.d/*.conf;

}

EOF
```

## 19. 配置实例

我们要配置实例，定义如下文。首先，如何切换到 `awx` 用户：

```
[root@olam-test ~]$ sudo su - awx /bin/bash
[awk@olam-test ~]$ aw-manage provision instance --hostname=10.0.0.193 --node-type=hybrid

Successfully registered instance 10.0.0.193
(Changed: True)
```

## 20. 注册环境

我们通过运行以下命令注册环境：

```
[root@olam-test ~]$ awk-manage register_execution_environments
'OLAM EE (latest)' Default Execution Environment registered.
'OLAM EE (latest)' Default Execution Environment updated.
Control Plane Environment registered.
(Changed: True)
[root@olam-test ~]$ awk-manage register_queue --queuename=controlplane --hostnames=10.0.0.193
Creating instance group controlplane
Added instance 10.0.0.193 to controlplane
(Changed: True)
controlplane
(Changed: True)
```

```
# redial: true

# tls-server:

# name: mutual-tls

# cert: /etc/receptor/certs/awx.crt

# key: /etc/receptor/certs/awx.key

# requireclientcert: true

# clientat: /etc/receptor/certs/ca.crt

- control-service:

  service: control

  filename: /var/run/receptor/receptor.sock

- work-command:

  worktype: local

  command: /var/lib/ol-automation-manager/venv/bin/runner

  params: worker

  allowunlimitedimeparams: true

  verifignature: true
```

## 22. 启用 OLAM 服务

现在，我们将通过运行以下命令来启用 OLAM 服务，这开始了访问 OLAM 的过程：

```
[root@olam-test ~]# systemctl enable --now ol-automation-manager.service
Created symlink /etc/systemd/system/multi-user.target.wants/ol-automation-manager.service -> /usr/lib/systemd/system/ol-automation-manager.service.
```

## 23. 预加载数据

现在，我们想通过运行以下命令来预加载数据。一旦完成，我们就可以准备登录您的 OLAM 实例，我们的安装将是：

```
[awx@olam-test ~]$ awx-manage create_preload_data
```

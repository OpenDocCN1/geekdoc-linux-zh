
Mar 28 10:01:51 serverb setroubleshoot [27387]: SELinux is preventing `/usr/sbin/httpd` getattr access on the file `/lab-content.html` For example SELinux messages: `sealert -1 8562c3d4-4ac5-4bf6-8e6e79fe2cd`

Mar 28 10:01:51 serverb platform-27387]: SELinux is preventing `/usr/sbin/httpd` getattr access on the file `/lab-content.html#0121* Plugin catch (100, confidence) suggests`

*****************\*\*\*\*\*

#0122if you believe that httpd was allowed getattr access on the lab.html file by default.#0122then you should report this as a bug, #012b you can generate a local policy module to allow this access. #012db this access for now by executing:#012a search -c 'httpd' --raw | audit2allow -M my-httpd#012m -X 300 -i my-httpd#012

```
- 3.2. 运行建议的 `sealert` 命令。注意源上下文（source context）、目标对象（target objects）、策略和强制模式（enforcing mode）。
```

```
[root@serverb ~]# sealert -1 8824e73d-3ab0-4caf-8258-86e879fe2fd

SELinux is preventing /usr/sbin/httpd getattr access on the /lab-content.html.
```

\*\*\*\* Plugin catch (100, confidence) suggests
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

如果你认为默认允许对 lab.html 文件进行 getattr 访问，你应该将其报告为错误。
你可以生成一个本地策略模块来允许此访问。
现在通过执行以下命令临时允许此访问：
## `ausearch -c 'httpd' --raw | audit2allow -M my-htpd`
## `seman -X 300 -i my-httpd`

附加信息：
| Field | Value |
| :--- | :--- |
| Source Context | system_u:system_httpd_t |
| Target Context | unconfined:u:object_r:default:t |
| Target Objects | /lab-content.html |
| Source | httpd |
| Source Path | /usr/sbin/httpd |
| Port | <Unknown> |
| Host | server.lab.example.com |
| Source RPM Packages | |
| Target RPM Packages | |
| Policy RPM | selinux-policy-3.14.1-59.el18.noarch |
| SELinux Enabled | True |
| Policy Type | targeted |
| Enforcing Mode | Enforcing |
| Host Name | server.lab.example.com |

# 章节 | 管理 SELinux

Linux server.lab.example.com

Platform 4.18.0-67.el8.x86_64

```
#1 SMP Sat Feb 9 12:44:00 UTC 2019 x86_64
```

x86_64
15:19:46 CET

Alert Count 2
First Seen 2019-03-28 15:19:46 CET
Last Seen 2019-03-28
Local ID 8824e73d-d3b0-4caf-8258-86e879fe2d
Raw Audit Messages type=AVC msg=audit(15532876.213:864): avc: denied ( getattr ) for pid=15606 comm="httpd" path="/lab-content/lab.html" dev="vda1" ino=8763212 context=system_u:system_r:httpd_t:s0 context=unconfined_u:object_r:default_t:s0 class=file permissive0
Hash: httpd,httpd_t,default_t, getattr

3. `sealert` 的 Raw Audit Messages 部分包含了来自 `/var/log/audit.log` 的信息。使用 `ause` 命令搜索 `/var/log/audit.log`。`-m` 选项按类型搜索。

# 5 | 管理 SELinux 安全

显示新 HTTP 根目录和原始 HTTP 根目录的 SELinux 上文。解决阻止 Apache 提供内容的 SELinux 问题。

- 4.1 比较 `/lab-content` 和 `/var/www/` 的上下文。

```
[root@serverb ~]# ls -dZ /lab-content /var/www/

un__u:object_r:default_t:s0 system_u:system_t:s0
```

- 4.2 创建一个文件上下文，将 `/lab-content` 及其所有子文件的默认类型设置为 `httpd_content_t`。

```
[root@serverb ~]# semanage fcontext -a -t httpd_content_t '/lab-content/(.*)'
```

- 4.3. 使用 `restorecon` 命令为 `/lab-content` 中的文件设置 SELinux 上文。

```
[root@serverb ~]# restorecon -R /lab-content/
```

- 5 验证 SELinux 问题已解决，且 Apache 能够提供 Web 内容。使用浏览器刷新 http://server/lab.html 链接。现在你应该可以看到一些 Web 内容。

> 这是 SELinux 最终实验的 html 文件

6 退出服务器。

```
[root@serverb ~]# exit

logout

[student@server ~]$ exit

logout

Connection to server closed.

[student@workstation ~]$
```

## 评估

工作站上，运行 `lab selinux-review grade` 脚本确认练习成功。

```
[student@workstation ~]$ lab selinux-review grade
```

## 完成

在工作站上，运行 `lab selinux-review finish` 脚本以完成实验。

```
[student@workstation ~]$ lab selinux-review finish
```

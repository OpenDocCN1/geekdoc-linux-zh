
| 服务器 | `smtp.example.com` |
| 端口 | `587` |

# 完成

账户已成功连接。

消息正在导入。这可能需要一些时间。你可以离开此页面继续工作，甚至关闭浏览器。导入将在后台继续。

当你回来时，所有邮件都会在那里。

如果在导入邮件时发生错误，请阅读（帮助）以获取更多详情。

当我使用邮箱网站的网页界面处理邮件并点击此项时，`firefox` 会尝试在我的浏览器中安装扩展，就像它处理 Google Docs 那样。

看现在 `onlyoffice` 会发生什么

# 步骤 5（可选）：在 onlyoffice 中设置邮箱

请确保你已经访问该账户

| 字段 | 值 |
|---|---|
| 邮箱 | `user@example.com` |
| 密码 | `password` |
| 服务器 | `smtp.example.com` |
| 端口 | `587` |

# 完成

账户已成功连接。

消息正在导入。这可能需要一些时间。你可以离开此页面继续工作，甚至关闭浏览器。导入将在后台继续。

当你回来时，所有邮件都会在那里。

如果在导入邮件时发生错误，请阅读（帮助）以获取更多详情。

此配置设置了 SSL、定义了共享目录并配置了身份验证。

## 7. 将以下内容添加到服务文件中：

```ini
[Unit]
Description=WsgDav WebDAV Server
After=network.target

[Service]
ExecStart=/usr/local/bin/wsgdav --config=/etc/wsgdav/wsgdav.yaml
Restart=always

[Install]
WantedBy=multi-user.target
```

这创建了一个用于自动启动 `WsgDav` 的 `systemd` 服务。

## 8. 为配置文件设置正确的权限：

```bash
sudo chown root:root /etc/wsgdav/wsgdav.yaml
sudo chmod 644 /etc/wsgdav/wsgdav.yaml
```

这使得只有 `root` 用户可以修改配置文件。

## 9. 启用并启动 WsgDav 服务：

```bash
sudo systemctl enable wsgdav.service
sudo systemctl start wsgdav.service
```

这使得服务能够在开机时自动启动并立即运行。

现在，是时候回到之前的 OnlyOffice 窗口来输入 WebDAV 服务器信息了。看到我的路径是 `/webdav` 吗？那是因为

### 3.2 理解文件位置

`WsgDav` 配置文件中的行负责设置从该处开始在我们的系统中可见的目录。显然，如果你的名字不是 `loris`，你的路径也会不同。请根据此进行编辑。

```yaml
provider_mapping: '/webdav': '/home/louis/webdavroot'
```

请记住，`WsgDav` 在启动时仅允许我进入一个目录。我绕过这个限制的方法如下，这样我的 `Documents` 目录和 `androidbackup` 目录就可以可见了：

```bash
ln -s /home/louis/Documents /home/louis/webdavroot
ln -s /home/louis/androidstuff /home/louis/webdavroot
```

现在，我的家目录以及同步所有手机文件的 `androidstuff` 备份目录对所有人可见了！

### 3.3 配置防火墙 (UFW)

`UFW`（简单配置防火墙）为管理 `iptables` 提供了一个用户友好的界面。除了连接我们的 WebDAV 服务器外，不需要任何操作，因此我们将确保只有 `localhost` 可以连接我们的 WebDAV 服务器。

如果你觉得这很荒谬，那么 Office 需要允许我访问本地服务器上已经存在的文件。

1. 允许所有出站流量：

```bash
sudo ufw allow outgoing
```

2. 允许来自特定源的 `8080` 端口入站流量：

```bash
sudo ufw allow from 192.168.5.0/24 to any port 8080 proto tcp
sudo ufw allow from 10.0.0.0/8 to any port 8080 proto tcp
sudo ufw allow from 172.17.0.0/16 to any port 8080 proto tcp
sudo ufw allow from 172.16.0.0/16 to any port 8080 proto tcp
```

这允许仅从特定 IP 范围通过 HTTPS `WsgDav`。

3. 启用防火墙：

```bash
sudo ufw enable
```

这激活了带有配置规则的防火墙。

![](img/63f12be029370b8891d876ebe7b9f412_252_0.png)

## 步骤 4: 确保此工作正常

- 打开 `onlyoffice`，并尝试打开文件

![](img/63f12be029370b8891d876ebe7b9f412_253_0.png)
![](img/63f12be029370b8891d876ebe7b9f412_253_1.png)
![](img/63f12be029370b8891d876ebe7b9f412_253_2.png)

# ONLYOFFICE

请确保你已获得账户访问权限

| 字段 | 值 |
|---|---|
| 邮箱 | `user@example.com` |
| 密码 | `password` |
| 服务器 | `smtp.example.com` |
| 端口 | `587` |

# 完成

账户已成功连接。

消息正在导入。这可能需要一些时间。你可以离开此页面继续工作，甚至关闭浏览器。导入将在后台继续。

当你回来时，所有邮件都会在那里。

如果在导入邮件时发生错误，请阅读（帮助）以获取更多详情。

当我使用邮箱网站的网页界面处理邮件并点击此项时，`firefox` 会尝试在我的浏览器中安装扩展，就像它处理 Google Docs 那样。

看现在 `onlyoffice` 会发生什么

# 步骤 5（可选）：在 onlyoffice 中设置邮箱

请确保你已经访问该账户

| 字段 | 值 |
|---|---|
| 邮箱 | `user@example.com` |
| 密码 | `password` |
| 服务器 | `smtp.example.com` |
| 端口 | `587` |

# 完成

账户已成功连接。

消息正在导入。这可能需要一些时间。你可以离开此页面继续工作，甚至关闭浏览器。导入将在后台继续。

当你回来时，所有邮件都会在那里。

如果在导入邮件时发生错误，请阅读（帮助）以获取更多详情。

## 1.6 设置网络

- 确保连接已设置为桥接模式（Bridge）并与您的局域网网络匹配（例如，`br0`）。这将允许您的虚拟机从现有网络中获取静态 IP。在“网络”设置下，请确保它已设置为桥接模式以实现正确的网络集成。

## 1.7 设置 FreePBX 开机自启

- 输入 `virsh dominfo freepbx` 检查此设置是否正确，并查看 `autostart` 行是否设置为启用（enable）。

- 如果你不执行操作，一旦你重启了服务器（出于某种原因）并离开了家，就会发现为时已晚，你的电话系统失效了。

![](img/63f12be029370b8891d876ebe7b9f412_259_0.png)
![](img/63f12be029370b8891d876ebe7b9f412_259_1.png)
![](img/63f12be029370b8891d876ebe7b9f412_259_2.png)

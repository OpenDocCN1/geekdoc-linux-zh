
以下截图显示了 Nessus 漏洞扫描器的图形用户界面 (GUI)：

![](img/8c6a223c57e25ea0cc1593903a1b920f_394_0.png)

图 13.3 – Nessus 漏洞扫描器的 GUI

好了——现在，让我们深入研究两个最著名的漏洞扫描工具：OpenVAS 和 Nexpose。

## 使用漏洞扫描器 (OpenVAS)

OpenVAS 是目前最著名的开源漏洞扫描器。

该软件主要由 Greenbone networks (www.greenbone.net) 作为开源项目维护，是其商业漏洞解决方案套件的一部分。

该软件能够测试整个网络以发现设备，然后执行多种操作来确定系统的操作系统 (OS)、端口、配置和安装的软件，如下方的截图所示：

使用漏洞扫描器 (OpenVAS)
![](img/8c6a223c57e25ea0cc1593903a1b920f_395_0.png)

图 13.4 – OpenVAS 网络扫描结构

之后，OpenVAS 可以执行若干检查来识别每个已识别组件的漏洞。

## 身份验证测试

OpenVAS 的强大功能之一是能够执行两种类型的测试：未身份验证测试和身份验证测试。

未身份验证测试的侵入性较小，因为它仅根据发现的软件、配置和端口测试通用漏洞。

另一方面，身份验证测试更强大，因为它允许你为测试添加另一个因素——即用户的会话、身份验证和授权。

在这里，OpenVAS 将运行有效的身份凭据（由测试人员提供）来运行本地安全检查 (LSC)，以收集有关目标系统漏洞的更多详细信息。

这里给出了身份验证测试中使用的测试示例：

-   **服务器消息块 (SMB)**：用于检查如 Adobe Reader 或 Java 软件套等系统上的补丁级别和本地安装的软件。
-   **安全外壳 (SSH)**：用于检查 Unix 和 Linux 系统上的补丁级别。
-   **ESX 集成 (ESXi)**：在本地测试 VMware ESXi 服务器。
-   **简单网络管理协议 (SNMP)**：测试路由器和交换机等网络组件。

现在，让我们看看如何在我们的 Kali Linux 机器上安装此工具。

## 安装 OpenVAS

好了——第一步将使用以下命令下载并安装 OpenVAS：

```
sudo apt-get install openvas
```

一旦安装了软件，就是时候使用以下命令执行配置脚本了：

```bash
sudo gvm-setup
```

你遇到错误了吗？

如图所示，有一个与 postgresql 相关的常见错误，但我们将看到如何修复它：

```bash
kali@~$ sudo gvm-setup
ERROR: The default postgresql version is not 13 required by libgvmd
Error: Use pg_upgradecluster to update your postgres cluster
```

图 13.5 – postgresql 错误

该错误的产生是因为有两个版本的 postgresql 同时运行，且 postgresql 使用传输控制协议 (TCP)，正如你所知道的，两个版本不能使用相同的端口。

因此，为了修复这个问题，我们只需要确保版本 13 运行在 TCP 端口 5432 上，然后我们将任何其他可用端口分配给版本 12。操作方法如下。

让我们从打开 postgresql 13 的配置文件开始，如下：

```bash
sudo nano /etc/postgresql/13/main/postgresql.conf
```

在这里，你需要导航到端口并将当前值更改为 5432，如下截图所示：

## 使用漏洞扫描器 (OpenVAS) 375
![](img/8c6a223c57e25ea0cc1593903a1b920f_397_0.png)

然后，使用 Ctrl + O 保存文件并使用 Ctrl + X 退出，如下所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_397_1.png)

下一步是修改 postgresql 12 中的端口并将其设置为 5433，如下：

```bash
sudo nano /etc/postgresql/12/main/postgresql.conf
```

然后，像我们之前的那样，我们需要更改端口，这次从 5432 更改为 5433，如下所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_398_0.png)

图 13.8 – 在 postgresql 12 上更改端口

然后，使用 **Ctrl + O** 保存文件并使用 **Ctrl + X** 退出。

现在，我们只需要使用以下命令重启 **postgresql**：

```bash
sudo systemctl restart postgresql
```

这应该解决问题！

现在，我们可以返回并运行 OpenVAS 配置脚本：

```bash
sudo gvm-setup
```

现在，几分钟后，你应该会看到这样的界面：

![](img/8c6a223c57e25ea0cc1593903a1b920f_399.png)

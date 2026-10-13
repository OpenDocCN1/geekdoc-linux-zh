
```
PLAY [Task Failure Exercise]
************************************

TASK [Gathering Facts]
****************************************************
ok: [servera.lab.example.com]

TASK [Check local time]
**************************************************
ok: [servera.lab.example.com]

TASK [Print local time]
**************************************************
ok: [servera.lab.example.com] => {
  "command_result.stdout": "mié mar 27 09:35 EDT 2019"
}

TASK [Install httpd package]
**************************************************
fatal: [servera.lab.example.com]: FAILED! => {"changed": false, "failed_when_result": true, "msg": "Nothing to do", "rc": 0, "results": "[Installed: httpd"]}

```
TASK [Install mariadb-server package]
************************************
ok: [servera.lab.example.com]
```
```
TASK [Start mariadb-service]
************************************
ok: [servera.lab.example.com]
```
```
PLAY RECAP
****************************************************
servera.lab.example.com : ok=5 changed=0 unreachable=0
failed=1
```
仔细观察输出。`Install httpd package`任务报告失败，但它实际上运行并首先安装了软件包。`failed_when`关键字更改了任务运行后报告的状态；它并没有改变任务本身的行为。

然而，报告的失败可能会改变 play 其他部分的行为。因为该任务位于块中并报告了失败，块的`rescue`部分中的`Install mari-server package`任务被执行了。

## 结束

在 workstation 上，运行`lab control-errors finish`脚本以清理在此练习中创建的资源。

```
[student@workstation ~]$ lab control-errors finish
```

本引导练习结束。

## 实验

# 实现任务控制

## 性能检查清单

在本实验中，你将安装 Apache 服务器并使用 mod_ssl 对其进行安全防护。你将在 playbook 中使用条件、处理程序（handlers）和任务失败处理来部署环境。

## 预期结果

你应该能够在 Ansible Playbooks 中定义条件判断，设置迭代元素的循环，在 playbook 中定义处理程序，并处理任务错误。

## 准备工作

在工作站上以学生身份登录，并运行`lab control-review start`。该脚本确保了被管理的主机（服务器）在网络上是可访问的。它还确保了控制节点上安装了正确的 Ansible 配置文件和清单。

```
[student@workstation ~]$ lab control-review start
```

1. 在工作站上，切换到`/home/student/control-review`项目目录。
2. 项目目录包含一个部分完成的 playbook `playbook.yml`。使用文本编辑器，在`#Fail Fast`注释下添加一个使用`fail`模块的任务。确保为该任务提供适当的名称。此任务仅应在远程系统不满足最低要求时执行。远程主机的要求列如下：
- 内存至少达到`min_ram_mb`变量指定的数量。`min_ram_mb`变量定义在`vars.yml`文件中，值为 256。
- 运行的是 Red Enterprise Linux。
3. 在 playbook 的`#Install all Packages`注释下添加一个任务，以安装任何缺失包的最新版本。所需的包由`packages`变量指定，该变量定义在`vars.yml`文件中。
任务名称应为`Ensure required packages are present`。
4. 在 playbook 的`#Enable and start services`注释下添加一个任务以启动所有服务。由`vars.yml`中定义的`services`变量指定的所有服务都应该被启动并启用。确保为该任务提供适当的名称。
5. 在 playbook 的`#Block of config tasks`注释下添加一个块（block）。该块包含两个任务：
- 一个确保`ssl_cert_dir`变量指定的目录在远程主机上存在的任务。该目录存储 Web 服务器的证书。
- 一个将`web_config_files`变量指定的所有文件复制到远程主机的任务。检查`vars.yml`文件中`web_config_files`变量的结构。配置任务将每个文件复制到远程主机上的正确位置。

如果远程服务器上的这些任何文件发生更改，此任务应触发重启 Web 服务处理程序。

此外，如果上述两个任务任一失败，将执行一个调试任务。在这种情况下，任务将打印消息：`One or more of the configuration changes failed, but the web service is still active.`。
确保为所有任务提供适当的名称。

6. playbook 配置远程主机以监听标准的 HTTPS 请求。在 playbook 的`#Configure the firewall`注释下添加单条任务来配置防火墙。此任务应确保远程主机允许标准的 HTTP 和 HTTPS 连接。这些配置更改应立即生效并在系统重启后依然有效。确保使用重启 Web 服务处理程序。
7. 定义重启 web 处理程序。
当被触发时，此任务应重启由`vars.yml`文件中`web_service`变量定义的 Web 服务。
8. 从项目目录`~/control-review`运行`playbook.yml playbook`。playbook 应在无错误的情况下执行，并触发处理程序任务的执行。
9. 验证 Web 服务器响应 HTTPS 请求，并使用自签名自定义证书加密连接。Web 服务器的响应应匹配字符串`Configured for both HTTP and HTTPS`。

# 评估

在工作站上运行`lab control-review grade`命令以确认本次练习的成功。修正任何报告的失败并重新运行脚本直到成功。

```
[student@workstation ~$ lab control-review grade
```

## 结束

运行`lab control-review finish`命令来清理实验后的环境。

```
[student@workstation ~$ lab control-review finish
```

实验结束。

# 第 5 章 | 实现任务控制

## 答案

# 实现任务控制

## 性能检查清单

在本实验中，你将安装 Apache 服务器并使用 mod_ssl 对其进行安全防护。你将在 playbook 中使用条件判断、处理程序（handlers）和任务失败处理来部署环境。

## 预期结果

你应该能够在 Ansible Playbooks 中定义条件判断，设置迭代元素的循环，在 playbook 中定义处理程序，并处理任务错误。

## 准备工作

在工作站上以学生身份登录，并运行`lab control-review start`。该脚本确保了主机（服务器）在网络上是可访问的。它还确保了控制节点上安装了正确的 Ansible 配置文件和清单。

```
[student@workstation ~]$ lab control-review start
```

1. 在工作站上，切换到`/home/student/control-review`项目目录。

```
[student@workstation ~]$ cd ~/control-review
```

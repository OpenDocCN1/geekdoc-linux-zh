
从应用程序菜单中打开 `GUFW`，确保选择“防火墙配置”。在“配置”框中选择“家庭”。通过向右切换“状态”开关激活防火墙。对于“入”流量，选择“拒绝”。对于“出站”流量，选择“允许”。导航到“规则”部分并点击“+”添加规则。选择“简单”选项卡。在“名称”框中输入“HTTP”。从“策略”下拉菜单中选择“允许”以许可流量。将“方向”设置为“入站”。对于“协议”，根据你配置的端口选择“两者”（`TCP` 和 `UDP`）、仅 `TCP` 或仅 `UDP`。在“端口”字段中输入“80”。点击“添加”应用规则。

这种方法允许你高效地管理 `GUFW` 中的端口规则，确保你的防火墙设置正确。

## GUFW 多端口规则

要在 `GUFW` 中配置多个端口规则，按如下步骤操作：

从应用程序菜单中打开 `GUFW`，确保选择“防火墙配置”。导航到“规则”部分并点击“+”添加规则。选择“简单”选项卡。在“名称”字段中输入描述性名称，例如“HTTP/HTTPS”。从“策略”下拉菜单中选择“允许”以许可流量。将“方向”设置为“入站”。对于“协议”，根据配置的端口选择“两者”（`TCP` 和 `UDP`）、仅 `TCP` 或仅 `UDP`。在“端口”字段中输入你想要允许的端口，用逗号分隔，例如“80,443.”。点击“添加”完成并应用规则。

这种方法使得能够在 `GUFW` 中设置多个端口的防火墙规则，简化了系统网络流量的管理。

## GUFW 端口范围规则

要在 `GUFW` 中实现端口范围规则，请遵循以下指令：

- 从您的应用程序菜单中打开 `GUFW`，确保选择了正确的“防火墙配置”（Firewall Configuration）选项。
- 进入“规则”（Rules）部分并点击 "+" 按钮以创建新规则。
- 在规则创建窗口中，切换到“简单”（Simple）选项卡。
- 在“名称”（Name）字段中为您的规则输入名称，例如“HTTP Range”。
- 从“策略”（Policy）下拉菜单中选择“允许”（Allow）以许可流量。
- 从“方向”（Direction）下拉菜单中选择“入站”（In）以处理入站流量。
- 对于协议，根据您的需要，设置 `TCP` 端口时选择“TCP”，设置 `UDP` 端口时选择“UDP”。
- 点击“添加”（Add）应用并保存您的新端口范围规则。

此方法允许您在 `GUFW` 中高效管理端口范围，便于对您的网络流量权限进行精确控制。

## GUFW 多端口规则与端口范围规则

要在 `GUFW` 中配置多个端口和端口范围的规则，请遵循以下步骤：

- 从您的应用程序菜单中启动 `GUFW`，选择“防火墙配置”（Firewall Configuration）。
- 进入“规则”（Rules）部分并点击 "+" 按钮添加新规则。
- 在规则创建窗口中选择“简单”（Simple）选项卡。
- 在“名称”（Name）字段中输入类似“HTTP”的描述性名称。
- 从“策略”（Policy）下拉菜单中选择“允许”（Allow）以启用流量。
- 将“方向”（Direction）设置为“入站”（In）用于入站规则。
- 对于协议，根据您的要求为 `TCP` 端口选择“TCP”，为 `UDP` 端口选择“UDP”。
- 在“端口”（Port）字段中输入所需的端口和范围，例如，“1111,22:24”。
- 点击“添加”（Add）应用规则。

此过程允许您在 `GUFW` 中轻松管理单个端口和范围，确保您的防火墙配置精确并符合您的网络需求。

## GUFW 从报告添加规则

要在 `GUFW` 中根据报告添加防火墙规则，请遵循以下指令：

- 从您的应用程序菜单中打开 `GUFW`，确保您选择了“防火墙配置”（Firewall Configuration）。
- 导航到“报告”（Report）部分。
- 从列表中选择一个规则编号。
- 点击 "+" 按钮开始添加规则。
- 点击“添加”（Add）进行确认。

此方法允许您直接从 `GUFW` 报告高效地实施防火墙规则，简化管理网络安全设置的流程。

## GUFW 移除端口规则

要在 `GUFW` 中删除端口规则，请按照以下步骤操作：

- 从您的应用程序菜单中打开 `GUFW`，确保选择“防火墙配置”（Firewall Configuration）。
- 导航到“规则”（Rules）选项卡。
- 通过选择其编号来高亮显示您想要删除的规则。
- 点击 "-" 按钮删除该规则。

> 请在删除之前双重检查您是否选择了正确的规则，因为 `GUFW` 在移除规则时不会提示确认。

## ClamAV

访问 `ClamAV` 官方网站 `https://www.clamav.net/` 了解所有关于 `ClamAV` 的信息。

在终端中通过 `APT` 安装 `ClamAV`：

只需输入这些命令：

```bash
sudo apt update
sudo apt install clamav clamav-daemon
```

## clamd .conf 命令行与 GUI 设置

要通过命令行和 GUI 配置 `clamd`，请遵循以下步骤：

在终端中执行以下命令打开 `clamd` 配置文件：

```bash
sudo gedit /etc/clamav/clamd.conf
```

从 `OnAccessMaxFileSize` 行开始更新 `clamd.conf` 文件：

```bash
OnAccessMaxFileSize 101M
ScanOnAccess yes
OnAccessIncludePath /
OnAccessExcludePath /home/.wine/mnt
OnAccessPrevention yes
```

点击“保存”（Save）保存您的更改。

接下来，为 `clamd` 运行设置必要的环境：

使用以下命令创建 `clamav` 目录：

```bash
sudo mkdir /run/clamav
```

设置目录权限以允许读取、写入和执行：

```bash
sudo chmod 777 -R /run/clamav
```

启动 `clamd` 服务：

```bash
sudo clamd
```

启动 `clamd` 后，通过将权限改回来保护目录：

```bash
sudo chmod 755 -R /run/clamav/
```

## ClamAV 自动更新与扫描

要在 `ClamAV` 设置自动更新和扫描，请在终端中遵循以下步骤：

打开 `crontab` 文件进行编辑：

```bash
sudo crontab -e
```

在提示时选择 `nano` 编辑器编号。

在 `crontab` 文件中添加以下行以配置计划任务。

每天晚上 11:00 更新 `ClamAV` 数据库：

```bash
0 23 * * * /usr/bin/freshclam
```

每天午夜针对特定目录进行扫描、记录过程并移除任何检测到的感染文件：

```bash
0 0 * * * /usr/bin/clamscan --log --infected --remove -r /home /usr /etc /bin /sbin
```

按 `CTRL` + `S` 保存更改，并按 `CTRL` + `X` 退出。

此设置确保了您的 `ClamAV` 数据库定期更新，并且您的系统每天都会扫描威胁，从而增强您的安全措施。

## ClamTk

访问 `ClamTk` 官方网站 `https://github.com/dave-theunsub/clamtk` 了解所有关于 `ClamTk` 的信息。

通过软件管理器安装 `DEB`/`FLATPAK` 软件包：

- 打开软件管理器并搜索 `ClamTk`。

（注：由于源文件中 `ClamTk` 的 OCR 文本似乎是碎片化的，遵循保留所有信息的指令进行。）

启动安装脚本：

```bash
sudo ./install.sh
```

在安装过程中，你将遇到多个提示。请按照以下说明操作：
- 输入 `en` 并按回车键选择英语。
- 输入 `local` 选择本地安装类型，并指定安装路径为 `/var/ossec`。
- 第一个问题回答 `n`，后续问题回答 `y` 以接受默认设置。
- 在最后按回车键确认你的选择。

此步骤将引导你高效地在系统中设置好 `OSSEC`。

## OSSEC Systemd 服务

首先，打开终端并输入以下命令来编辑 `OSSEC` 服务文件：

```bash
sudo gedit /etc/systemd/system/ossec.service
```

在 `ossec.service` 文件中，插入以下配置：

```ini
[Unit]
Description=OSSEC service
After=network.target

[Service]
Type=simple
ExecStart=/var/ossec/bin/ossec-control start
ExecStop=/var/ossec/bin/ossec-control stop
TimeoutStartSec=0
Restart=on-failure
StartLimitInterval=0

[Install]
```

要保存更改，点击“保存”（Save）按钮。

接下来，在终端中执行这些命令以启用、启动并检查 `OSSEC` 服务状态：

```bash
sudo systemctl enable ossec.service
```

```bash
sudo systemctl start ossec.service
```

```bash
sudo systemctl status ossec.service
```

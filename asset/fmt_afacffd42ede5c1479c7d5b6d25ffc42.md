
# 自我管理生活入门指南：FUTO software 的 13 小时 28 分钟演示

## 为什么不用 Intel 网卡？

更好的替代方案：重用旧台式电脑

- 选择网络接口卡 `NICs`
- 购买网卡的注意事项
- 不要买 Diginom

### 第 1 步：下载 `pfSense` 并准备可启动的 USB 盘

- 1. 下载 `pfSense`
- 2. 解压下载的 `pfSense` 文件
- 3. 使用 `pfSense` 镜像创建可启动 USB 盘

支持 Windows、Linux 或 macOS：

### 第 2 步：禁用安全启动并在 Intel 网卡上安装 `pfSense`

- 1. 在 BIOS 中禁用安全启动

### 第 3 步：在 Intel 网卡上安装 `pfSense`

- 从 USB 闪盘启动

  1.1 Intel 网卡

  1.2 在启动菜单中选择 USB 盘

开始 `pfSense` 安装

  2.1 `pfSense` 安装菜单

  2.2 选择安装方法

选择正确的安装驱动器

- 3.1 选择内部 SSD 或硬盘

3.2 确认擦除并安装

完成安装并重启

- 4.1 移除 USB 闪盘

4.2 重启并加载 `pfSense`

### 第 4 步：`pfSense` 首次配置

- 1. 连接并启动 `pfSense`

  1.1 连接你的设备：

  1.2 开机并观察启动过程：

  2. 初始配置步骤

  2.1: VLAN 设置提示

  2.2: VLAN 设置提示

  2.3: WAN 和 LAN 接口分配

  3. 配置 LAN IP 地址

  3.1: 默认 LAN IP

  3.2 更改 LAN IP（可选）

  3.3 DHCP 设置

  4. 完成

- 5. 进入 `pfSense` Web 界面

  5.1: 初始 Web 设置向导

6. 最终检查并准备后续步骤

# 为 FreeDNS 设置动态 DNS `DDNS`

为什么你需要动态 DNS？

设置 `FreeDNS`

- 第 1 步：注册 `FreeDNS`

1.1 创建 `FreeDNS` 账户

1.2: 登录 `FreeDNS` 并创建订阅

1.3 从 `FreeDNS` 获取更新 URL

1.4 保持 `FreeDNS` 页面打开并确保它对你来说是错误的 IP：

## 第 2 步：为 `pfSense` 配置动态 DNS

- 2.1 登录 `pfSense`

2.2 进入动态 DNS 设置

2.3 输入动态 DNS 条目

## 第 3 步：查看动态 DNS 是否实际生效

验证 DNS 解析

为什么这很重要

# OpenVPN：从任何地方建立安全访问

- 为什么用 `OpenVPN`？我为什么需要这个？

列出我们必须开放的端口

为什么开放所有端口比 820-230 MacBook Macbook 的合页设计更愚蠢

`OpenVPN`：仅需开放 1 个端口，且安全性更高：

四张图说明 VPN 安全性：

使用 `OpenVPN` 减少攻击面是最佳实践

在 `pfSense` 中设置 `OpenVPN` 以实现安全访问

- 第 1 步：在 `pfSense` 中安装 `OpenVPN` Client 导出包

1.1 登录 `pfSense`：

## 第 2 步：设置证书

2.1 - 创建一个证书

2.2 - 创建证书颁发机构 `CA`

2.2 - 创建 `OpenVPN` 服务器证书

2.3 - 为你的 VPN 用户创建一个 VPN 组

2.4 创建一个 VPN 用户

- 第 3 步：配置 `OpenVPN` 服务器

3.1 配置 `OpenVPN` 向导，并根据下文 3.2 节及上文内容进行设置

3.2 `OpenVPN` 服务器配置

- 第 4 步：获取 `.ovpn` 文件以连接 VPN

4.1 为你的 Android 设备导出 `OpenVPN` 客户端配置

4.2 将配置导入到 Android 设备

配置 Android 设备以连接 VPN

IPv4 与 IPv6

配置 `pfSense` 的安全访问

# 本地安装媒体

## 第一步：设置虚拟机管理器 `virsh`

- 1.0 创建新虚拟机

- 1.1 选择安装媒体

- 1.2 选择操作系统版本

- 1.3 配置内存和 CPU

- 1.4 配置存储

- 1.5 使用网桥接口设置网络

- 1.6 完成并定制化为虚拟机

## 第二步：作为虚拟机安装 Ubuntu Server

- 2.1 在虚拟机中启动安装过程

- 2.2 配置静态 IP 地址

- 2.3 分区虚拟“驱动器”

- 2.4 完成安装且不安装 docker

## 第三步：安装后任务

- 3.1 移除光驱驱动器 `CDROM`

- 3.2 在 `pfSense` 中设置静态 IP 映射；

- 3.3 设置此虚拟机随随机自启动：

# 在 Mailcow 中使用 SoGo 管理日历与联系人

## 前提条件

- 对于自托管日历与联系人：

- 对于自托管电子邮件

- 准备 Ubuntu Server

## 第一步：安装 Docker

- 1.1 更新并升级你的系统

- 1.2 检查其他 Docker 安装情况：

- 1.3 使用官方 Docker 脚本安装 Docker：

- 1.4 安装 Docker Compose：

- 1.5 验证安装情况

- 1.6 设置正确的权限：

## 第二步：安装 mailcow

- 2.1 克隆 `mailcow` 仓库

- 2.2 设置正确的权限文件

- 2.3 生成配置文件

- 2.4 启动 `mailcow` 服务

## 第三步：访问并配置 mailcow

- 3.1 访问 Web 

- 3.2 使用默认凭据登录

- 3.3 修改管理员密码

- 3.4 添加域名

- 3.5 添加邮箱账户

## 第四步：访问日历/联系人服务

## 第五步：使用 DAV+ 将安卓 与 mailcow 同步

- 5.1 在安卓手机上安装 `DAVX+`

- 5.2 使用 `OpenVPN` 在安卓上安装自带的日历 App

- 5.3 确保安卓手机的 `OpenVPN` 连接保持连接状态

- 5.4 在手机的 `DAVX+` 中添加 `Mailcow`

- 5.5 调整同步设置

## 第六步：使用 Mailcow 与安卓管理联系人

- 6.1 在安卓中找到你的新 `Mailcow` 联系人账户

- 6.2 在 `Mailcow` 中添加联系人并在安卓上进行验证

- 6.3 从旧通讯录中导出联系人

- 6.4 将联系人导入你的新邮箱地址通讯录

- 6.5 在邮箱 Web 界面中验证联系人

## 第七步：设置并使用你的邮箱日历

- 7.1. 使用与 `DAVX` 同步的邮箱日历配置 Fossility 日历 App

- 7.2 在安卓日历 App 中添加事件并在邮箱中验证

- 7.3 在邮箱中添加事件并在安卓上验证

- 7.4 刷新日历数据

日历 App 中的刷新按钮不是真实的

为什么工作原理是这样运行的？

# 使用 Mailbox & Postmark 管理邮件

为什么我需要 SMTP 继继？

## 第一步：设置 Postmark 作为 SMTP 继继

- 1. 创建 `Postmark` 账户

- 2. 创建新服务器

- 3. 配置消息流 `Message Streams`

- 4. 获取 SMTP 继继凭据

## 第二步：配置 Postmark 使用 SMTP 继继

- 2.1. 访问 `Mailbox` 管理界面

- 2.2 找到 SMTP 继继部分

- 2.3. 输入 `Postmark` SMTP 详情

## 第三步：在 Mailbox 中添加域名和邮箱

- 3.1. 添加域名

- 3.2 将 `Postmark` 设置为继继

- 3.3 添加邮箱账户

- 3.4 保存更改并应用

- 3.5. 访问 `SoGo` Wemail/日历/联系人 

## 第四步：在你的域名注册商处设置 DNS 记录

域名注册商简介

什么是域名注册商？

以 `Namecheap.com` 为例

在 `Namecheap` 中配置 DNS 记录

- 4.1. 找到你域名的 DKIM 相关项

- 4.2. 在 `Namecheap` 中配置 DNS 记录

  - CNAME 记录

  - DMARC 记录

  - DKIM 记录 `TXT`

  - `Postmark` DKIM 记录 `TXT`

  - 你域名的 DKIM 记录 `TXT`

  - SPF 记录 `TXT`

  - 邮件 CNAME 记录

  - 客户端配置 CNAME 记录

- 4.3. 返回 `Postmark` 并验证你的 DNS 记录。

## 第五步：`pfSense`

### 第一节：`pfSense` 中的别名 `Aliases`

什么是 `pfSense` 中的别名？

实际应用示例：

使用别名的益处

搞鬼？设置 `OpenVPN` 是为了我们**不**开启端口；我们为什么在讨论开启端口？

如何在 `pfSense` 中设置别名

- 5.1.1. 访问别名列表

- 5.1.2. 创建别名

- 5.1.3. 在防火墙中使用别名

使用别名进行安全访问

### 第二节：为邮件服务器设置 `pfSense` 防火墙规则

理解 NAT `网络地址转换`

防火墙规则

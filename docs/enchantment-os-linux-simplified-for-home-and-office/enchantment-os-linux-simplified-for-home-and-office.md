# Enchantment OS：家庭与办公极简版 Linux





















# XFCE




```bash
bash-2.05b$ pwd
/home/dstone
bash-2.05b$ cd /usr/app-shells/bash
bash-2.05b$ ls -al
total 60
drwxr-xr-x 3 root root 4096 May 14 12:05
drwxr-xr-x 26 root root 4096 May 17 02:36
drw-rw-xr-x 1 root root 13710 May 03 22:35 Changelog
drw-rw-xr-x 1 root root 14128 May 14 12:05 Manifest
drw-rw-xr-x 1 root root 3720 May 14 12:05 bash-2.05b-r11.ebuid
drw-rw-xr-x 1 root root 3516 May 21 20:05 bash-2.05b-r9.ebuid
drw-rw-xr-x 1 root root 25536 May 14 12:05 bash-3.0-r11.ebuid evendrw-rw-xr-x 1 root root 4038 May 14 12:05 bash-3.0-r7.ebuid
drw-rw-xr-x 1 root root 3931 May 14 12:05 bash-3.0-r8.ebuid
drw-rw-xr-x 1 root root 3998 May 14 12:05 bash-3.0-r9.ebuid
drwxr-xr-x 2 root root 4096 May 13 22:35 files
drwxr-xr-x 1 root root 164 Dec 29 2003 nodata.xml
bash-2.05b$ cat version.xml
<?xml version="1.0" encoding="UTF-8"?>
<pkgnedata SYSTEM "http://www.gentoo.org/dtd/nodata.dtd">
<pkgnedata>
<chardbase-system-herd>
</pkgnedata>
bash-2.05b$ sudo /etc/init.d/bluetooth status
Password: * stopped
bash-2.05b$ ping -c 6 en.wikipedia.org
PING en.wikipedia.org (172.102.141.54): 56(84) bytes of data.

--- en.wikipedia.org ping statistics
6 packets transmitted, 6 received, 0.0% packet loss, time
rtt min avg/max/mdev = 112.076/112.076/112.078/0 ms
bash-2.05b$ grep -i /dev/sda /etc/fstab | cut --fields=3
/dev/sda1
bash-2.05b$ ls /dev/sda
/dev/sda1  /dev/sda2
bash-2.05b$ date
Wed May 25 11:36:56 PDT 2005
```




请选择启动设备：
SATA:PM-PLEXTOR PX-64M1S
USB:Verbatim TUFF

↑ 和 ↓ 移动选择
ENTER 选择启动设备
ESC 使用默认设置启动


# Enchantment
简化的 Linux

Enchantment OS，基于 Xubuntu 16.04 LTS

使用 Linux：保存文件（持久性 USB 驱动）
尝试 Linux：文件不保存（DVD 或 USB）
在硬盘上安装 Enchantment Linux


```
GNU GRUB 版本1
Ubuntu
Ubuntu 的高级选项
内存测试 (memtest86+)
内存测试 (memtest86+, 串口 con
```












# #软件

Enchantment 有大量的软件可用，这是针对 Ubuntu 的精选软件集合。如果您没有找到想要的内容，请检查软件中心。

| 许可证 | 来源 |
| --- | --- |
| 开源 | 32-bit 64-bit aarch3(ARM7) PowerPC |
| 类别 | 解码器 |
| 来源 | Ubuntu |






# Samba 用户

kelley

- 添加用户
- 编辑用户
- 删除用户

## 创建新 Samba 用户

Unix 用户名：kelley
Windows 用户名：kelley
Samba 密码：********
确认 Samba 密码：********

确定
取消
确定

## 创建 Samba 共享

基本访问

目录：/home/kelley/Pictures [浏览...]
共享名称：Pictures
描述：我的照片

- 仅允许特定用户访问
- kelley
- 可写
- 可见
- 允许所有人访问

确定

取消
确定
取消

## Pictures

家目录
- Pictures
  - (空)
- Videos
  -  下载 (Downloads)
- 计算机
  - WDC WD100S12X-555JTETO: home:1000
- JetFlash Transcend 16GB: Transcend
- SD02G: 2.0 GB 卷
- 目录
- 选择

显示：全部
13 个文件 (4.3 MB) · 剩余 78.5 GB 空间

## Transcend - 文件管理器

/media/kelley/Transcend/

| 名称 | 大小 | 类型 | 修改日期 |
| :--- | :--- | :--- | :--- |
| Pictures | 8.2 kB | 文件夹 | 2016-06-26 16: |

- 文件系统
- home1000
- linux64
- uefi
- Transcend
- 2.0 GB 卷
- kelley
- 桌面
- 垃圾箱

1 个项目，可用空间：15.8 GB

| ID | 属性 | 值 | 归一化 | 阈值 | 最差 | 类型 | 状态 | 评估 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 读取错误率 | 0 | 200 | 51 | 200 | 故障前 | 在线中 | OK |
| 3 | 启动时间 | 1 秒 | 188 | 21 | 187 | 故障前 | 在线中 | OK |
| 4 | 启动/停止次数 | 34 | 100 | 0 | 100 | 老化 | 在线中 | OK |
| 5 | 重映射扇区计数 | 0 扇区 | 200 | 140 | 200 | 故障前 | 在线中 | OK |
| 7 | 寻道错误率 | 0 | 200 | 0 | 200 | 老化 | 在线中 | OK |


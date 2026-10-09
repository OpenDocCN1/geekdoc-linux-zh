

## X 终端
一种专为运行 X 窗口系统而设计的图形终端。

## X 窗口系统
一套用于编写灵活、可移植窗口应用程序的设计和工具集，由 MIT 的研究人员与几家主要计算机制造商共同创建。

## XDMCP
X 显示管理器控制协议（X Display Manager Control Protocol）。XDMCP 允许登录服务器接受来自网络显示器的请求。许多 X 终端都内置了 XDMCP。

## xDSL
不同类型的 *DSL*（第 1147 页）通过前缀来标识，例如 ADSL、HDSL、SDSL 和 VDSL。

## Xinerama
X.org 的一个扩展。Xinerama 允许窗口管理器和应用程序将两个或更多物理显示器作为一个大型虚拟显示器使用。请参阅 Xinerama-HOWTO 文档。

## XML
可扩展标记语言（Extensible Markup Language）。一种用于 Web 上结构化文档和数据的通用格式。XML 由 *W3C*（第 1180 页）开发，是 *SGML* 的简化版本。参见 www.w3.org/XML 和 www.w3.org/XML/1999/XML-in-10-points。

## XSM
X 会话管理器（X Session Manager）。该程序允许您创建一个包含特定应用程序的会话。在会话运行期间，您可以执行 *检查点*（保存应用程序状态）或 *关机*（保存状态并退出会话）。当您重新登录时，可以加载您的会话，使会话中的所有程序恢复到您注销时的运行状态。

## Z Shell
*zsh*。一种 *shell*（第 1171 页），它融合了 *Bourne Again Shell*（第 1138 页）、*Korn Shell*（第 1156 页）和 *TC Shell*（第 1176 页）的许多特性，同时具备许多独创功能。

## Zulu 时间
参见 *UTC*（第 1179 页）。

# 快速入门索引

## A
- Apache：启动和运行 Apache 903
- APT：使用 aptitude 安装和移除软件包 519

## C
- CUPS：配置本地打印机 549
- CUPS：使用 CUPS Web 界面设置本地或远程打印机 555

## D
- DNS：设置 DNS 缓存 834

## F
- firestarter：使用防火墙向导配置防火墙 867
- FTP：使用 ftp 下载文件 690
- FTP：启动 vsftpd FTP 服务器 700

## M
- Mail：配置 exim4 以发送和接收邮件 718
- Mail：配置 exim4 以使用智能主机（Smarthost） 716
- MySQL：设置 MySQL 629

## N
- NFS：使用 shares-admin 配置 NFS 服务器 783–785
- NFS：挂载远程目录层次结构 777–780

## O
- OpenSSH：启动 OpenSSH 服务器 677
- OpenSSH：使用 ssh 和 scp 连接 OpenSSH 服务器 667

## S
- Samba：使用 system-config-samba 配置 Samba 服务器 800

# 文件树索引

浅色页码（例如 456）表示简要提及。

- /bin 213
  - echo 995
  - false 495
- /boot 38, 213, 582, 583, 613
  - grub
    - grub.cfg 447, 587
    - menu.lst 584
- /dev 213, 244, 488, 502
  - disk
    - by-path 489
    - by-uuid 489
  - fd0 488
  - hda 489
  - null 250, 489, 622, 973
  - pts 490
  - random 490
  - sda 489
  - tty 1008
  - urandom 490
  - zero 491
- /etc 214
  - aliases 619, 722
  - alternatives 491
  - anacrontab 402, 607
  - apache2
    - apache2.conf 906, 932–934
    - conf.d 908
  - envvars 908
  - httpd.conf 908
  - mods-available 905, 907
  - mods-available/alias.conf 907
  - mods-enabled 905, 908
  - ports.conf 908
  - sites-available 906, 908
  - sites-available/default 934
  - sites-enabled 906, 908
  - apt
    - apt.conf 524
    - apt.conf.d 524
    - sources.list 523
  - at.allow 491
  - at.deny 491
  - auto_master 793
  - bash.bashrc 492
  - bashrc 294
  - bind 836, 841
  - db.127 844
  - db.local 843
  - db.root 841
  - named.conf 836, 839–841, 851, 856
  - named.conf.options 841
  - cacti
    - apache.conf 651
    - debian.php 651
  - cron.allow 491
  - cron.d 403, 606, 607
  - cron.daily 607
  - cron.deny 491
  - cron.monthly 607
  - cron.weekly 607
  - crontab 403, 606
  - cups
    - cupsd.conf 565
    - ppid 563
  - default
  - default 492
    - autofs 794
    - bind9 834
    - dhcp3-server 473
    - exim4 724
    - grub 584-586
    - nis 746, 751, 757
    - snmpd 655
  - defaultdomain 745, 746
  - dhcp3
    - dhclient.conf 472
    - dhcpd.conf 473, 474
  - dovecot
    - dovecot.conf 735
  - dumpdates 492, 603
  - exim4.dirty1 439
  - exim4 724
    - exim.crt 736
    - exim.key 736
  - exim4.conf.localmacros 737
  - update-exim4.conf.conf 724
  - exports 783, 786-789
  - firestarter 866
  - fstab 507, 710, 778, 781
  - ftpusers 711
  - gustomb.conf 271
  - PreSession 449
  - group 492, 598, 1082
  - grub.d 586
  - hostname 493
  - hosts 386, 493
  - hosts.allow 463, 465-466
  - hosts.deny 463, 465-466
  - hosts.equiv 391, 1119
  - init 434, 438
  - init.d 440
  - naacron 607
  - apache2 901
  - init
  - control-alt-delete 451
  - rc.conf 438, 445
  - rc5.conf 445
  - rc-sysinit.conf 439
  - inittab 439, 493
  - issue 147
  - ldap
    - schema 758
    - slapd.d/cn=config 761
  - lftp.conf 674
  - login.defs 494, 597
  - logrotate.conf 622-624
  - logrotate.d 622, 624
  - magic 500
  - mainlan
  - mm_cfg.py 735
  - mainlane 718
  - motd 494, 615
  - mtab 494
  - nologin 495
  - nologin.txt 481
  - nsswitch.conf 475-477, 742
  - ntp.conf 404
  - opt 214
  - pam.d 478
  - passwd 448, 494-495
  - printcap 495
  - profile 294, 495
  - protocols 495, 888
  - rc.local 441
  - rcn.d 440-443
  - resolv.conf 496, 834, 835
  - rpc 496
  - rsyslog.conf 626-627
  - samba
  - smb.conf 804, 807-814
  - smbusers 799
  - security 421
  - security
    - access.conf 421
  - services 402, 497
  - shadow 448, 497
  - shells 457
  - skel 597
  - ssh 665
  - ssh
    - ssh_config 674
    - ssh_known_hosts 668–670
    - sshd_config 679
  - ssl
  - s1svftpd.pem 710
  - sudoers 426–431
  - termcap 1176
  - ufw
  - applications.d 874
  - vsftpd.banned_emails 703
  - vsftpd.conf 701
  - vsftpd.user_list 702, 711
  - X11 214
  - yp.conf 747
  - ypserver.conf 751
- /home 39, 214
  - ftp 700, 703, 705
- /lib 214
  - modules 214, 580
  - security 478
- /lost+found 488
- /mnt 214
- /opt 39, 214, 541
- /proc 214, 497
  - mounts 494, 790
  - sys 572
- /root 214
- /sbin 214
- /srv
  - ftp 700, 703, 705
- /sys 214, 499
- /target 36, 84
- /tmp 214, 983
- /usr 39, 214
  - bin 214
  - tppasswd 907
  - test 956
  - games 214
  - include 214
  - lib 214
    - cgi-bin 908
    - terminfo 1176
  - local 39, 214, 542
  - pub
    - ascii 1135
  - sbin 214
    - apache2 907
    - apache2ctl 907
    - nologin 495
    - rotatologs 907
  - share 214
    - sharecertor 908
    - shareicons 908
    - doc 143, 215, 408, 616, 1100
    - shareapache2-doc/condex.html 908
    - file
    - sharemagick 500
    - info 215
    - magic 1158
    - man 215
    - ppd
    - sharecuston 563
    - recovery-mode 447
  - src 215
    - linux 575
    - srcDocumentation 143
- /var 38, 215
  - cache
  - apt
  - cachearchives 524, 533
  - exim4
  - mainlog 720
  - lib
  - apt
  - liblist 524
  - dhcpc3 472
  - dpkg
  - libavailable 533, 534
  - libvatcus 533
  - exim4
  - libconfig.autogenerated 724
  - libDB_CONFIG 760
  - named 847
  - libetc
  - lib_bind 836
  - nfs
  - libeatbf 789
  - libratmbat 790
  - log 39, 215, 500, 626, 1100
    - apache2 908
    - logaccess.log 908
    - loggermon.log 908
    - apitude 526
    - auth.log 500, 1100
    - messages 500, 617, 1100
    - syslog 849
    - vsftpd.log 708, 711
    - wtmp 623
  - mail 720
  - name 321
  - spool 215, 1100
  - cron
    - spoolcronTabs 403, 606
  - www 902, 905, 909
  - YP
  - Makefile 753
  - nicknames 743
  - nisdomainname 743
  - securenets 753
- ~/ （用户的主目录）
  - .bash_history 330
  - .bash_login 294
  - .bash_logout 294
  - .bash_profile 294, 331, 351, 488
  - .bashrc 294, 488
  - .cshrc 1143
  - .dmrc 449
  - .forward 723
  - .inputrc 343
  - .login 1158
  - .logout 1158
  - .netrc 694
  - .pgpkey 182
  - .plan 182
  - .profile 294, 1166
  - .project 182
  - .rhosts 391
  - .ssh/config 674
  - .ssh/known_hosts 668-670
  - .toprc 610

# 实用工具索引

浅色页码（例如 456）表示简要提及。后跟字母 t 的页码指表格。

- **符号**
  - . （点） 296, 1007
  - : （null/空值） 1002, 1011
  - [[...]] 1018

- ash *参见 dash shell*
- aspell 971
- at 403, 491, 608
- awk *参见 mawk*

## A
- a2dismod 905
- a2dissite 906
- a2enmod 905
- a2ensite 906
- a2enstite 906
- a2cton 1120
- a2dduser 597
- AIDE 1119
- alias 346
- amanda 600
- anacron 607
- anacrontab 402
- apache2ctl 903, 940
- apropos 139, 437
- apt-cacher 530
- apt-file 521
- apt-get *参见 aptitude*
- aptitude 519–520, 526–529, 573

## B
- basename 982
- bash *参见主索引中的 bash（第 1195 页）*
- bg 255, 309
- bind 344
- btdownloadcurses 540
- btshowmetainfo 541
- buildins 1015t
- bunzip2 175
- bzcat 175
- bzip2 174, 602
- bzjrep2recover 175

## C
- cancel 559
- cat 162, 245, 247, 960
- cd 209, 231, 324
- chrootkit 1124


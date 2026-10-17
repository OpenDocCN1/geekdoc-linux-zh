
A T1 connection is a high-speed (1544 Kbps) and expensive digital connection that can handle 300 or more concurrent users—sufficient for all but the busiest sites. You can also get fractional T1 service, which provides either 256 or 512 Kbps for less than the cost of a full T1 connection. T1 connections typically require the installation of a router (a piece of hardware that the T1 line plugs into).

One alternative to a router is the RISCom/N2 adapter card from SDL Communications (http://www.sdlcomm.com), which allows you to plug a full or fractional T1 line directly into a Linux box. This card is much cheaper than other alternatives and has great performance.

# ONSITE ISP CONNECTION

An onsite ISP connection requires no phone line, because your computer resides at your ISP's place of business. In this case, your Linux system is cabled directly into the ISP's ethernet network, and you have T1 access. The downside is that you don't have physical access to your computer, so you have to log in via Telnet.

# SETTING UP YOUR WEB SITE

Red Hat Linux comes with the very popular Apache Web (`httpd`) server. Prior to the Red Hat 6.1 release, Apache was included in the default set of packages selected by the install program. But in the current version you have to explicitly install it from the CD. Refer to Chapter 14, "Updating Your Linux System," for help on using `GNOPRM` to install Apache. After installing, you must logout and login again to get the Apache server running. To test Apache, start the Lynx browser and display the default Web page, which is stored as `index.html` in the `/home/httpd/html` directory. Of course, you'll want to create your own home page, so edit the `index.html` file to suit your needs, and you're in business.

If you want other Internet users to connect to your Web server, you'll have to provide them with your IP address and tell them to connect with a URL like this:

`http://205.161.119.112`

The IP address comes from the `ifconfig` command, but remember that it changes each time you connect to your ISP, unless you've arranged for a static IP address or obtained your own domain name, as discussed earlier.

The default Apache configuration files in the `/etc/httpd/conf` directory will work fine for most people, but if you're curious about ways to change the behavior of the server, have a look at the other files in this directory. Refer to the Apache home page at http://www.apache.org for help.

# HELP WITH LINUX NETWORKING

If you run into trouble establishing your dial-up connection, or if you have questions about Linux networking, visit the Linux Documentation Project home page on the Web at http://sunsite.unc.edu/mdw/linux.html to find the `Net-2-HOWTO`, `PPP-HOWTO`, and `Serial-HOWTO` files.

本网站还托管了一份非常全面的文档，名为《Linux 网络管理员指南》，其中详细介绍了 SLIP 和 PPP 连接、设置系统以允许他人拨入，以及应遵循的安全相关程序。

你也可以在 Red Hat 的“PPP Setup Tips”文档中找到一些有用的提示，网址为 http://support.redhat.com/docs/PPP-Client-Tips/PPP-Client-Tips.html。

这些文档将有助于回答你可能对 Linux 网络提出的任何问题，如果你在使用 PPP 连接时遇到困难，或者计划允许他人通过 PPP 连接到你的 Linux 机器，我强烈推荐阅读它们。

# LIVING IN A SHELL

## Logging In 95

## Bash (and Other Shells) 99

## Linux Commands 99

要使用 Linux——或者任何类 Unix 系统——你需要了解一些关于 shell 的知识。Shell 是一个充当你与操作系统核心之间中介的程序。在 DOS 环境中，`command.com` 充当你的 shell。Linux shell 有更有趣的名字（如 `bash`、`pdksh` 和 `tcsh`），但它们做的事情基本相同。除了将你的命令翻译成内核可以理解并执行的形式外，shell 还增加了一些基本操作系统不提供的功能。

使用 Linux shell 意味着使用命令行，这与从 DOS 提示符工作非常相似。你已经在上一章中了解了 X Windows 环境和 GNOME 图形界面，但某些 Linux 任务只能从命令行完成。本章中你将获得的关于 Linux 如何工作的知识，将为你成功高效地使用 Linux 提供基础。以下是所有 Linux shell 的基本功能描述、它们执行的功能预览，以及本章你将学习的内容概述。

**Prompts** 提示符是 shell 在准备接收新命令时显示的一个字符或一串字符（如 `$` 或 `#`）。你将了解不同类型的提示符以及如何根据自己的工作方式对其进行自定义。

**Command resolution** 当你输入命令时，shell 必须确定要运行哪个程序来执行该命令。你将学习 shell 如何做到这一点，以及如何更改命令解析过程以满足你的需求。

**Job control** Linux 允许多任务处理（同时运行多个命令）。你将学习如何启动、列出和停止任务；你还将了解前台和后台任务执行之间的区别。

**Command history and completion** 当你输入大量命令时，有时你想重复上一个命令或发出类似的命令。你将学习如何召回和修改以前输入的命令，以及了解一些键盘快捷键，可以自动为你补全命令。

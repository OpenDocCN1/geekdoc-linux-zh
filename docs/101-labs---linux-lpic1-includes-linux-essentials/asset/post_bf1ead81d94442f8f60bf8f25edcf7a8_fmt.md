
### 5. Please DO NOT attempt to configure these labs on other Linux distros.

We’ve chosen `Ubuntu` (`18.04 LTS`) for the labs due to the fact it’s the most popular Linux distribution among the top 1000 sites and gains around 500 of the top 10 million websites per day.

### 6. You MUST be reading or have read a Linux study guide or watched a theory video course.

Apart from some configuration tips and suggestions, we don’t explain much theory in this book; it’s all hands-on labs.

### 7. It’s impossible for us to give individual support to the thousands of readers of this book (sorry!), so please don’t contact us for tech support.

Each lab has been tested by several tech editors from beginner to expert.

## ALSO FROM REALITY PRESS LTD.

- `Cisco CCNA Simplified`

- `Cisco CCNA in 60 Days`

- `IP Subnetting—Zero to Guru`

- `101 Labs—CompTIA A+ (due 2019)`

- `101 Labs—CompTIA Network+`

- `101 Labs—IP Subnetting`

- `101 Labs—Cisco CCNP`

- `101 Labs—Cisco CCNA`

- `101 Labs—Wireshark WCNA (due 2019)`

## TECHNICAL EDITORS

Thanks to all the tech editors who donated their time to check all the labs and give feedback.

- `Charles L. Burkholder`

- `Carol Wood`

- `Dante J. Alarcón`

- `Timothy A Clark`

- `Tim Peel`

- `Elbert L Freeman`

- `John DeGennaro`

- `Steve Quan`

## LPI-Linux Essentials

# LAB 1

## Linux Evolution and Popular Operating Systems

`Lab Objective:`

Understand what Linux is, how various Linux distributions evolved, and the use cases and target audiences of those distributions. Install `Ubuntu 18.04`, or a distro of your choice, into a VM.

`Lab Purpose:`

Unlike with proprietary operating systems, Linux's nature means that its users have limitless options in terms of what software will (and won't) be installed on their computers. There are hundreds of Linux distributions or “distros” available today, but Linux didn't begin that way. `Debian`, `Slackware`, and `Red Hat` have existed since the early 1990s and are three of the oldest distros still in use. Many of the current most popular distros were derived or forked from one of those three.

`Lab Tool:`

An internet-connected computer that can support `VirtualBox`, or another hypervisor software.

`Lab Topology:`

`N/A`

## Lab Walkthrough:

### Task 1:

Review this tree of Linux distributions (see URL in the notes). Try to locate some of the most commonly used distros:

- `Debian`

- `Ubuntu`

- `CentOS`

- `SUSE`

- `Red Hat`

- `Linux Mint`

- `Scientific Linux`

- `Raspbian`

- `Android`

How are these distros related to one another?

### Task 2:

If you haven't already done so, consider that you are about to install a Linux distro for the first time. Think about what your needs would be on a desktop, or a server, or both. Then take this quiz: `https://distrochooser.de/en`

### Task 3:

Make a note of your results from Task 2. Visit the websites of any distros that look interesting to you. What are their use cases and development philosophies (if any)?

### Task 4:

Now it is time to install a Linux distro for use in the rest of the labs. For simplicity, we will assume the use of `Ubuntu 18.04 LTS`. However, if you are an advanced user, you are encouraged to try these labs on another distro of your choice.

Here is a great guide on how to install `Ubuntu 18.04` in `VirtualBox`:

`https://linuxhint.com/install_ubuntu_18-04_virtualbox/`

`Notes:`

Many distributions have a “Live USB” that you can test out without having to erase a computer’s hard drive. You can also use `VirtualBox`, or another hypervisor, to test any number of Linux distros. Nearly every distro should run in a VM without trouble.

In subsequent labs, we will assume the use of an `Ubuntu 18.04 LTS` VM running on `VirtualBox`. This is by no means the only possibility, and once you’ve practiced the labs a few times, we encourage you to experiment with other distros!

`https://upload.wikimedia.org/wikipedia/commons/1/1b/Linux_Distribution_Timeline.svg`

# LAB 2

## Major Open Source Applications: Desktop

`Lab Objective:`

Learn about common Linux desktop applications and how to install new applications using a package manager.

`Lab Purpose:`

Linux has a variety of open-source desktop software, serving the same functions as common proprietary software on other operating systems. In this lab, you will learn about some popular open-source software, and how to install and update said software using a tool called a package manager.

`Lab Tool:`

`Ubuntu 18.04` (or another distro of your choice)

`Lab Topology:`

A single Linux machine, or virtual machine

`Lab Walkthrough:`

### Task 1:

A default `Ubuntu` desktop has some common software already installed. See if you can locate, and familiarize yourself with, the following applications:

- `LibreOffice`—Office suite

- `Thunderbird`—Mail client

- `Firefox`—Web browser

Can't find these? Click `"Show Applications"` in the lower lefthand corner, then you can search for an application in the search box:

`![](img/64f3c5d0defa97e8b856b229f9322b97_19_0.png)`

### Task 2:

As just one example, you will now configure `Thunderbird` to connect to an e-mail account. Upon opening `Thunderbird` for the first time, you should be greeted with a dialog like this:

`![](img/64f3c5d0defa97e8b856b229f9322b97_19_1.png)`

Enter the details for your e-mail account, then click `Continue`. Many common mail providers are included in `Mozilla`’s own database and will require no further configuration. For example, if you have a `Gmail` account, `Thunderbird` will set it up for you automatically once you’ve provided credentials.

If your e-mail service is not auto-configured, you will have to click `"Manual config"` (on the next screen) to enter your server details. Check with your mail provider for the correct values to enter.

### Task 3:

What if you want to use an application that isn’t already installed? You will have to install it! Fortunately, with Linux package managers, this is easy to do. Search for `"GIMP"` and install it with `Ubuntu Software`. Then, familiarize yourself with `GIMP` as well. `GIMP` is an image editing application.

### Task 4:

Under the hood, `Ubuntu Software` uses a package manager called `apt`. Different Linux distros use different package managers, but their primary purpose is the same—to provide a centralized location from which to install and update thousands of common software packages.

Can you match the following distros below with their default package managers?

| Distro | Package Manager |
| :--- | :--- |
| Arch | `pacman` |
| CentOS | `yum` / `dnf` |
| Debian | `apt` |
| Fedora | `dnf` |
| Gentoo | `Portage` |
| SUSE | `Zypper` |

`Notes:`

Sometimes, you may need to install a package that is not available in a distro’s package management repositories (repos). In this case, you will either need to add additional repos, or install the package manually with a tool like `dpkg`.

# LAB 3

## Major Open Source Applications: Server

`Lab Objective:`

Learn about some software and development tools commonly deployed on Linux servers.

`Lab Purpose:`

In this lab, you will survey several common Linux server software tools. Though configuring these tools in detail is outside the scope of this lab, it is important to familiarize yourself with their applications.

`Lab Tool:`

`Ubuntu 18.04` (or another distro of your choice)

`Lab Topology:`

A single Linux machine, or virtual machine

`Lab Walkthrough:`

### Task 1:

Use a web browser on your Linux VM to research some of the following common Linux server applications:

- Web Servers: `Apache httpd`, `nginx`

- Databases: `MariaDB`, `MySQL`

- File Servers: `NFS`, `Samba`

- Private "Clouds": `Nextcloud`, `ownCloud`

In what situations would you deploy each application?

### Task 2:

Are you familiar with any programming languages, such as...

- `C`?

- `Java`?

- `JavaScript`?

- `Perl`?

- `Python`?

- `PHP`?

- Something else?



如果你有任何软件开发经验，你可能喜欢在上Ubuntu Software或其他包管理器中搜索你喜爱的语言工具。所有这些语言以及更多语言都支持在Linux上运行。

### 任务3：

现在，你将连接到远程Linux服务器。首先，使用Ubuntu Software安装一个名为PuTTY的应用程序。PuTTY是SSH/Telnet客户端的图形化版本，通常用于连接远程Linux服务器，特别是从Windows机器。

运行PuTTY后，你会看到一个连接屏幕。输入`towel.blinkenlights.nl`，选择Telnet，然后单击Open：

![](img/64f3c5d0defa97e8b856b229f9322b97_23_0.png)

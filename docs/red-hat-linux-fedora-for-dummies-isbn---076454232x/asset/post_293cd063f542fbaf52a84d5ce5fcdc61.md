
# Building an Apache Web Server

  The Web is the Internet, and the Internet is the Web. Well, that’s not completely true because the Internet provides the foundation for widely used functions, such as e-mail. However, the Internet became immensely popular because of the World Wide Web (WWW).

  The Web isn’t as mysterious as it may seem at first. It’s essentially all the world’s web servers that are connected to the Internet. The Internet serves the same function as the world’s telephone system: It interconnects everyone. You can think of web servers as the telephones that allow people to contact each other, businesses, and other organizations. Just as you can start a business or organization and let people contact you via your phone, you can also allow people to contact you via your web server. This section describes how to construct a simple web server.

> **TIP** Describing how to set up anything more than a simple web server is beyond the scope of this book. Needless to say, you can configure Apache to provide a whole world of Web services. If you want to utilize the powers of Apache, consult such books as the excellent *Apache Server 2 Bible*, by Mohammed J. Kabir, published by Wiley Publishing, Inc.

## Installing and starting the web server

  Linux provides the ideal platform for providing Web services. The Apache web server system is bundled with Red Hat Linux. Apache is easy to set up and use.

  Because you’re entering the world of creating and administering Linux services, you switch your orientation from performing work in GUIs to the command-line interface (CLI). Linux system administrators should become comfortable with using the CLI because many functions are best performed with the command line. You enter commands in the GNOME Terminal (terminal emulator) window in this chapter rather than use graphical utilities.

  Follow these steps to install and configure a basic web server:

- 1. **Log in as root and mount the companion DVD-ROM.**
   Now you need to install the Apache RPM packages.
- 2. **You manually install the packages by first starting a GNOME Terminal window by clicking the GNOME Menu and choosing System Tools→Terminal. Enter these commands:**

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/apr*
rpm -ivh /mnt/cdrom/RedHat/RPMS/httpd*
```

  The Apache RPM package puts all configuration files in place, so all you have to do is start the appropriate daemon.

- 3. **Enter this command from the GNOME Terminal window:**

```
/etc/init.d/httpd start
```

![](img/8c094d1b36276212c03d10d898508a6e_237_0.png)

  Linux uses the term *daemon* when referring to a process that runs continuously in order to provide a service. The Apache daemon is named `httpd`, short for HyperText Transfer Protocol Daemon. *HyperText Transfer Protocol (HTTP)* is the system used to coordinate the transfer of Web pages between the server and the client (for example, the Mozilla browser). HTTP is the common language that both sides speak.

- 4. **Start your Mozilla Web browser and enter localhost in the URL window.** Your new web server is displayed, as shown in Figure 16-1.

- 5. **If you want your web server to start automatically every time you boot your computer, enter this command in the terminal emulator window:**

```
chkconfig --level 35 httpd on
```

  The *level 35* option configures the web server to start in either non-graphics mode (system level 3) or graphical (system level 5) modes.

![](img/8c094d1b36276212c03d10d898508a6e_237_1.png)

  Running the chkconfig utility creates *soft links*, which are roughly analogous to a pointer. In this case, the soft link S05httpd is run automatically whenever you boot your computer.

  Your web server should now be visible on your private network. (If your computer isn't connected to a LAN — for example, if it's a stand-alone machine with a telephone, cable, or DSL Internet connection — you can still use your web server from the machine itself.) However, keeping your web server all to yourself isn't much fun. The following section describes how to allow access to your web server from the Internet.

![](img/8c094d1b36276212c03d10d898508a6e_237_2.png)

  The Open Office suite has an HTML editor you can use to create Web pages. It's simple to use and can produce great-looking documents. Open any Open Office program (Writer or Spreadsheet, for example) and choose File > New > HTML Document. The HTML editor window opens, and you can create Web pages.

## Accessing your web server through your firewall

  This section describes how to open your firewall to allow access to your web server. Exactly how you allow access depends on whether you're connecting to the Internet directly from your Linux computer or through a LAN. The steps in this section describe how to modify your firewall and a DSL Internet connection to allow the Internet to view your Web page.

![](img/8c094d1b36276212c03d10d898508a6e_238_0.png)

  Figure 16-1: Your first web server!

  You must modify the network address translation (NAT) configuration if you're using a DSL modem like the one we describe in Chapter 6. Connect to the DSL modem as described in Chapter 6 and run these commands:

```
set nat entry add 10.0.0.1 80 192.168.32.254 80
write
```

  You have to modify your Internet gateway or firewall too. You have to allow external web browsers to connect to port 80 on your Apache server. Create the firewall rule by entering this command:

```
iptables -A INPUT -p tcp -m state --state NEW,ESTABLISHED -j ACCEPT -dport 80
```

  Amazons of the world, watch out! Okay, it takes just a bit more than the default Apache Web page to upset the big boys, but you have the basics in place. All you have to do is figure out what to sell. How about a great Linux book?

## Building a Samba File Server

  Early in the game, Linux gained much popularity by acting as a file server for both Windows and Linux computers. It did that by dancing the Samba. Samba is more than just a dance routine — it’s a suite of programs that speaks the same file-sharing language (the *protocol*) as Microsoft Windows. Using Samba produces a way to share the Linux file system on a network.

  This section describes how to install and configure Samba on your Red Hat Linux computer. Samba comes bundled with Red Hat Linux, of course, so installation is a breeze. Samba is also configured to automatically share the ubiquitous `/home` directory, so configuration is also easy.

![](img/8c094d1b36276212c03d10d898508a6e_239_0.png)

  Samba is based on the client-server model in which a computer (server) provides services to one or more computers (clients). Samba uses the term *share* (which comes from the Microsoft Windows world) to refer to any object it exports to a network. An object can be a directory or a printer.

### Installing and starting Samba

  Samba consists of several programs, configuration files, and documentation files. The complete Samba package consists of four RPM files that come bundled on the DVD-ROM accompanying this book. This list describes the purpose of each RPM file:

- **samba-client:** This package contains the utility and other supporting software to connect a Linux computer to a Samba server. You can use the interactive utility `smbclient` to connect to a Samba share. The default Red Hat Linux installation installs this package by default.
- **samba:** The Samba server software is included in this package. All the programs for sharing files, directories, and printers are included here; the two essential daemons are `smbd` and `nmbd`; the essential configuration file is `smb.conf`. The utilities for controlling the daemons are also included.
- **samba-swat:** You can manually configure the Samba configuration file, `smb.conf`, if you’re an expert. However, Samba provides a Web-based system that is much easier to use and produces clean and readable configuration files.
- **samba-common:** All the software required by the other three packages is included in this file. This package is also installed by default.

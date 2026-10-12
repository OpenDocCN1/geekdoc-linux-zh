
## Chapter 16
### Creating Basic Linux Network Services

#### In This Chapter

- Preparing a network server
- Building a Linux Web server
- Building a DNS server
- Building a Samba file server
- Building a print server

Linux was built from scratch with networking in mind. Networking is not merely an afterthought, as with other operating systems. Fedora Core comes bundled with software that provides file sharing, printer sharing, and other functions. This is why Linux gained its initial popularity.

In earlier chapters, we show you how to use a Fedora Core computer with an existing network. We also show you how to build a private network using Fedora Core computers as both clients and the Internet gateway, or firewall. In this chapter, we describe how to configure a Linux box to provide some popular services to the private network.

### Preparing a Network Server

All examples shown in this chapter can be run from any Linux computer, such as the one set up around the Fedora Core distribution in Chapter 3. Linux doesn’t care what your intentions were when you built your computer. Linux eagerly does what it’s told and works gracefully as either a workstation or server.

Linux works equally well whether it’s running a Web browser or a Web server; the difference between them is just the software used and how it’s configured.

For example, you start the Mozilla application when you're using your computer as a Web browser, or you use the Apache program to serve Web pages. You can, of course, run both programs at once and (for example) do word processing while running a Web server.

You can configure the Fedora Core computer from Chapter 3 to provide services to a private network like the one we describe in Chapters 7 and 15. This chapter describes how to make the Apache Web server visible to the Internet. Services such as Samba and printing, however, definitely should be kept private and not shown to the Internet.

We also assume in this chapter that you're connecting to the Internet through a private network, as described in Chapters 7 and 15. (Chapter 15 shows you how to create an Internet gateway/firewall for your private network with a Fedora Core computer.) This chapter assumes that you want to use the same computer to provide services to your private network. This assumption is reasonable for small-office and home-office (SOHO) networks because the demands put on a modern PC by a small network aren't excessive. Using a single computer for multiple purposes greatly simplifies the work you must do and is an efficient way to use your resources.

![](img/41feae212f5c6612ff709354891f7b39_229_0.png)

Using a single Linux computer to act as an Internet gateway and provide network services is a cost-effective way of using your limited resources — but this type of configuration is more difficult to secure. Each function you place on a single machine increases the machine’s potential number of vulnerabilities. Think of adding functions as similar to adding doors and windows to a house: A house with a single door and no windows is more secure than a house with 5 doors and 15 windows — but who wants to live in a dark house? As with everything else in life, security is a matter of compromise. Consult Part II and Chapters 17 and 21 in this book for ways to increase security.

### Building an Apache Web Server

The Web is the Internet, and the Internet is the Web — well, that’s not completely true. Although the Internet became immensely popular because of the World Wide Web (WWW), there’s more to the Internet — it provides the foundation for widely used functions. E-mail is one such; the Web is another.

The Web isn’t as mysterious as it may seem at first. It’s composed of essentially all Web servers that are interconnected via the Internet. The Internet itself serves the same function as the world’s telephone system: It allows everyone to communicate with each other. You can think of Web servers as the telephones that allow people to contact each other, businesses, and other organizations. Just as you can start a business or organization and let people contact you via your phone, you can also allow people to contact you via your Web server. This section describes how to construct a simple Web server.

Describing how to set up anything more than a simple Web server is beyond the scope of this book. Needless to say, you can configure Apache to provide a whole world (so to speak) of Web services. If you want to utilize the powers of Apache, consult such books as the excellent *Apache Server 2 Bible*, by Mohammed J. Kabir (Wiley).

#### Installing and starting the Web server

Linux provides the ideal platform for providing Web services. The Apache Web server system — which is bundled with Fedora Core — is easy to set up and use.

Follow these steps to install and configure a basic Apache Web server:

1. Log in as any user and insert the companion DVD.
   - The Apache software is on the DVD.
2. Click the Fedora menu and choose System Settings::Add/Remove Applications.
   - The Query dialog box opens if you’re not already logged in as the superuser (root).
3. Enter the root password if you’re prompted.
   - The Checking System Status dialog box opens and displays a progress bar while it determines which software is installed on your computer. The Add and Remove Software dialog box opens.
4. Scroll down and click the Web Server button.
5. Click the Update button.
   - The Preparing system update dialog box opens while the package-installation utility prepares to install the software. The window title changes to Completed System Preparation when it finishes.
6. Click the Continue button.
   - A dialog box labeled Updating system shows the installation progress.
7. Click the OK button.
   - Control returns to the Package Management window.
8. Click the Quit button.

If you’re connected to the Internet, you can use YUM — the Yellowdog Updater, Modifier (yucky acronym, but, er, yummy functionality) — to install the Apache (or any) package. YUM connects to the Fedora Core project’s download server and installs any packages you want; you can also use a Fedora Core mirror. YUM also performs other functions, such as updating your computer. Enter the command **yum -y install httpd** and YUM does all the work for you. YUM "Yummifies" your computer. Stupid puns aside, it's a wonderful system. See Appendix E for more on YUM.

The Apache Web server comes preconfigured to display a sample Web page, which we use for the example in this section. All you have to do is configure your Apache Web server. Fedora Core provides a simple GUI to help you with the configuration.

The following steps describe how to configure your server:

1. Click the GNOME Menu and choose **System Settings->Server Settings**.
   - A Query dialog box opens if you're not logged in as **root**.
2. Enter your **root password** if you're prompted.
   - The HTTP dialog box opens.
3. Enter **localhost** in the **Server Name** text box.
   - Alternatively, you can enter the Internet name of your computer (for example, the computer *cancun.paunchy.net* in our example) if you want to share the Web server with your private network.
   - You can configure other options by clicking to select the various tabs at the top of the dialog box. A description of those options is beyond the scope of this book; the default settings work fine for your simple Web server.
4. Click the **OK** button.
5. Click the **Yes** button when the Question dialog box opens.

The HTTP window closes and your Web server is configured. You need to start the server to view the sample Web page. Follow these steps to start the server.

1. Click the GNOME Menu and choose **System Settings->Services**.
2. Enter the **root password** if prompted.
   - The Service Configuration dialog box opens.
3. Scroll down the left submenu and click the box next to the **httpd**.
4. Click the **Start** button to start the **Apache Web server**.
   - An Information dialog box opens.
5. Click the **OK** button.


Your operating system: The operating system you use for your Web server is very important. If you run Apache on a version of the operating system (whether it be Linux, Windows, or Solaris) that is known to have a security risk then your server can be attacked. Running an up-to-date operating system is a must.

Your Web server software: This is your third security checkpoint. Make sure that you're running a version of Apache that has no known security risks.

I discuss these checkpoints in the following sections.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_527_0.png)

## Checkpoint 1: Your network

The first checkpoint to consider is your network, and how it is connected to the Internet. The real issue is where you place your Web server. The general idea is to isolate your internal network, keeping it away from prying eyes as much as possible. Definitely consider installing a firewall in your Internet-to-LAN router. If a firewall is not an option, you can consider the proxy-server option. A proxy server takes one network's request to another network without ever connecting the two. This might be a good solution because it also provides an excellent logging facility.

As you can see, you should be more concerned about your internal network than the Web server, itself. Because networks introduce Internet-accessible Web server(s) within the network, they are likely to get broken into by way of exploiting a security hole in the Web server software, or by a hole in an application (such as a CGI program) that is running on the Web server. The chances of this occurring are reduced by choosing a network architecture that isolates the LAN from the Web server.

If you have a network configuration, such as the one shown in Figure 18-2, your network is virtually unprotected.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_528_0.png)

Figure 18-2: A simple network with an Internet connection.

To keep things simple, the discussion assumes that you only have a single connection to the Internet. In this network model, all Internet traffic can be routed to and from your network. In other words, anyone on the Internet can reach any host on your network and vice versa. This also means that a hacker on the Internet can find a weak point in one of the many hosts that you have on your network. Of course, not all of these hosts are servers with services enabled for others to use; but, even if you have a Windows machine with file sharing enabled, it is a potential target. Because the entire network uses TCP/IP, a simple file-sharing option on a Windows workstation machine can lead to a break-in. This network almost invites criminals who want to break in.

If you have this configuration, check your router documentation to determine whether you can enable IP-based restrictions. I recommend this configuration be avoided at all costs.

> See the Choosing a Security Configuration section later in this chapter for some network configurations you can use.

## Checkpoint 2: The operating system

Apache runs on virtually all Unix platforms, and it is already starting to run on Windows 2000, Windows 95, and even on the new Macintosh operating system, Mac OS X. But just because Apache runs on virtually any platform does not mean that you should use just any operating system to run Apache. Choosing the right operating system (OS) can be a significant factor in system security. Well-known Unix and Unix-like operating systems include Mac OS X, BSDI, FreeBSD, SunOS, Solaris, HP-UX, Digital Unix, and Linux. Internet server administrators favor these operating systems. Although the quality and reliability may vary among these operating systems, all are designed for use as server operating systems.

If you do not like Unix, look into the Windows 2000 server platform. Windows 2000 is a very powerful Unix competitor, likely to give Unix a run for its money in the future; however, Windows 2000 is new to the Internet game. Most Unix and Unix-like operating systems have been around long enough to suffer numerous hacks and attacks. They stand as the survivors and—though never completely hack-proof—remain tall.

**Tip** After you have chosen an operating system, you should disable any extra features that you don’t intend to use on the Web server machine running that OS. For example, if you do not need SMTP/POP mail or FTP services, disable them or completely remove the mail server programs from the system. If you don’t need a lot of powerful system utilities, delete them. Make certain that your Web server is just a Web server and has only the services it needs.

**Cross-Reference** You can learn about vulnerabilities that exist in your operating platform by browsing www.cert.org. CERT (Computer Emergency Response Team) works with the Internet community to facilitate awareness of, and response to, security issues. The organization also conducts research targeted at improving the security of computer systems.

## Checkpoint 3: Web server software

Obviously, you use Apache as the Web server software or you would not be reading this book. Make sure, however, that you use the latest, stable version of Apache 2 server for your system. It is a good idea to compile your own Apache binaries instead of using those of a binary distribution.

Apache is freely available software, so it is important that you obtain it from a reliable source. Do not ever download Apache binaries or source code from just any Web or FTP site. Always check with the official site, www.apache.org, first. Apache source is PGP (Pretty Good Privacy) signed. Also note that the current Apache distribution includes a PGP key-ring file containing the PGP keys of most active Apache developers.

The Apache group PGP signatures are in the file `KEYS` in the top-level distribution of Apache. If you trust the site from which you obtained your distribution, you can add these keys to your own key ring. If you do not know how to use PGP on your system, learn about it at `www.pgp.com`.

Each Apache source distribution is PGP signed and these signatures are stored in files with an `.asc` extension (for example, the signature for `apache_2_0_tar_gz` is stored in `apache_2_0_tar_gz_asc`). These can be used to check the validity of the distribution if you have added the `KEYS` file contents to your key ring.

The latest stable version of Apache does not have any known bugs; however, its capability to incorporate external third-party modules gives rise to a security issue: Can you trust a third-party module? People all over the world write many of the Apache modules. Make sure that you only use modules that are available on the official Apache Web site or registered in the Apache module registry located at `http://modules.apache.org/`.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_530_0.png)

Never use experimental modules in your production sites. In fact, it is a good idea to determine which modules you really need, and then to configure and compile Apache accordingly. This way you have a smaller, faster server with potentially better security.

When configuring Apache, pay a great deal of attention to security configuration issues. The basic idea is to disable anything you do not use. This way, you are taking preventive security measures and are likely to reduce risks.

## Choosing a Security Configuration

There are many ways you can configure Apache while enhancing your overall Web security. Before you can choose a configuration suitable for you, you need to develop a security policy and then choose a configuration suitable to meet your policy requirements. When it comes to security there is always a chance that you can overestimate the risks and become too paranoid or underestimate your security needs and keep things too open. In the sections below I discuss a few configurations that suit different environments.

### Security policy considerations

An administrative security policy identifies practices that are vital to achieving robust network security. If you do not yet have one, consider adding some of the following items to an administrative security policy as a start.

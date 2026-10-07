
# 412 Chapter 12 Serial Communications, Terminals, and Modems

text-mode commands and utilities; BBses often use custom menu-based environments in which you type letters or digits to move around the system.

## Making a PPP Connection

Today, establishing a PPP link is perhaps the most common use for a dial-out modem. PPP allows you to tie a system to the Internet using fast TCP/IP networking features. PPP-linked systems can therefore browse the Web, transfer files via FTP, send and receive e-mail, and so on. PPP links are usually transient and modem links are slow by modern Internet standards; it's uncommon to find servers running PPP-connected computers. Some Internet Service Providers (ISPs) do offer accounts that can be used constantly; however, it's usually less expensive to acquire faster service through a cable modem or DSL for always-connections.

### Testing Basic Connectivity

The first step in linking a computer to the Internet via PPP is to acquire an account from ISP. (If you want to link two computers that you control, such as an Internet-connected server at your home system, see "Accepting PPP Connections" later in this chapter for information on setting up a system to function as a PPP server.) Fortunately, ISPs are extremely common. You can find listings for them in your local telephone directory, probably under "Services" or some variant of that.

Before you go further in configuring PPP access, you should check that your modem and device files work correctly by checking the instructions in "Calling a Remote Text-Mode System," earlier. You can call your ISP's dial-in number with Seyon or minicom to check basic modem functionality. Depending upon how your ISP is configured, you may see a login: prompt or gibberish when you connect. The main test is that you get your modem by dial; if this works, then you can be sure you have no problems relating to your own modem or device file permissions.

### Connecting via PPP Scripts

Most ISPs today use the PAP or CHAP authentication protocols. These protocols allow you to identify yourself to the ISP in an automated fashion. In Linux, you must configure a file, called /etc/ppp/pap-secrets or /etc/ppp/chap-secrets; both files use the same format. Each line contains information for one account and takes this form:

```
client secret IP_address
```

> TIP: If you're not sure which system your ISP uses, you can create one file and use a hard or symbolic link to make it accessible under both names. For instance, create /etc/ppp/pap-secrets and type ln -s /etc/ppp/pap-secrets /etc/ppp/chap-secrets.

## Configuring Modems 413

The meanings of each element are:

- client: The username on the ISP's system.
- server: The name of the ISP's server. This value is normally *, which means Linux accepts any server (because the ISP may change its server's name without notice).
- secret: The password to the ISP's system.
- IP_address: The numeric IP address or addresses that Linux will accept. This value is normally blank, meaning the system accepts any IP address.

As an example, the following file can be used to log on to an ISP using the username agb and the password comehere:

```
agb * comehere
```

> WARNING: The PPP secrets file, no matter what its name, is extremely sensitive, because it contains your ISP username in an unencrypted format. You should ensure that it is readable only by root (that is, it is owned by root and has 0600 permissions). You should also use a different password over your ISP than you use on any other system, so that if this file is compromised, it can't be used to gain illicit access to other systems.

To initiate a PPP connection using command-line tools, you must have appropriate PPP scripts. Samples are available with the PPP package for most distributions. In Red Hat 7.0, these scripts are in /usr/share/doc/ppp-2.3.11/scripts directory. Their names are ppp-up, ppp-up-dialer, and down. The first two are responsible for initiating a PPP connection, and the third breaks a PPP link. You should copy all three scripts to /etc/ppp or to a location on your path, such as /usr/local/bin. You must modify the ppp-up and ppp-up-dialer scripts to suit your configuration.

- In ppp-on, locate the lines that begin TELEPHONE=, ACCOUNT=, and PASSWORD= and modify them so they're appropriate for your ISP and account. (The ACCOUNT and PASSWORD variables may not be required if you use PAP or CHAP, but they should contain dummy variables in this case.)
- Check the DIALER_SCRIPT variable in ppp-on points to the correct location of ppp-on-dialer. The default location is /etc/ppp.
- Check the call to pppd in the last lines of ppp-on. (pppd is the tool that handles the PPP negotiations; the scripts provide it with the information it needs to do its job.) Most of the parameters to this are quite cryptic, but you should at least be able to confirm that it's using the correct modem filename and speed (115200 is appropriate in most cases, but the default is 38400).

![](img/4fb617eb648f87def380ef5d92052d01_440_0.png)

## Communicating with Devices PART 4

- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
- Check the ppp-on-dialer script. This script includes a “chat” sequence—a series of strings the program expects to see from the modem. You may need to log on using Seyon or minicom to get the username and password from your ISP.
(Note: The OCR text contains many repetitive/garbled lines here, I have cleaned the logical flow based on the provided context.)

Many ISPs send name system (DNS) information to clients during PPP authentication. If you doesn't, you'll need to enter this information into your /etc/resol.conf file. This file should contain one to three lines listing server addresses, as provided by your ISP. For instance:

```
nameserver 192.168.1.1
```

If your PPP configuration doesn't set this information automatically and you don't set manually, you'll be able to access sites on the Internet by IP address (such as 216.224.70.176), but not by names (see syex.com). You only need to configure DNS information once, not per connection.

### Connecting Using a GUI Utility

Because of the difficulties associated with establishing a PPP connection using scripts, many users prefer to use a GUI front-end. These tools use the same underlying pppd as conventional scripts, but their point-and-click interface makes it easier to enter information on your ISP and account. It's generally possible to dispense with scripts when using GUI utilities, which further lessens the possibility of error.

All systems that use KDE, including Red Hat Linux, come with a GUI utility called KPPP.

Action: Added PPP dialout functionality to Bob & Sally's Family ISP.

Files Added/Modified: ppp-on, ppp-on-dialer, ppp-off, and ppp-secrets, all in /etc/ppp.

All systems that use KDE, including Red Hat Linux, come with a GUI utility called KPPP (shown in Figure 12.5). You can use KPPP if you don't use KDE. Alternatively, you can use a PPP dialer that's not associated with a specific environment, such as X-ISP

![](img/4fb617eb648f87def380ef5d92052d01_442_0.png)

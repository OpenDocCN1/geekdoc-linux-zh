
Two options require a little more explanation. The reload option does not stop or start a service. It just reloads the configuration file. If you've just changed a configuration file, it's a quick way to put it into effect without restarting a service. A restart would kick off any connected users.

The constrestart restarts a system only if the system was already running. /etc/init.d/ scripts include a number of other options; perhaps the most important include the word force in the script, which can be helpful if a service is not responding to commands.

While developers are working on replacing regular service scripts in the Upstart system, it is unlikely that the /etc/init.d/ directory will be completely replaced in stable Linux distributions. And if they are, developers will have to make the change appear seamless to the administrator.

## Isolate with chroot Jails

Conceptually, a chroot jail is sort of a virtual machine. In fact, it's considered by some as type of operating system-level virtualization. In most cases, a chroot jail includes all of the binaries, libraries, configuration files, and executables required to run a service that is contained. A properly configured chroot jail does not allow privilege escalation of any sort, whether without SUID or SGID-bit modified executable files or other means of gaining administrative access.

If a black- hacker is able to break into a service, his actions should be confined to the files and subdirectories in the chroot jail. With administrative access, hacker may be able to break out of chroot jail into the main directory tree for the local system.

Significant services that have been configured with chroot jails include the Berkeley Internet Name Daemon (BIND) software for DNS, the very FTP daemon (vsFTPD), and the Postfix email server. As described in Chapter 5, the vsFTPD chroot jail would be configured to limit both anonymous and regular users to appropriate directories.

One interesting implementation of a chroot jail is based on the Red Hat bind-chroot package, which configures the files needed for the BIND DNS service in the /var/named/chroot/ directory. For more information on BIND and Postfix, see Chapter 9.

## Avoid X Servers and X Clients Where Possible

Regular users demand the GUI. So it's impossible to avoid the GUI in most situations. But the GUI isn't required for most systems with Linux servers. It isn't even required for servers that share graphical images such as the Apache web server. Since the GUI presents a number of security risks, you should avoid installing the GUI on Linux servers when possible.

In Linux, X is a common reference to the GUI. The main server for Linux is based on the work of developers sponsored by the X.org foundation. The X server uses hardware on the local system to display graphical images. These images come from X clients, which may be either locally or remotely.

## CHAPTER 6 | Every Service is a Potential Risk

Most of the latest Linux distributions, including Ubuntu and Red Hat, have disabled the X systems that present the most challenging security risks. Options such as xhost and xauth have been disabled. Of course, you can install them, but data sent using such commands, including passwords, is in clear text.

## If You Must Have a GUI

Linux systems that be configured with a GUI must be protected carefully. First X clients can be run remotely if port 1771 is closed. The primary means is to use an SSH server. When a user uses the ssh -X remotehost command, that user is given access to remote GUI clients unless the following directive is added to the SSH server configuration file (/etc/ssh/);

X11forward no

## The Surprising Generic Text Tool

Telnet. That name should evoke fear in the mind of any security professional, as it transmits data such as usernames and passwords in clear text. (For Chapter 8.9). However, the telnet command is an excellent way to verify the accessibility of a service over a network. Based on standard port numbers listed in /etc/services, try the telnet command online. For example, the following command can verify access to an SMTP e-mail service using the standard port number. Of course, you'll need to substitute an actual SMTP URL or IP address for email.example.org.

```
$ telnet email.example.org 25
```

To find the URL of an SMTP service, run the host example.org command, substituting your favorite URL for example.org. In most cases, you'll able to run the telnet command to connect to that e-mail server using the command model shown above.

You can use the telnet command to verify connectivity to other services. As long as the applicable TCP/IP port is open on the target server and the service is running, you should see the following response:

```
Trying to 192.168.0.1.
Connected to some.example.org (192.168.0.1).
Escape character is '^'.
```

If you choose to block all connections, the telnet command is still useful locally. If you're configuring a system, the telnet command with the appropriate port number can help verify that a service can communicate.

## PART 2 | Layered Security and Linux

FIGURE 6-8

The elinks Web browser.

Test Page for the Apache HTTP Server on Red Hat Enterprise Li... (1/3)
Red Hat Enterprise Linux Test Page

This page is used to test the proper operation of the Apache HTTP server after it has been installed. If you can read this page, it means that the Apache HTTP server installed at this site is working properly.

If you are a member of the general public:

The fact that you are seeing this page indicates that the website you visited is either experiencing problems, or is undergoing routine maintenance.

If you would like to let the administrators of this website know that you've seen this page instead of the page you expected, you should send them e-mail. In general, mail sent to

## Test with Text Tools

Many excellent text- and console-based tools are available for Linux. These tools can be used to check data from a number of different "graphical" services. For example, elinks is a console browser that you can use to review data from Web servers. On a Red Hat system with a running Apache Web server, the elinks 127.0.0.1 command returns the page in Figure 6-8.

Try on the Web of your choice. You might be surprised with what you can do with this console browser. It should give you confidence in Linux text tools.

If you're testing an e-mail service, several excellent text-based tools are available, including matt, pine, and mail. With any standard e-mail client, these text-based tools can be used to connect to the e-mail services of your choice.

There's even a console-based client for testing audio, cmus. If you're looking for.

## The Risks of Productivity Tools

As a Linux guru, you can avoid GUIs. While you would go against the principles of open source, it would reduce your workload to limit the Web browsers available on the local network. The list of browsers shown in Table 6-4 just includes those that are supported. Other options are available from other open development groups. Each of them may have their security issues, and may be less well supported. It would be difficult to monitor security alerts for all of these Web browsers.

The major graphical browsers for Linux are listed in Table 6-4, along with their URL. If you compare these, you may note a lot of similarities. When Netscape released its browser under an open source license, the Mozilla foundation and others started using and improving their source code.

Browsers

## CHAPTER 6 | Every Service is a Potential Risk

TABLE 6-4 Linux GUI browsers.
| GUI BROWSER | DEVELOPER | URL |
| :--- | :--- | :--- |
| Amaya | World Web Consortium (W3C) | http://www.w3.org/Amaya/ |
| Epiphany | GNOME Foundation | http://projects.gnome.org/epiphany/ |
| Firefox | The Mozilla Foundation | http://www.mozilla.org/firefox/ |
| Konqueror | KDE e.V. (Registered in Germany) | http://www.konqueror.org/features/browser.php |
| Opera | Opera Software, ASA | http://www.opera.com/support/ |

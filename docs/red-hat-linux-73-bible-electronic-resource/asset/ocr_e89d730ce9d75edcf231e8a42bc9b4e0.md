+   • FTP server — Port 21
+   • DNS server — Port 53 (if you're doing your own DNS)
+   • SSH server — Port 22 (allows secure login service to administer the computer remotely)

To see which ports are assigned to which services by default, refer to the /etc/services file. In most cases, a configuration file for a service indicates the default port number the service listens on. One way of making a service more private is to change the port number that a service listens on. Then the user must know to ask for the service at that particular port.

Chapter 14 describes how to change your firewall to accept requests for these services. I start with the iptables example in that chapter when I create the DNS example later in this chapter. So you can use that description as a model for setting up a firewall to go with DNS. In the DNS example, you have separate computers for mail, FTP, and Web services. For a low-volume server, however, you can have them all on the same computer.

# Checking logs and system files

By making your servers public, you also make them more open to attacks. Although firewalls are a good first line of defense, you still need to watch the activity on those ports that you leave open. A consistent program of monitoring traffic and checking changes to your server, therefore, becomes more critical. The following are a few techniques that you can use to help secure your servers:

+   * **General security** — Make sure that you protect all your user accounts by using good passwords and the correct file permissions settings.
+   * **Tripwire** — Use tripwire to essentially take a snapshot of your critical system files so that you can check later to determine whether anyone's altered those files.
+   * **Logcheck** — Use logcheck to screen your log files and e-mail any suspicious messages to you.

I describe these and other security techniques in Chapter 14.

# Keeping up with fixes

You can expect to find and correct security breaches constantly. You need to keep up with fixes that published to plug security holes. Although some of these fixes address theoretical security problems, others are created in response to actual break-ins or denial-of-service attacks that are known to exploit weaknesses in the components that come with your operating system.

Using the Red Hat Network (and its update facility) is one way of getting security fixes that are tailored for Red Hat Linux systems and that become available on a very timely basis. Checking CERT and other organizations (which I describe in Chapter 14) for security alerts is another thing that you should do.
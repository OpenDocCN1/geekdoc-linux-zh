# Devices

Do not ever advertise that you have set a NIC to promiscuous mode. Promiscuous mode (which can be set on an interface by using *ifconfig*'s *promisc* option) is good for monitoring traffic across the network and can often allow you to monitor the actions of someone who might have broken into your network. The *tcpdump* command also sets a designated interface to promiscuous mode while the program runs; unfortunately, the *ifconfig* command does not report this fact while *tcpdump* is running! Keep in mind that this is one way a cracker will use to monitor your network to gain the ever-so-important root password.

> NOTE
> Browse to <http://www.redhat.com/docs/manuals/> to read about how to detect unauthorized network intrusions or packet browsing (known as network *sniffing*). You can use the information to help protect your system. Scroll down the page and click the Security guide link.

Do not forget to use the right tool for the right job. Although a network bridge can be used to connect your network to the Internet, it would not be a good option. Bridges have almost become obsolete because they forward any packet that comes their way, which is not good when a bridge is connected to the Internet. A router enables you to filter which packets are relayed.

# Viruses

In the right hands, Linux is every bit as vulnerable to viruses as Windows is. That might come as a surprise to you, particularly if you made the switch to Linux on the basis of its security record. However, the difference between Windows and Linux is that it is much easier to secure against viruses on Linux. Indeed, as long as you are smart, you need never worry about them. Here is why:

+   - Linux never puts the current directory in your executable path, so typing `ls` runs /bin/ls rather than any `ls` in the current directory.
+   - A nonroot user is only ever able to infect files he has write access to, which is usually only the files in his home directory. This is one of the most important reasons for never using the root account longer than you need to!
+   - Linux forces you to mark files as executable, so you can’t accidentally run a file called `myfile.txt.exe`, thinking it was just a text file.
+   - By having more than one common web browser and email client, Linux has strength through diversity: Virus writers cannot target one platform and hit 90% of the users.

Despite saying all that, Linux is susceptible to being a carrier for viruses. If you run a mail server, your Linux box can send virus-infected mails on to Windows boxes. The Linux machine would be fine, but the Windows client would be taken down by the virus.
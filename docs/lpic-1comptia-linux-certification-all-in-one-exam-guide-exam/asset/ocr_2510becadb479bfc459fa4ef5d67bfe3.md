These two entries specify that the /etc/hosts file (files) is consulted first for name resolution. If there is no applicable entry, the query is then sent to the DNS server (dns) specified in the resolv.conf file.

TIP
You can use the hostname command at the shell prompt to show or set the system’s hostname. You can also use the dnsdomainname command to show the system’s DNS domain name

With this in mind, let’s next look at some of the tools you can use to troubleshoot networking issues on Linux.

# ### Troubleshooting Network Problems

Getting your network interface installed is only half the battle. To enable communications, you need to use a variety of testing and monitoring tools to make sure the network itself is working properly. We’ll discuss how to do this in this part of the chapter. We’ll cover the following topics:

+   * Using a standardized troubleshooting model
+   * Using ping
+   * Using netstat
+   * Using traceroute
+   * Using name resolution tools

Let’s begin by discussing how to use a standardized troubleshooting model.

# ### Using a Standardized Troubleshooting Model

Being a good troubleshooter is a key part of being an effective Linux system administrator. I’ve been teaching new system administrators for 16 years now, and this is one of the hardest skills for some to master. Some new admins just seem to have an intrinsic sense for how to troubleshoot problems; others don’t. The reason for this, in my opinion, is that troubleshooting is part art form. Just as it’s difficult for some of us (me included!) to learn how to draw, sculpt, or paint, it’s also difficult for some of us to learn how to troubleshoot.

However, I’ve noticed that, with a little training and a lot of practice, most new administrators can eventually learn how to troubleshoot effectively. There are three keys to doing this:

+   * Using a solid troubleshooting procedure
+   * Obtaining a working knowledge of troubleshooting tools
+   * Gaining a lot of experience troubleshooting problems

The last point is beyond the scope of this book. The only way to gain troubleshooting experience is to spend a couple of years in the field. However, we can work with the
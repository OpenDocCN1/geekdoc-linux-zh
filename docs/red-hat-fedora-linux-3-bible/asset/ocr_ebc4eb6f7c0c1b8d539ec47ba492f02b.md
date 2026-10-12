Although these files are created in the /etc directory, the NIS administrator can copy these files to a different location and change them, so as not to share the master NIS server's original configuration files. Files can also be added to this list or removed from the list as the NIS administrator chooses. When an NIS client computer is configured, this configuration information can be obtained from the NIS master server.

# ## Setting Up Fedora as an NIS Client

If your network uses NIS centrally to administer users, groups, network addresses, and other information, you can set up your Fedora system to use that information as an NIS client. To configure Fedora as an NIS client, you need to get the following information from your NIS administrator:

+   - **NIS Domain Name** — This is a keyword used to describe the group of hosts that use the common set of NIS files. Domain name is an unfortunate way of referring to this keyword, because it doesn't have anything to do with the TCP/IP domain name. Its only similarity is that it refers to a group of computers.

+   - **NIS Master Server Name** — This is the name of the computer on your network that maintains the NIS databases and responds to requests from the network for that information.

+   - **NIS Slave Server Names** — An NIS domain may have more than one NIS server that can handle requests for information from the domain's NIS database. An NIS slave server keeps copies of the NIS maps so that it can respond to requests if the master NIS server goes down. (NIS slave servers are optional.)

When you installed Fedora, if you knew that your network used NIS, you may have selected NIS as the way to handle user names and passwords on your computer. If you have not already configured NIS for your computer, the procedures that follow will describe how to do that. The procedures consist of defining your NIS domain name, setting up the /etc/yp.conf file, and configuring NIS client daemons (ypbind and ypwhich) to start when you boot your system.

# ## Defining an NIS domain name

You can set the Fedora computer's NIS domain name using the **domainname** command. For example, if your NIS domain name were *trident*, you could set it by typing the following as the root user from the shell:

```
```
# domainname trident
```
```

To verify that your NIS domain name is set, simply type **domainname** and you will see the name. Unfortunately, you're not done yet. Running **domainname** doesn't set the NIS domain name permanently. As soon as you reboot the computer, it is gone. (You can verify this by typing **domainname** again after a reboot.)
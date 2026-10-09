Mountain View, California 94039
United States
1888446337 Fax -- 1888446337

Domain servers in listed order:
NS1.HUNGERHOST.COM
NS2.HUNGERHOST.COM

Several top-level registries serve various regions of the world. You are most likely to use the following ones:

+   North American registry whois.arin.net  
+   European registry www.ripe.net  
+   Asia-Pacific registry www.apnic.net  
+   U.S. military whois.nic.mil  
+   U.S. government www.nic.gov

# Distributed Computing

When many similar systems are part of a network, it is often desirable to share common files and utilities among them. For example, a system administrator might choose to keep a copy of the system documentation on one computer's disk and to make those files available to remote systems. In this case, the system administrator configures the files so users who need to access the online documentation are not aware that the files are stored on a remote system. This type of setup, which is an example of *distributed computing*, not only conserves disk space but also allows you to update one central copy of the documentation rather than tracking down and updating copies scattered throughout the network on many different systems.

Figure 8-2 illustrates a *fileserver* that stores the system manual pages and users' home directories. With this arrangement, a user's files are always available to that user no matter which system the user logs in on. Each system's disk might contain a directory to hold temporary files as well as a copy of the operating system. Chapter 22 contains instructions for setting up NFS clients and servers in networked configurations.

# THE CLIENT/SERVER MODEL

+   *Mainframe model* The client/server model was not the first computational model. First came the main-frame, which follows a one-machine-does-it-all model. That is, all the intelligence

![](bbox=[0.25, 0.77, 0.92, 0.91])

Figure 8-2 A fileserver
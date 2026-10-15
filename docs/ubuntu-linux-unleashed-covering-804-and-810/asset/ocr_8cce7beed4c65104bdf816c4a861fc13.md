# CHAPTER 28

# Securing Your Machines

# IN THIS CHAPTER

+   - Understanding Computer Attacks
+   - Assessing Your Vulnerability
+   - Protecting Your Machine
+   - Viruses
+   - Configuring Your Firewall
+   - Forming a Disaster Recovery Plan
+   - Keeping Up-to-Date on Linux Security Issues
+   - Reference

No home computer with a connection to the Internet is 100% safe. If this information does not concern you, it should! Although there is no way to stop a serious cracker who is intent on getting into your computer or network, there are ways to make it harder for him and to warn you when he does.

In this chapter, we discuss all aspects of securing your Linux machines. You might have wondered why we did not spread this information around the book wherever it was appropriate, but the reason is simple: If you ever have a security problem with Linux, you know you can turn to this page and start reading without having to search or try to remember where you saw a tip. Everything you need is here in this one chapter, and we strongly advise you read it from start to finish.

# Built-in Protection in the Kernel

A number of networking and low-level protective services are built in to the Linux kernel. These services can be enabled, disabled, or displayed using the sysctl command, or by echoing a value (usually a 1 or a 0 to turn a service on or off) to a kernel process file under the /proc directory.

# Understanding Computer Attacks

There are many ways in which computer attacks can be divided, but perhaps the easiest is internal which are
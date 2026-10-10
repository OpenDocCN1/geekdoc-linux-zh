As previously stated, there are several options for alerts, including executing other programs. These programs could be shell scripts or really anything, so the possibilities are virtually limitless.

# ## How to Not Become Compromised

Virtually nothing can be done to stop an attacker with unlimited resources and unlimited time. From DoS attacks to rootkits to physical attacks, if someone wants at your data bad enough, chances are that he can get to it, given no other constraints. That said, there are many things you can do to limit your exposure to most risks.

Neither this chapter nor this book deals with physical attacks on any level. If an attacker is onsite and can simply walk off with the computer or hard drive containing the data, there’s no amount of firewalling that will help. If the attacker has physical access to the computer or device holding the data, the attacker can steal the data itself or possibly plant his own malicious trojan software.

This section gives some general suggestions that are field-tested to keep systems secure. The suggestions given here are by no means all-encompassing; rather they are merely things I suggest to help ensure system integrity.

# ## Secure Often

Securing the computing environment is a continual process rather than an endpoint. As you work to secure systems and networks, new vulnerabilities are being discovered and new software is being developed. There is simply no magic bullet that enables you to do one and complete when it comes to securing a computer environment. This book has been devoted to securing a network and its systems through the use of a firewall built on Linux. This chapter has introduced some of the other aspects of a security-in-depth process.

Using the tools available to you, such as those already introduced in this chapter, you can secure a computer and the network on which it resides. There are, of course, additional steps you can take to further enhance the security of the environment.

# ### KERNEL ENHANCEMENTS

There are certain things you can do with the Linux kernel to enhance its security. Naturally, anything you do at this, the lowest, level of the operating system will only serve to help the security of those things above it.

Two such kernel enhancements, SELinux and GrSecurity, are discussed in Chapter 13, “Kernel Enhancements.”
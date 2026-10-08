# CHAPTER 13 Testing and Reporting

There is risk involved. Black-hat hackers could somehow included their code in the packages released for a distribution. They may have penetrated the mirror servers from where many Linux distributions are downloaded and updated. They may take advantage of security issues before you're about to update a default system with fixes.

But there are safeguards. Open source developers test their software in the public eye. The source code is publicly available. If there are security issues, a great majority is revealed in the public testing process. Any issues that this process produces are publicized as soon as they are known by the community.

There are safeguards on the mirror servers that carry Linux distributions. Downloads with commands like yum and apt get GNU Privacy Guard (GPG) keys to ensure the integrity of a downloaded package. If you trust certain groups of developers, one option is to use security tools already included with live boot media.

# Some Tools Already Available on Live CDs

One excellent option for security tools is live boot media, such as CDs, DVDs, and USB keys. Perhaps the model for live media for Linux systems is the Knopix distribution. The operating system can be booted directly from a CD/DVD drive or even a downloaded ISO file is impressive. With the tools on the Knopix distribution, you can back up or recover troubled media. Even Nessus is included on the Knopix DVD as version of 6.2.

One impressive option for live DVD media is Ubuntu Pentest. It includes about 300 tools for penetration testing. Some of the tools for testing DNS servers are shown in Figure 13-10. While it is based on the Ubuntu distribution, the developers behind Ubuntu Pentest are not affiliated with Ubuntu or Canonical. It includes tools for port scanning, virtual private network probing, database testing, and more.

![](bbox=[0.125, 0.605, 0.655, 0.915])

FIGURE 13-10

Ubuntu Pentest Edition.
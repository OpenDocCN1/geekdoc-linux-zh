and read *IPCHAINS-HOWTO* as noted in *ipchains Documentation* on page 487 for further details.

# **NOTE**

> In order to get the most out of this chapter, you ought to be comfortable with the concepts and the administration of TCP/IP networking. *TCP/IP Networking Overview* on page 28 provides an overview and also includes references. Refer to those resources whenever you run across something in this chapter that is not familiar to you.

# ## CONFIGURING THE KERNEL FOR ipchains

Normally, when you install Red Hat 6.0 (or Red Hat 5.2 for *ipfwadm*), the initial kernel configuration will include support for *ipchains* (or *ipfwadm*, if Red Hat 5.2) and IP masquerading (see *IP Masquerading* on page 458).

However, if you install with “expert” mode¹ or you rebuild your kernel (see *Rebuilding and Recompiling the Kernel* on page 420 for a discussion of kernel rebuilding), then you will need to make sure that you select the appropriate kernel configuration parameters to support *ipchains* and IP masquerading. The configuration parameters, the proper choice (either to enable or disable), and descriptions are given in the *Linux IP Masquerade HOWTO*,² as cited in *Masquerading Documentation* on page 487. Make sure that you read through that document **before** proceeding!

# **NOTE**

> Red Hat 6.0 includes *ipchains* version 1.3.8. Any version of *ipchains* at or after 1.3.8 is considered stable. As of this writing, *ipchains* is at version 1.3.9. Visit the *ipchains* home page regularly and consider subscribing to the *ipchains* mailing list to keep up to date regarding upgrades and vulnerability reports. The *ipchains* home page and other resources are cited in *ipchains Documentation* on page 487.

# ## ipchains OVERVIEW

Linux *ipchains* provides for the capability to insert rules into the kernel that will cause all network packets to be filtered against those rules. The rules are
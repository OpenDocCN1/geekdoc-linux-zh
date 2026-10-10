An important source of specific technical information relating to the Internet and the TCP/IP suite of protocols are RFCs. RFC is an acronym for “Request for Comment” and is the standard means of submitting and documenting Internet protocol standards. There are many RFC repositories. Many of these sites are ftp sites and others provide World Wide Web access with an associated search engine that allows you to search the RFC database for particular keywords.

One possible source for RFCs is at Nexor RFC database (see http://pubweb.nexor.co.uk/public/rfcs/index/rfcl.html).

# # GENERIC NETWORK CONFIGURATION INFORMATION

The following subsections you will pretty much need to know and understand before you actually try to configure your network. They are fundamental principles that apply regardless of the exact nature of the network you wish to deploy.

# ## What Do I Need to Start?

Before you start building or configuring your network you will need some things. The most important of these are:

# ### Current Kernel Source

Because the kernel you are running now might not yet have support for the network types or cards that you wish to use you will probably need the kernel source so that you can recompile the kernel with the appropriate options.

You can always obtain the latest kernel source from ftp.kernel.org (see ftp://ftp.kernel.org/pub/linux/kernel). Please remember that ftp.kernel.org is seriously overloaded: the preferred way to get current sources is by downloading patches instead of whole tar files; moreover, you should first try to reach mirrors of the main ftp site, like ftp.funet.fi (see ftp://ftp.funet.fi/mirrors/ftp.kernel.org/pub/linux/kernel); also remember that every Linux site usually carries updated kernel sources.

Normally the kernel source will be untarred into the /usr/src/Linux directory. For information on how to apply patches and build the kernel you
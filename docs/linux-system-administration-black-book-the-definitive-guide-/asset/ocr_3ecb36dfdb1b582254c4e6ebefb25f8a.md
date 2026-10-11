# **In Depth**

The larger your network gets, the more difficult it is to manage individual user accounts on each and every machine. Fortunately, a service is available that enables you to centrally manage accounts you want to duplicate. This service is called the Network Information System (NIS). A newer and somewhat more advanced version is NIS+. It is important that you understand this service and whether it is right for you before implementing it. Otherwise, it will make your life more difficult rather than easier.

# ### Introduction To NIS And NIS+

The Network Information System was originally developed by Sun to provide a centralized mechanism for managing a user base on a large network. Back then, it was called the Sun Yellow Pages—the name had to be changed because British Telecom in the U.K. trademarked the phrase “Yellow Pages.” A newer and more security-savvy version of NIS is NIS+.

Unfortunately, each Linux distribution takes a different approach to whether to use NIS or NIS+. Because this book focuses on Red Hat Linux, its approach is discussed in depth. However, for those who are not using Red Hat, pointers are given to information on other distributions' implementations.

# ### Differences Between NIS And NIS+

Several differences exist between NIS and NIS+. This applies only to the pure implementations, however, because various distributions actually mix NIS and NIS+ together. One of the primary differences between NIS and NIS+ is the ability of NIS+ to use shadow passwords. Classic implementations of NIS do not support shadow passwords. Removing the ability to hide your master password file is not something many system administrators are willing to do. This is actually one of the primary reasons many administrators moved to NIS+, which does support the shadow suite.

However, Red Hat's implementation of the NIS server—and those of some other distributions—does support shadow passwords. You do not have to disable them to run an NIS server under Red Hat, because Red Hat is one of the distributions that use a mix of NIS and NIS+.

One of the main differences between NIS and NIS+ is the ability to encrypt data between server and clients. Go to www.suse.de/~kukuk/nisplus/download.html
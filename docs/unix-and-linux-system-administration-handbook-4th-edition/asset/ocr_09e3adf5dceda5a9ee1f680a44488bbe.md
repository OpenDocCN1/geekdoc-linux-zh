# 4 Access Control and Rootly Powers

![](bbox=[0.22, 0.24, 0.89, 0.56])

Access control is an area of active research, and it has long been one of the major challenges of operating system design. Generically speaking, operating systems define accounts for individual users, and they offer those users a smorgasbord of possible operations: editing text files, logging into remote computers, setting the system’s hostname, installing new software, and so on. The access control system is the black box that considers potential actions (user/operation pairs) and issues rulings as to whether each action is permissible.

In the case of UNIX and Linux, there isn’t really a single black box that implements access control. In fact, it’s more like a warehouse full of black boxes—and the warehouse is running out of storage space. In this chapter, we first go back to the dawn of UNIX to understand how the access control situation got to be the way it is. We then look at modern UNIX and Linux access control systems in theory and in practice, then review some tools that help make the administration of access control (and especially, the management of the all-powerful root account) relatively painless.

Chapter 22, Security, describes how to avoid unwanted and embarrassing superuser access by others. Chapter 32, Management, Policy, and Politics covers the relevant political and administrative aspects.
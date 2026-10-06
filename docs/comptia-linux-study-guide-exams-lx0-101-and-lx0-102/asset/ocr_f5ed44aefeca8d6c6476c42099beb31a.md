![](bbox=[0.147, 0.105, 0.335, 0.26])

Much of Linux system administration deals with handling mundane day-to-day tasks. Many of these tasks relate to users and groups: adding them, deleting them, configuring their environments, and so on. On a small system you may perform such tasks infrequently, but on a busy system you might adjust accounts frequently. In any event, you must know how to do these things. Another class of day-to-day tasks involves managing and reviewing log files. These are files that record detail of system operations, such as remote logins. Log files can be invaluable debugging resources, but if you aren't experiencing a problem, you should review them periodically to be sure everything is working as it should.

Many Linux tasks relate to time. Linux keeps time somewhat differently than other OSS, and understanding how Linux treats time is important. So are the skills needed to set the time in Linux.(Some automated tools can be very helpful, but you must know how to configure them.) You can also tell Linux to run particular jobs at specific times in the future. This can be handy to automate repetitive tasks, such as synchronizing data with other systems on a regular basis.

# # Managing Users and Groups

Linux is a multi-user system that relies on accounts—data structures and procedures used to identify users of a computer. Managing these accounts is a basic but important system administration skill. Before delving into the details, I describe a few basic concepts you should understand about user and group administration. With out of the way, I describe the tools and configuration files that you employ to manage users and groups.

# ## Understanding Users and Groups

Chances are you have a good basic understanding of accounts already. Fundamentally, Linux accounts are like accounts on Windows, Mac OS, and other OSs. Some Web sites uses accounts too. Nonetheless, a few details deserve explanation. These include Linux username conventions, the nature of Linux groups, and the way Linux maps usernames to group names that people generally use.

# ## Understanding Linux Usernames

Linux is fairly flexible about its usernames, although details vary from one utility to another. The most liberal Linux naming rules require usernames to begin with a letter and to be no more than 32 characters in length. Aside from the first character, numbers and
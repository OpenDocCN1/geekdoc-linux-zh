**The MySQL data directory.** The data directory is where the server stores its databases and status files. It's important to understand the structure and contents of the data directory so that you know how the server uses the filesystem to represent databases and tables, as well as where the server logs are located and what they contain. You should also know your options for managing allocation of disk space across filesystems should you find that the filesystem on which the data directory is located is becoming too full.

# ## 10.2 General MySQL Administration

General administration deals primarily with the operation of mysqld, the MySQL server, and with providing your users with access to the server. The following duties are most important in carrying out this responsibility.

**Server startup and shutdown.** You should know how to start and stop the server manually from the command line and how to arrange for automatic startup and shutdown when your system starts and stops. It's also important to know what to do to get the server going again if it crashes or will not start properly.

**User account maintenance.** You should understand the difference between MySQL user accounts and Unix or Windows login accounts. You should know how to set up MySQL accounts by specifying which users can connect to the server, where they can connect from, and what they are allowed to do. You'll also need to know how to reset forgotten passwords.

**Log maintenance.** You should understand what types of logs are available and which ones will be useful to you, as well as when and how to perform log maintenance. Log rotation and expiration are essential for preventing the logs from filling up your filesystem.

**Server configuration and tuning.** The MySQL server is highly configurable. Some of the operational characteristics that you can control include which storage engines the server supports, the default character set, and its default time zone.

Another configuration issue involves server tuning. Your users want the server to perform at its best. The quick-and-dirty method for improving how well the server runs is to buy more memory or to get faster disks. But those brute-force techniques are no substitute for understanding how the server works. You should know what parameters are available for tuning the server's operation and how they apply to your situation. At some sites, queries tend to be mostly retrievals. At others, inserts and updates dominate. The choice of which parameters to change will be influenced by the query mix that you observe at your own site.

**Multiple server management.** It's useful to run multiple servers on the same machine under some circumstances. You can test a new MySQL release while leaving your current production server in place, or provide better privacy for different groups of users by giving each group its own server. (The latter scenario is particularly relevant to Internet service providers.) For such situations, you should know how to set up multiple simultaneous installations.
Establishing your own groups, consisting of people who perform similar administrative functions, lets you avoid distributing the root password and still allow people to do their work. In this section, we'll implement group-level access control over nameserver files. The same principles apply to any files you choose to protect. Mail and web configuration files are other popular choices for group-based management.

# System Accounts

FreeBSD reserves some user account names for integrated programs. We discuss these unprivileged accounts in Chapter 19. For example, the nameserver runs under the user account `bind` and the group `bind`. If an intruder compromises the nameserver, she can access the system only with the privileges of the user `bind`.

Don't have users log in as these users. They're not set up as interactive accounts by design. What's more, do not allow the group of the system account `user` to own the files created for that function. Create a separate `user` and `group` to own program files. That way, our hypothetical intruder can't even edit the files used by the DNS server, further minimizing potential damage. If the program regularly updates the files (e.g., a database's backend storage), you must give the program access rights, but chances are that a human being doesn't ever need to edit that file. Similarly, there's no reason a database should be able to edit its own configuration file.

# Administrative Group Creation

The simplest way to create a group that owns files is to employ `adduser(8)` to make a user that owns them and then to utilize that user's primary group as the group for the files. Because we already have a user called `bind`, we'll create an administrative user `dns`. The username isn't important, but you should choose a name that everyone will recognize.

Give your administrative user a shell of *nologin*, which sets a shell of `/sbin/nologin`. This prevents anyone from actually logging in as the administrative user.
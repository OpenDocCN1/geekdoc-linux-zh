“resurrect” themselves or new system accounts were not added without your knowledge, and nonlogin system accounts don’t “suddenly” get assigned valid password hashes and shells.

# The Root Account

The root account is the key to your entire server kingdom (and to your entire network if the server in question serves as the central authentication server). Nothing is more important than the password to the root account in the Linux/Unix world. For this reason, you will not want to make your root password known to anyone else but yourself. Well, this is often easier said than done.

As you may already have found out, many of the administrative tasks, such as resetting a user's forgotten password, changing system configuration, and so on, require you to be root. If you’re the lone ranger who looks after the system(s) at your organization, keeping the root password safe is relatively easy. Follow the recommendations given earlier in this chapter about selecting strong passwords, change it often, never write it down, and so on. However, it is not uncommon in a company for system administration tasks to be shared by two or more people. In such cases, how do you safeguard the root password effectively? The more people who know it, the higher the likelihood it will be leaked to someone who shouldn’t know about it!

# TIP

> If you are the sole system administrator at your organization, it might be a good idea to record the root password in a sealed envelope and keep it in a secure location where only trusted company officers (such as the accountant or CTO) have access to it; a bank safety deposit box is a good choice. The idea here is that although you would want to keep the root password secret from others, you need to provide a way for “continuity” should you be unavailable, due to illness or any other reasons.

There are a number of ways to address the multiple administrator requirements, and we discuss two of them here:

+   - **Setting up multiple root users**—Instead of providing the root password to the people who need access, you can set up multiple root accounts. Suppose, for example, both Tasha and Carol require administrative access as part of their job. One way to track their root activities is to set up two separate accounts, say tasha-root for Tasha and carol-root for Carol, each with a unique (strong) password and each with a UID of 0. Whenever Tasha needs root privileges, she would log in as tasha-root or su as
to be successful when installing and managing NNLS, and grouped them together into the objectives covered in Chapters 2 and 3.

If you're comfortable with these skills, we're ready to move on with an introduction to the NNLS product. If not, you should spend some additional time learning the basics of Linux.

# What Is NNLS?

Since the 1980s, Novell has been *the* leader in the network operating system (NOS) industry. In the early days, this leadership was established with the NetWare OS, which provided mainly file and print services on local area networks (LANs). Prior to this time, these types of services were provided mostly by expensive Unix systems.

Novell took the innovative approach of creating an NOS that ran on the x86 Intel CPU. This allowed businesses to provide file and print services using relatively inexpensive server hardware. In fact, you didn't even need to buy server hardware; you could grab any desktop system with a networking board and install NetWare on it. NetWare was such an efficient operating system that you could get reasonable performance from off-the-shelf desktop systems. Even today, you may run into an organization, from time to time, that still has a NetWare server running on an old 80486 system.

There was, however, one glaring problem in the early days of NetWare. User accounts were local to each server. If your organization only implemented one server, this wasn't a problem. It was, however, a serious impediment for larger institutions that may have hundreds of servers. To use the services provided by a particular server, you had to have a user account on that server.

That doesn't sound too bad on a small scale, but imagine the administrative nightmare associated with a company that has thousands of users and hundreds of servers. In that world, you had to manage duplicate user accounts, passwords, and rights on multiple servers.

Believe me, it could become very cumbersome. The first network administration job I had back in the early 1990s involved this very situation. My organization had four LANs connected by routers; each was serviced by its own NetWare 3.1 server. That doesn't sound too bad, but I also had over a thousand users who needed access to each server. Maintaining consistent user accounts and passwords was difficult.

It was also difficult for the end users. If they were logged in to one particular server, but then needed to access files they had saved in their home
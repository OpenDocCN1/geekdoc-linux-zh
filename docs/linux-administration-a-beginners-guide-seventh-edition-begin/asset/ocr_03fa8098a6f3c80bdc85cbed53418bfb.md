# CHAPTER 8 Core System Services

functionality they provide. For the daemon's authors you decide that their daemon require
or relies on either xinetd or inet, then you need it—no two ways about it!

The inet and xinetd programs can be considered as daemon processes themselves. You probably know that daemons are special programs that, after starting, voluntarilyelease control of the terminal from when they started. The main mechanism by which
daemons can interface with the system-wide is via IPC channels, by sending
messages to the "super-server" or by logging to a file on.

inet functions as a "super-network" to other network-server processes,
such as Telnet, FTP, SMTP, and so on. It's a simple philosophy: Not all processes
(including those accept new connections) are called upon so often that require
a program to be running in memory all time. The main reason for the existence
of a super-server is to conserve system resources. Instead of needing to maintain
potzens of services loaded in memory waiting to be used, they are all listed
in inetd's configuration file, /etc/inetd.conf. On their behalf, inetd listens for
connections. Thus, only a single process needs to be in.

A secondary benefit of inetd falls to those processes needing network connectivity
but whose programmers do not want to have to write it into the system. The inetd
program will handle the network code and passing incoming network streams into
as process as standard input (STDIN). Any of the process output (STDOUT) is sent
back to the host that has connected to the process.

> Unless you are programming, you don't have to connect with inetd's
DIN/STDOUT feature. On the other hand, if you want to write a simple script and\make it available through the network, it's worth making this powerful tool.

As a rule of thumb, low-volume services (such as TFTP) are usually best run
through inetd, whereas higher-volume services (such as web servers) are better run as
stand-alone processes that are always in memory, ready to handle requests.

Current versions of Fedora, RHEL, openUSE, Mandrake, and even Mac OS
with a sharper connection of inet called xinetd—the name is an acronym for
"Extended Internet services daemon." The xinetd program accomplishes the task
as the regular inetd program: It helps to starts that provide Internet Services.
Instead of having programs automatically start up during system initialization
and remain unused until a connection arrives, xinetd stands in the gap
for those programs and their normal service port. As a result, when inetd
hears a service request meant for one of the services it manages, it starts or spawns the
appropriate service.

Inasmuch as xinetd is similar to inetd in function, you should realize that xinetd\includes a new configuration file format and a lot of additional features. The xinetd
daemon uses a configuration file format that is quite different from the classic inetd
configuration file format. (Most other variants of UNIX, including Solaris, AIX, and
FreeBSD, use the classic inetd format.) This means that if an application relies on\inetd, you may need to provide some manual adjustments to make it work. Of course,
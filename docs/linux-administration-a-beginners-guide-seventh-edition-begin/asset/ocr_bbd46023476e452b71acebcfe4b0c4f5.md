# 214 Linux Administration: A Beginner's Guide

Regardless of distribution, network configuration, and overall system design, every Linux-based system ships with some core services. These services init, systemd, logging daemon, cron, and others. The functions performed by these services might be simple, but they are also fundamental. Without their presence, a great deal of Linux's power would be useless.

This chapter will discuss each of the core services, in addition to useful system service xinetd. It also discusses each service's corresponding configuration file and the suggested method of deployment (if appropriate). You'll find that the sections covering these simple services are not terribly long, but don't neglect this material. Take some time to get familiar with these services. Hopefully, many creative solutions will be realized through the use of these services. This will inspire you more.

# The init Daemon

The init process is the patron of all processes. It is always the first process that gets started in any Linux/UNIX-based system. init is executed by the kernel and is responsible for starting all processes initially on a system. The process identification (PID) for init is 1. Should init ever fail, the rest of the system will likely follow suit.

The init daemon as it traditionally known has been replaced on most new Linux distributions by different solutions. One solution is an upstart (pun intended). Another recent solution is known as systemd and is discussed in its section later in this chapter.

The init process serves two roles: First, it can always be sure of its presence and, if necessary, make reference to it. The need to refer to init usually happens when a process dies before of all its spawned children processes have completed. This causes the children to inherit its parent process. A quick ps -ef command will show a number of processes that will have a parent ID (PPID) of 1. init also handles the various runlevels by executing the appropriate programs when a particular runlevel is reached. This behavior is defined by the etc/initab file or its equivalent in other distributions.

> If you want to be strictly technically correct, init is not actually the very first process that is run. To remain politically correct, we'll assume that it is! You should also keep in mind that some-called "security-hardened Linux systems" deliberately randomize the PID of init, so don't be surprised if you find yourself working on such a system and notice that the PID of init is not 1.
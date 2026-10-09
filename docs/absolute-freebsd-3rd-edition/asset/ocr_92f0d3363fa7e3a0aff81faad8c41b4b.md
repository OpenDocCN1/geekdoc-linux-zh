If the pagedaemon keeps running, incrementing the sr field in your
vmstat output, the kernel is working hard to provide memory. The host
might well have a memory shortage. Once the host start to use swap,
though, this memory shortage is no longer hypothetical. It might not be
bad, but it's not theoretical.

# ## Swap Space Usage

Swap space helps briefly cover RAM shortages. For example, if you're
untarring a huge file you might easily consume all of your physical
memory and start using virtual memory. It's not worth buying more
RAM for such occasional tasks when swap suffices. If a memory-starved
server runs a daemon that doesn't ever get called, that daemon will
eventually get mostly or entirely swapped out in favor of processes that
are performing work.

Only worry about swap space use when the system constantly pages
data in and out of swap.

In short, swap space is like wine. A glass or two now and then won't
hurt you and might even be a good choice. Hitting the bottle constantly
is a problem. If you have to swap constantly, consider a really fast but
durable SSD.

# ## CPU Usage

A processor can do only so many things a second. If you run more tasks
than your CPU can handle, requests will start to back up, you'll develop
a processor backlog, and the system will slow down. That's CPU usage
in a nutshell. If performance is unacceptable and top(1) shows your
CPU hovering around 100 percent all the time, CPU utilization is
probably your problem. While new hardware is certainly an option, you
do have other choices. For example, investigate the processes running
on your system to see whether they're all necessary. Did some junior
sysadmin install a SETI@Home client to hunt for aliens with your spare
CPU cycles? How about a Bitcoin miner? Is anything running that was
important at one time, but not any longer? Find and shut down those
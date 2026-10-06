# UNIX SYSTEM MANAGEMENT PRIMER PLUS

Following are some important points to take into account planning for upgrade capacity.
You can read more about each of these points in Chapter 11.

+   - Ensure that you have enough disks and controllers to accommodate RAID configurations on the old world.

+   - Assuming your processing needs have not decreased, upgrade one multiprocessor system with another multiprocessor system. If you upgrade to a single-processor machine, you may incur a severe performance hit if the new processor is faster than that of the old processors; a faster processor cannot replace the concurrency of multiple processors.

+   - Ensure that the total network capacity of the new system meets or exceeds that of the old system. Take into account new technologies—such as upgrading 100Mbit Ethernet to Gigabit Ethernet—as well as tricks such as interfacing.

+   - Verify the maximum capacity of each subsystem on your new systems; these limitations may affect the systems you choose for your upgrade. For example, a Sun Enterprise 220R has a maximum memory capacity of 2GB. If your application required 4GB of memory, you would have to purchase an Enterprise 420R, which supports up to 4GB of memory.

+   - If you have decided to replace a single system with multiple systems to better distribute the load of your applications, ensure that the total processor capacity, memory, and bandwidth exceed that which is available on the original system. In fact, many organizations choose to purchase systems identical to the original but of higher capacity, because they already know the performance limitations of their applications on that server configuration.

# Planning a Smooth Transition to Upgraded Hardware

Implementing a smooth transition between the old hardware and the new hardware should be included in the goals of any upgrade. A successful upgrade is one in which end users don't notice the change, let alone experience problems with the new hardware. The last things any administrator wants to worry about during an upgrade are user problems and server uptime.

Some of the more effective ways to achieve this smooth transition include redundancy and hot swapping.

# Incorporating Redundancy into the Transition

Redundancy—keeping the system functioning with redundant hardware while new hardware is installed—is the most straightforward way to any transition to upgraded hardware. You can use redundancy, for example, to upgrade one or more servers by keeping other servers in production serving requests. Load-balancing hardware can provide redundancy, If you use load-balancing hardware while upgrading two servers, you can upgrade one server at a time without an interruption in service. The load-balancing hardware sends all requests to whichever server is running at the time.
# # Chapter 4
## Monitoring the System

A computer system consists of processors, memory, and I/O devices. Users log in to the system and run business jobs or applications. Network software and interface cards connect users over the network to the computer system. This chapter focuses on monitoring the processors and memory components, as well as the user activity on the system. Disks, networks, databases, and applications are covered in separate chapters.

# ### Identifying Important System Monitoring Categories

This chapter identifies important system resources to monitor, so that you can detect faults, avoid problems, and ultimately ensure availability. Many important system resources can be monitored for events and faults, and many system management tools are available with which to monitor them. Instead of categorizing based on specific hardware components, this chapter relates its descriptions of tools to the different ways of monitoring your system. For example, your focus as an operator may be on watching for system faults and failures, software or hardware configuration changes, system resource usage, performance management, or security. This chapter tries to show a tool's role, if any, in each of these monitoring categories.

# ### Monitoring System Configuration Changes

This category includes monitoring for changes in hardware and software configurations that can be caused by an operating system upgrade, patches applied to the system, changes to kernel parameters, or the installation of a new software application, for example. The root cause of system problems can often be traced back to an inappropriate hardware or software configuration change. Therefore, it is important to keep accurate records of these changes, because the problem that a change causes may remain latent for a long period before it surfaces.

Adding or removing hardware devices typically requires the system to be restarted, so configuration changes can be tracked indirectly (in other words, remote monitoring tools would notice system status changes). However, software configuration changes, or the installation of a
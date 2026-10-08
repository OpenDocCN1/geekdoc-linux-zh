PRM can be used in conjunction with HP GlancePlus to adjust system configuration. For example, if an administrator detects unwanted system load for a PRM group, GlancePlus can be used to lower that group's entitlement dynamically.

Normally, if one PRM group doesn't need its system resources, PRM allocates them to other groups that may need them. However, PRM can also help with capacity planning, by allowing resource maximums to be specified. Thus, if an administrator knows that a system will soon have 25 percent more users, the administrator can allocate a maximum of 80 percent of system resources to simulate the upcoming load.

Although PRM can ensure that users get a certain percentage of CPU resources, it can't prevent all system performance problems. For example, an application sending large network packets but using very little CPU resources can starve a more critical application, because network bandwidth is not controlled by PRM.

PRM can also be used to adjust workload dynamically in a high availability environment. For example, if three MC/ServiceGuard packages are each running with similar PRM entitlements, and one package fails to another system, this can be automatically detected, and a new PRM configuration can be applied, giving the two remaining packages higher entitlements.

Despite these efforts, you still are likely to have some performance problems to investigate. The next sections describe how to use the data collected by the various performance monitoring tools to address performance issues.

# ## Detecting CPU Contention

UNIX commands, such as top and uptime, and performance monitoring tools, such as Glance-Plus, provide CPU utilization information. CPU utilization and run queue length can be used together to determine whether a CPU bottleneck exists. High CPU utilization alone may not be indicative of a problem; batch jobs may be consuming the CPU remaining from interactive users. However, if interactive users are getting poor response times, that indicates a problem, such as a system bottleneck.

If the run queue is greater than one, the likelihood that a CPU bottleneck exists increases as the CPU utilization gets closer to 100 percent. Make sure that the high utilization and large run queue are sustained for a period of time.

If a CPU bottleneck is identified, recovery may depend on the applications and processes consuming large amounts of CPU. This can be determined by using performance monitoring tools such as GlancePlus. Applications spending the majority of their time in system code may need to be changed. In some cases, an application can be recompiled, optimized, or restructured to improve its performance. If batch processing is causing a problem, a job scheduler can be used to route jobs to less utilized systems. Less important applications, such as batch processes, can also be reconfigured to run at a lower priority by using nice. An application may need to be aborted or moved to another system if it continually thrashes with other applications. Tools such as PRM can be enabled or reconfigured to handle resource allocation among applications or users. PRM can keep applications within configured CPU limits.
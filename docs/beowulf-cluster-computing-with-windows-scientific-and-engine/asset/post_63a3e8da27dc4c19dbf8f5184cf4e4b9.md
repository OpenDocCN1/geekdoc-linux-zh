
users submit jobs to a queue in order to specify the work to be performed. (Once a job has been submitted, the user can request status information about that job at any time.) The jobs then wait in the queue until they are scheduled to start on the cluster. The specifics of the scheduling process are defined by the policy rules. At this point, resource management mechanisms handle the details of properly launching the job and perhaps cleaning up any mess left behind after the job either completes or is aborted. While all this is going on, the workload management system is monitoring the status of system resources and accounting for which users are using what resources.

![](img/e2283ffaea56e577ac05056b4bb738fc_329_0.png)

**Figure 13.1**  
Activities performed by a workload management system.

## 13.2 Workload Management Activities

Now let us take a look in more detail at each of the major activities performed by a cluster workload management system.

### 13.2.1 Queuing

The first of the five aspects of workload management is *queuing*, or the process of collecting together “work” to be executed on a set of resources. This is also the portion most visible to the user.

The tasks the user wishes to have the computer perform, the work, is submitted to the workload management system in a container called a “batch job”. The batch job consists of two primary parts: a set of resource directives (such as the amount of memory or number of CPUs needed) and a description of the task to be executed. This description contains all the information the workload management system needs in order to start a user’s job when the time comes. For instance, the job description may contain information such as the name of the file to execute, a list of data files required by the job, and environment variables or command-line arguments to pass to the executable.

Once submitted to the workload management system, the batch jobs are held in a “queue” until the matching resources (e.g., the right kind of computers with the right amount of memory or number of CPUs) become available. Examples of real-life queues are lines at the bank or grocery store. Sometimes you get lucky and there’s no wait, but usually you have to stand in line for a few minutes. And on days when the resources (clerks) are in high demand (like payday), the wait is substantially longer.

The same applies to computers and batch jobs. Sometimes the wait is very short, and the jobs run immediately. But more often (and thus the need for the workload management system) resources are oversubscribed, and so the jobs have to wait.

One important aspect of queues is that limits can be set that restrict access to the queue. This allows the cluster manager greater control over the usage policy of the cluster. For example, it may be desirable to have a queue that is available for short jobs only. This would be analogous to the “ten items or fewer express lane” at the grocery store, providing a shorter wait for “quick tasks.”

Each of the different workload management systems discussed later in this volume offers a rich variety of queue limits and attributes.

### 13.2.2 Scheduling

The second area of workload management is scheduling, which is simply the process of choosing the best job to run. Unlike in our real-life examples of the bank and grocery store (which employ a simple first-come, first-served model of deciding who’s next), workload management systems offer a variety of ways by which the best job is identified.

As we have discussed earlier, however, best can be a tricky goal, and depends on the usage policy set by local management, the available workload, the type and availability of cluster resources, and the types of application being run on the cluster. In general, however, scheduling can be broken into two primary activities: policy enforcement and resource optimization.

Policy encapsulates how the cluster resources are to be used, addressing such issues as priorities, traffic control, and capability vs. high throughput. Scheduling is then the act of enforcing the policy in the selection of jobs, ensuring the priorities are met and policy goals are achieved.

While implementing and enforcing the policy, the scheduler has a second set of goals. These are resource optimization goals, such as “pack jobs efficiently” or “exploit underused resources.”

The difficult part of scheduling, then, is balancing policy enforcement with resource optimization in order to pick the *best* job to run.

Logically speaking, one could think of a scheduler as performing the following loop:

- 1. Select the best job to run, according to policy and available resources.
- 2. Start the job.
- 3. Stop the job and/or clean up after a completed job.
- 4. Repeat.

The nuts and bolts of scheduling is, of course, choosing and tuning the policy to meet your needs. Although different workload management systems each have their own idiosyncrasies, they typically all provide ways in which their scheduling policy can be customized. Subsequent chapters of this book will discuss the various scheduling policy mechanisms available in several popular workload management systems.

### 13.2.3 Monitoring

Resource monitoring is the third part of any cluster workload management system. It provides necessary information to administrators, users and the scheduling system itself on the status of jobs and resources. There are basically three critical times that resource monitoring comes into play:

- 1. When nodes are idle, to verify that they are in working order before starting another job on them.
- 2. When nodes are busy running a job. Users and administrators may want to check memory, CPU, network, I/O, and utilization of other system resources. Such checks often are useful in parallel programming when users wish to verify that they have balanced their workload correctly and are effectively using all the nodes they’ve been allocated.
- 3. When a job completes. Here, resource monitoring is used to ensure that there are no remaining processes from the completed job and that the node is still in working order before starting another job on it.

The Microsoft Windows 2000 operating system provides several built-in tools for monitoring. The most common is the Computer Management console. It provides system details and allows administrators to monitor services, file I/O, user management information, and many other things. Figure 13.2 shows the Computer Management console.

![](img/e2283ffaea56e577ac05056b4bb738fc_332_0.png)

**Figure 13.2** Windows 2000 Computer Management console.

Another built-in tool is the Performance Monitor. It lets you monitor resource utilization on multiple nodes simultaneously. Figure 13.3 shows the Performance Monitor console.

Both of these tools rely upon Windows Management and Instrumentation (WMI), which is a built-in service that is part of any Windows 2000 installation and is also available for Windows NT. It acts as a COM+ object that allows administrators and users to develop monitoring tools on it using any language, including scripting languages.

![](img/e2283ffaea56e577ac05056b4bb738fc_333_0.png)

**Figure 13.3** Windows 2000 Performance Monitor console.

### 13.2.4 Resource Management

The fourth area, resource management, is essentially responsible for the starting, stopping, and cleaning up after jobs that are run on cluster nodes. In a batch system resource management involves running a job for a user, under the identity of the user, on the resources the user was allocated in such a way that the user need not be present at that time.

Starting jobs typically involves some form of secure impersonation. Microsoft Windows 2000, like other operating systems, provides mechanisms for doing this securely. Typically this is handled by the use of services or COM+ objects that can create a user process token for a given user and use it to run a job as that user. Short of a mechanism like this, users typically must supply their username and password at run time to authenticate to the system and start processes as them. This obviously does not work in a batch situation.

Once processes are started, the resource management system has to be able to enumerate those associated with a given job. Windows 2000 provides the *job object* for this purpose. All processes created within a job object can be monitored and

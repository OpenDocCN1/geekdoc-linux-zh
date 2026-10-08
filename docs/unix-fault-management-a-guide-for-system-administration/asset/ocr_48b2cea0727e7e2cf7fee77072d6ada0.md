Similarly, hardware external to the managed system may also be important. The failure of a network router can prevent any data from getting to the managed system.

Here is a sampling of some of the important external services that you need to monitor in your environment:

+   - Name servers, such as DNS and Network Information Service servers
- File servers
- E-mail server
- Directory service, such as Novell Directory Service
- Boot server
- Software license server
- Web proxy server
- News server

You can set up monitoring of these services if you know the processes that make up the application. Process failures can be detected, as mentioned earlier. More proactive approaches involve actually trying to use the service to see whether it is working properly. Many other conditions are equally important, but are much more difficult to detect, such as an expired software license, which could cause you unexpectedly to be denied access to a key application.

Redundancy of these network services is a key to maintaining the availability of your server. However, this alone is not sufficient. Configuration problems and issues such as software licenses can still prevent the use of an important service.

# ## Resource and Performance Events

In addition to looking for failure events, monitoring resource usage and performance are important. If users are unable to access critical system resources, you might as well consider the system down. The system operator needs to be notified when resource utilization reaches certain thresholds, so that measures can be taken to avert a crisis. The network, CPU, process table, filesystem, and memory are examples of critical system resources that should be monitored.

High utilization alone is not sufficient to indicate a problem. It could just indicate that you are getting optimal use of your server. You also need to determine whether system bottlenecks exist and, if so, which applications are being delayed.

This book distinguishes between resource usage and performance. Particular types of system resources have limitations. For example, you can run out of filesystem space, swap space, processes in the process table, files in the file table, system semaphores, or shared memory. You monitor resource usage so that you know when the system usage is approaching these configured limits. Performance describes the balance between CPU, memory, and I/O usage, and the relative usage of different applications. You want to avoid CPU, memory, and I/O bottlenecks and also ensure that high-priority applications are not blocked behind low-priority workloads. Application response time and throughput are also important to track, because those are the performance measures most visible to the users of an application.
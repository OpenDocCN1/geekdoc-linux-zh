
## 3.2.5 Will Multiple Applications Run on a Single Member?

When we plan how the applications will be mapped to cluster members, we have the choice of dedicating specific members to a specific application or running multiple applications on a single cluster member. One to one mapping of applications to servers in a cluster (or standalone servers) can simplify tuning, support, and computing resource management for the members. On the other hand, maximizing the investment in platforms is an incentive to run multiple applications on the same box.

This decision can have a lot to do with the nature of the applications and the services available in the operating system to simplify and control the running of multiple applications using resource management.

- Do the applications have extreme resource consumption patterns that make sharing a host difficult to optimize?
- Would utilizing the *Tru64* UNIX Operating system’s resource management facilities (including processor sets, class scheduling, and the ARMTech fair share scheduler) simplify resource management on a server?
- Would multiple applications conflict because they run at different times of the day?
- Even if a set of applications can share a host, how does the combination of applications affect the system if they were to failover to another cluster member, which is already running a different set of jobs?
- Would the doubling up of applications allow the overall cluster to be smaller, thus simplifying the cluster at large configuration and management?

### 3.2.5.1 Example

In the case of the Biotech cluster, some of the applications could be run on the same member without major risk:

- The web server and database can run on a common platform because neither is expected to be an excessive resource consumer. Also, the web server interfaces with the database so running them on the same platform will improve the performance seen by the web server’s clients.

After this, the resulting workloads could be reduced to:

- Home written compute application
  No change from earlier description.
- Small standard database application and Web Server Application
  A single ES40 system with four CPUs, 8 GB of memory, two HBAs, and 600GB of storage would be adequate.
- User logins and development environment application
  If run on a single system, one ES45 with four CPUs, 8GB of memory, and two HBAs would be more than adequate. The total storage required would be 400GB. Network interface requirements would be moderate. A single logical interface implemented with two Fast Ethernet physical NICs would be adequate.

## 3.2.6 Will There Be Homogeneity of Member Systems?

The *TruCluster Server* software supports homogeneous or heterogeneous cluster configurations. Homogeneous clusters have members that consist of the same model and computing resources and have the advantage of simplifying management of the cluster in a number of ways. First, the site does not need to worry about keeping track of which systems have which computing resources when assigning applications within the cluster either statically or when failover occurs. Moreover, tuning and hardware and software maintenance through patches can be more standardized. Heterogeneous environments can be more cost-effective as the site either pulls together existing hardware of different model types to make the cluster, or exactly matches systems to the applications when they are drastically different needs.

### 3.2.6.1 Example

In the Biotech cluster, no legacy servers will be included in the cluster, and the ease of management of a homogeneous cluster is deemed a priority so the design will center on a homogeneous configuration.

- 3 ES45s — Compute application
- 1 ES45 — Database and Web Server
- 1 ES45 — User Logins

Note that in the case of the Database and Web Server system, the server will have more power than is absolutely required by the application in the interest of keeping the cluster homogeneous.

## 3.2.7 Is Availability Insured By Providing Additional Computing Capacity?

Almost all cluster solutions have high availability as a design criterion. In this case, the cluster must have enough spare computing power so that if a member fails, the applications running on it can be moved to another cluster member and continue to run. The major question is what level of service is required for the application when moved to a new member. If it is the same as before the original member failed, then free computing capacity of the same amount as the failed member must be available to failover to. For example, if the cluster has one application running on one member, another member of the same size is required to meet this requirement. The key is that this additional member is idle until such time as the first member fails, causing the application to failover. Having 100% idle computing power is the worst case and can be reduced if you do the following:

- As cluster size increases, the overhead of the spare capacity can be amortized over a number of members. For instance, if the cluster has two applications on two members, it requires a third idle member to take either of the two applications if the current member fails.

+   - The site may be willing to live with degraded level of service or the termination of less essential applications when a failure condition exists. For instance, a two-node cluster with two applications could either allow both applications to run on a single member when one fails with degraded performance, or terminate the less important application when failover occurs.

Complicating all of this failover planning is the computing resources required by the applications of the cluster and whether or not the cluster will be homogeneous in member systems. For instance, if one workload requires an extremely large server, and other applications in the cluster do not, an additional large server would be required for failover of the large application – independent of the smaller needs of the remaining applications.

# 3.2.7.1 Example

The Biotech cluster design has already been narrowed down to a homogeneous cluster. This makes failover planning easier. The minimum number of members to support the applications without considering failover is already 5. The cost of adding a 6th member as a failover host is not excessive to the site’s plans so that solution will be taken. This results in a cluster as follows:

+   - 3 ES45s - Compute application
+   - 1 ES45 - Database and Web Server
+   - 1 ES45 - User Logins
+   - 1 ES45 - Failover host for the other jobs

# 3.2.8 Is There Room to Scale Out Cluster Size In Terms of Number of Members?

Many sites like to be able to design into a solution the ability to grow in computing capacity over time. Sometimes it is known up front that the application load will increase over time; other times it’s simply the desire to be ready in case it does, due to an unforeseen event. With a cluster, the computing power can be grown in two dimensions – the size of the members and the number of members.

The changes that can trigger a need to grow the cluster by adding new members are:

+   - The addition of new applications
+   - The number of members running instances of a multi-instance application
+   - Moving applications that were sharing member systems onto their own member systems

In the case of the number of cluster members, the currently supported maximum is eight nodes. This means that if a site would like to be able to grow, it needs to start with a cluster size of less than this value.
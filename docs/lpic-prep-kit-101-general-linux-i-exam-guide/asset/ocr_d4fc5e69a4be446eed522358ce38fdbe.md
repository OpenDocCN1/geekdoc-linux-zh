availability might be only during working hours. The increased cost for a more complex solution for disaster recovery is often justified when a server fills a critical role or requires a high level of availability.

# # Types of Backup Strategies

You can choose from several types of strategies when deciding which is right for you. Some of your options include

+   - Clustering
+   - Standby server
+   - Duplicate or backup server
+   - Backup and restoration

# ## Clustering

*Clustering* consists of two or more computers that share access to a central data repository, such as a RAID array. Each of these servers can run different applications. If one member of the cluster goes down, another member will take over the downed server's job. This change is invisible to users. If you require 24-hour availability, this solution will provide it. However, it is expensive both as far as initial setup costs and the expense of ongoing management.

# ## Standby or Failover Server

With this solution, a server that is identical to the online server is configured but is not available for users. It is live and listens to the main server to ensure it is available. When the main server goes offline, the standby server steps forward to handle the workload. It presents itself to the users with the same IP address and name, so the users never know which server is handling the workload. This is less expensive than clustering, but still is primarily used for systems that need 24-hour availability.

# ## Duplicate or Backup Server

*The duplicate or backup* server is installed with the same applications as the main server but is left offline until the original server goes down. The change over is not instantaneous as it is in the two previous solutions. You will have to bring up the new server and connect it to any volatile data, perhaps by moving hard disks from one computer to another or connecting it to a RAID array. This solution is less expensive but does result in some downtime if the main server dies.
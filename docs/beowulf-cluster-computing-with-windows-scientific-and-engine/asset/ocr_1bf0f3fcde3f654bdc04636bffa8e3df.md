![](bbox=[0.33, 0.26, 0.67, 0.3])

**Figure 13.3** Windows 2000 Performance Monitor console.

# 13.2.4 Resource Management

The fourth area, resource management, is essentially responsible for the starting, stopping, and cleaning up after jobs that are run on cluster nodes. In a batch system resource management involves running a job for a user, under the identity of the user, on the resources the user was allocated in such a way that the user need not be present at that time.

Starting jobs typically involves some form of secure impersonation. Microsoft Windows 2000, like other operating systems, provides mechanisms for doing this securely. Typically this is handled by the use of services or COM+ objects that can create a user process token for a given user and use it to run a job as that user. Short of a mechanism like this, users typically must supply their username and password at run time to authenticate to the system and start processes as them. This obviously does not work in a batch situation.

Once processes are started, the resource management system has to be able to enumerate those associated with a given job. Windows 2000 provides the *job object* for this purpose. All processes created within a job object can be monitored and
For example, my login name at one time was simply chris. As a result of poor planning, another user in one of our company’s other offices had a login name of chris. The two offices were not connected using TCP/IP; however, when a SLIP line was introduced between the two offices, there were suddenly problems. The most obvious problem was that each of us with the login chris could access files belonging to the other.

While changing the login name for one user solved the immediate problem, it did not address the real security issue — each of the users should have had an account for each machine on the network, each with the same User ID (UID).

As a first step toward providing equivalency, keep in mind the following points when setting up your network.

+   - You are essentially duplicating the /etc/passwd and /etc/group files on all of the machines in your organization. As a result, each user must have a unique login name and UID.
+   - Group permissions cross system boundaries, so the same guidelines apply for groups. The same groups with the same Group IDs (GID) must exist on all machines.

# Configuring Host Equivalency

Host equivalency must be set up and operational to use the commands rcmd (rsh) and rcp. The system administrator configures host equivalency using the file /etc/hosts.equiv, as shown in Figure 10.1. This file consists of host names, one per line (it is also a good idea to document in the file who the network administrator is).

Each entry in the hosts.equiv file is trusted. This means that users, with the exception of root, on the named machine can access their equivalent accounts on this machine without a password.

![](bbox=[0.13, 0.9, 0.88, 0.99])
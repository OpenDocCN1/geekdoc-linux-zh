# Configuration Server

If you are setting up custom JumpStart installations for systems on the network, you have to create a directory on a server called a configuration directory. This directory contains all the essential custom JumpStart configuration files, such as the rules file, the rules.ok file, the class file, the check script, and the optional begin and finish scripts.

The server that contains a JumpStart configuration directory is called a configuration server. It is usually the same system as the install and boot server, although it can be a completely different server. The configuration directory on the configuration server should be owned by root, and should have permissions set to 755.

# Setting up the Configuration Server

# STEP BY STEP

# 21.3 Setting Up a Configuration Server

To set up a configuration server, follow these steps:

+   1. Choose the system that acts as the server, and log in as root.
2. Create the configuration directory anywhere on the server (such as /jumpstart).
3. To be certain that this directory is shared across the network, edit the /etc/dfs/dfstab file, and add the following entry:
   share -F nfs -o ro,anon=0 /jumpstart
4. Execute the /etc/init.d/nfs.server start command. If the system is already an NFS server, you need to only type shareall and press Enter.
5. Place the JumpStart files (that is, rules, rules.ok, and class files) in the /jumpstart directory. The rules, rules.ok, and class files are covered later in this section.

```
share -F nfs -o ro,anon=0 /jumpstart
```
![](bbox=[0.05, 0.1, 0.13, 0.15])

Access Control Operators

# ## Access Control Operators

An access control operator is a tag that is used to specify the type of access an ACL is permitted or denied. The access control operator is followed by the *allow* or *deny* keyword and then the ACL name. There are many types of operators provided in the `squid.conf` file. The most common access operators are listed in the table below.

| Operator | Used To |
| :--- | :--- |
| `http_access` | Allow or deny access to HTTP ports. For example, `http_access allow | deny hostname | all` |
| `icp_access` | Allow or deny access to send and receive ICP queries to and from caches. |
| `no_cache` | Remove matching patterns from the cache. |

# ## How to Implement Access Control in a Proxy Server

# ### Procedure Reference: Install Squid

To install Squid:

+   1. Log in as root.
2. Mount the Linux installation media that contains Squid.
3. Navigate to the /media/[name of the media]/Server directory.
4. At the command line, enter `rpm -ivh squid-(version).(release).rpm` to install Squid.
5. Enter `rpm -qi squid` to verify that Squid has been installed.
6. Unmount the installation media.

# ### Procedure Reference: Configure Squid

To configure Squid:

+   1. Log in as root.
2. Using an editor, open the `/etc/squid/squid.conf` file.
3. Locate the line the "http_port 3128" and uncomment it to specify that the squid daemon will listen on port 3128 for requests.
4. Enter `cache_dir` Cache location path *(Maximum cache size)* *(Maximum number of subdirectories in first tier)* *(Maximum number of subdirectories in second tier)* to specify the cache requirements.
5. Save and close the file.
6. Enter `service squid start` to start the Squid service.
7. Enter `chkconfig squid on` to enable the Squid service during system startup.
8. On the system that has access to the proxy server, modify the browser settings with respect to the proxy server hostname and port.
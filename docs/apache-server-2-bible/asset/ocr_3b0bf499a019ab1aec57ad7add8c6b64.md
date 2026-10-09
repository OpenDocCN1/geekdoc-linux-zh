# **Monitoring packet fragments**

The Linux kernel controls the number of unprocessed UDP packet fragments it can handle using a high-to-low range. When unprocessed UDP packet fragment size reaches the high mark (usually 262144 bytes or 256K), the kernel throws away the incoming packet fragments. In other words, when UDP packet fragments reach the high mark, packet loss starts. The loss of packet fragments continues until the total unprocessed fragment size reaches a low threshold (usually 196608 bytes or 192K).

Because NFS protocol uses fragmented UDP packets, the above-high-to-low threshold used by Linux matters a great deal in NFS performance. You can view the current value of your high threshold size by running the `cat /proc/sys/net/ipv4/ipfrag_high_thresh` command. Similarly, you can view the low threshold value by running the `cat /proc/sys/net/ipv4/ipfrag_low_thresh` command. You can change the high values by running the `echo high_number > /proc/sys/net/ipv4/ipfrag_high_thresh`, and similarly, running the `echo low_number > /proc/sys/net/ipv4/ipfrag_low_thresh` changes the low number.

# ## Replicating contents among Web servers

Typically, content is developed and placed on a single (master) server and then is distributed to all the other Web servers that participate in the Web network. In this section I discuss a tool called `rdist`, which allows you to distribute contents from one Linux system to others.

# ## Using rdist to distribute files

The `rdist` program enables you to maintain identical copies of files over multiple hosts. It uses either the `rcmd` function calls or the remote shell (`rsh`) to access each of the target host computers.

The easiest way to get `rdist` working is to create a common account on all the machines involved and create `.rhosts` files for each target Web server system so that the common user on the name server host is allowed to run `rsh` sessions. For this purpose, create a user called `httpd` on all three systems involved. On each of the Web server systems, add a `.rhosts` file in the home directory of the `httpd` user. This file contains the host name of the `rdist` server in a single line.

The `.rhosts` file must be owned by the root user and be read-only for everyone else. This allows a user called `httpd` on the `rdist` server to run remote shell sessions on each Web server system. If you have created a back-end network as instructed in previous sections, you should use the `rdist` server’s host name associated with the back-end network interface, which enables you to keep the `rdist`-generated file traffic in the back-end network; thus, the packets will not compete with your Web traffic. The next step is to create a distfile for `rdist`. A distfile is a text file that contains instructions for `rdist` on how to perform the file distribution task. Listing 23-2 shows one such distfile, `rdist_distfile`.
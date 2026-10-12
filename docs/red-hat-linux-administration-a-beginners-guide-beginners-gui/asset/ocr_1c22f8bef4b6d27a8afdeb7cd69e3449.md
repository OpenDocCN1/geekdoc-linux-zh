decision, you can treat each campus as a single site and decide how many NIS servers need to be deployed. If you intend to keep a uniform NIS space, there should be only one NIS master server; the rest of the NIS servers at other campuses should be slaves.

# ## Module Summary

In this module, we discussed the process of installing master NIS servers, slave NIS servers, and NIS clients, as well as how to use some of the tools available on these servers. Here are the key points to remember about NIS:

+   NIS is a data-sharing and lookup service. NIS servers do not perform authentication.

+   Because anyone in your network can join an NIS domain, it is assumed that your network is already secure. Most sites find that the benefits of this arrangement outweigh the risks.

+   Once the makefile is set up and **ypinit** has been run, master NIS servers do not need additional setups. Changes to the files that you need to share via NIS (such as */etc/passwd*) are updated and propagated by running **cd /var/yp; make**.

+   NIS slave servers are listed on the master server’s file, **/var/yp/ypservers**.

+   NIS slave servers receive their information from the server via a server push.

+   Setup of an NIS slave server is little more than running the **ypinit -s** command.

+   NIS clients need their */etc/yp.conf* and */etc/nsswitch.conf* files to be adjusted, and then only the **ypbind** program is set running.

# # Module 17 Mastery Check

+   Can NIS allow sharing on any tabular file?

+   What is the main benefit of using NIS?

+   What is one of the two ways that NIS can be queried for the data it keeps track of?

+   A NIS database can also be referred to as a A. Flag B. Map C. Cookie D. None of the above
# # 10.1.3 ARPWatch

Another item to be discussed in Chapter 11 is ARPWatch. ARPWatch is software to watch for new network devices on the network. ARPWatch can be helpful for auditing the devices on the network, especially wireless networks.

# ## 10.2 Rootkit Checkers

A rootkit is a piece of software or a grouping of software that attempts to exploit one or more vulnerabilities with the goal of enabling an attacker to gain elevated privileges or perform any other type of attack against the target. Frequently, rootkits are used by less skilled attackers who use the software built by another attacker but don't really understand the underlying exploit; they're just interested in the results.

Many rootkits not only run the initial exploit to give the attacker root privileges but also attempt to mask or hide the fact that an attack has been launched. They do this by deleting log files or certain entries from log files, planting trojan-horse versions of programs, and employing other means. There is also nothing stopping an attacker from chaining rootkits together for multiple levels of deception and possible exploit.

Like network-centric attacks, rootkits frequently have signatures or leave other traces that identify them. These traces and signatures might be the aforementioned removal of log files, the presence of one or more processes, or other changes to the system that are specific to the rootkit software or the exploit.

Also as with network-centric attacks, there is software to search for the signatures and traces of rootkits as well. One such application is Chkrootkit.

# ### 10.2.1 Running Chkrootkit

Before you can run Chkrootkit, you need to get it. Chkrootkit can be downloaded from [http://www.chkrootkit.org/](http://www.chkrootkit.org/). After it's downloaded, Chkrootkit needs to be unpacked and compiled:

```
```
tar -zxvf chkrootkit.tar.gz
cd chkrootkit-<NNNN>
make sense
```
```

Yes, that does say `make sense` in the code example. Although Chkrootkit is a shell script, there is some additional functionality gained by compiling the code. Compiling is not required, but because it's quick and adds some additional levels of checking, I'd recommend doing so. Specifically, compiling Chkrootkit will enable these additional checks:

+   - ifpromisc
  - chklastlog
  - chkwtmp
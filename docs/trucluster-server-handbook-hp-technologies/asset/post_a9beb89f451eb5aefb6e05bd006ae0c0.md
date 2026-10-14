
# ./cvtpid 524289
1
cluster pid = 524289; standalone pid = 1

# ./cvtpid 525353
1065
cluster pid = 525353; standalone pid = 1065

# cat cvtpid
#! /usr/bin/ksh
if [[ $# != 1 ]]
then
    print "USAGE: $0 <pid_to_converts>"
    exit 1
fi
sapid=$(print "$1 % (2 ^ 19 )" | bc )
print cluster pid = $1; standalone pid = $sapid

Let’s start a process on cluster member sheridan. Note the PID of 1067727.

[sheridan]
# cat &
[1]      1067727

On molari, let’s see if we can see the process. No. Nothing appears except my grep command itself.

[molari]
# ps -Ao pid,comm | grep 1067727
532818 grep 1067727

Or use our home cooked cluster-wide ps command called "clu_ps" (discussed later in this chapter).

# clu_ps "-efp 1067727"
================================================================================
member2 (sheridan)          ps -efp 1067727
--------------------------------------------------------------------------------
UID     PID   PPID  C STIME   TTY            TIME CMD
root    1067727 1067722 0.0 03:31:28 pts/1   0:00.01 cat
================================================================================

The process is not on molari, but then again we already knew that. However, this will not prevent us from killing the process running on sheridan from molari.

[molari]
# kill 1067727

It is gone!

[sheridan]
# ps -Ao pid,comm | grep 1067727

532818 grep 1067727

[sheridan]
# jobs -l

[1] + 1067727  Terminated      cat &

Tru64 UNIX has altered the format of the PIDs beginning in V5.0 such that they include a cluster member identifier in bits 19-26 (See Chapter 6, section 6.5). This allows commands (such as the kill command) that reference a PID to indirectly use ICS to figure out on which member the target process lives.

Note that using the kill command on PID 1 sends a signal to the init process on the issuing member only.

Also note that a standalone system (not in a cluster) will be assigned member identifier zero. Recall that you can discern your system's cluster memberid through the following sysconfig command:

# sysconfig -q generic memberid
generic:
memberid = 1

In a cluster, the lowest member identifier will be one. The ps command is an example of a command that will only display information that is specific to the member on which it is running. While we all wait expectantly for a cluster-wide version of ps, below is some output from a home cooked script that does the cluster-wide ps job. So in the meantime, this script is available from the Digital Press web site and from the BRUDEN web site (See Appendix B for the URLs). To get a "ps" from member2 using our clu_ps script:

## 19.3 Common Files

Cluster-wide files are a distinguishing feature of the TruCluster Server product. Having common administration files is one of those good news, bad news situations, however. Sit back and consider whether you would like to have a cluster common /etc/rc.config file for example. You can quickly see that there are configuration items (such as HOSTNAME) that should not be shared among members. Yet the sharing of files such as /etc/passwd provides the good news of having the cluster appear to the users as a single system.

### 19.3.1 The passwd and group Files

Adding a new user account is an example of a typical system administration activity that is made easier (or at least no harder) by the existence of cluster common files. The /etc/passwd file and the /etc/group file are both shared by all cluster members. Therefore any information added to these files through “sysman accounts”, adduser, or dxaccounts(8) is immediately accessible to all cluster members. So rather than having to repeat the operation on each cluster member, do it once and you’re done. Any activities served by a database file in a common directory will function similarly.

### 19.3.2 Mounting File Systems

If you create and mount a file system, all cluster members immediately see it. Once again, if you think of the cluster as a single system, it makes sense that all members should see essentially the same files except for some configuration and support files. Needless to say, the /etc/fstab file is shared by all cluster members.

### 19.3.3 Swap Space

What about swap space? That’s not allocated from a file system so it can’t be handled by CFS activities. Swap space is allocated from one or more raw partitions. Since we are being coached to think of the cluster as a single system, does that mean that all systems are served by a single swap space? The answer is that the swap partition is indicated by the swapdevice entry in the vm subsystem portion of sysconfigtab(4). The /etc/sysconfigtab file is a CDSL and thus is member-specific. So each member will have its own swap space. Note that if you are in the habit of reflecting your swap space in /etc/fstab, change your habit. It is no longer meaningful in that file. Also be aware that if you use the swapon(8) command to add more swap space on the fly, the addition will be member-specific.

If you are concerned with performance, HP recommends that the swap partition be on a disk local to the member that uses it. This offloads some of the traffic on the shared bus where your swap partition would normally be. We suggest that you think this over carefully. Everybody wants to squeeze the last possible drop of performance from his or her system. But in this case the performance gain comes at the cost of your reliability. If your non-shared bus adapter fails, your

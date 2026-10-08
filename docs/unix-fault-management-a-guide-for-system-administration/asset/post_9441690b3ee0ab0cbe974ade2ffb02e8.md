
length of time the application has been running, and number of current users. Some resource and performance information is also available.

## DMI

System resource information can also be retrieved by using DMI, which is another standard for storing and accessing management information. Management information is represented in a text file in the MIF. It is divided into components, each of which has a Service Provider (SP) that is responsible for providing DMI information to the management applications that request it.

Several system platforms, including HP-UX, provide instrumentation for the System MIF and Software MIF. Appendix A contains a complete listing of these MIFs.

Similar to MIB-II, the System MIF can be used to get generic system information (such as how long it has been running) and system contact information. It includes the system name, boot time, contact information, uptime, number of users, and some information about the filesystem and disks.

The Software MIF provides information about the software products and product bundles installed on a system, and can be a useful tool after the discovery of a problem with an application. By using a MIF Browser, you can examine the Software MIF to see whether a problem might have been caused by a bad patch or modified file. The MIF contains revision information, including creation and modification times, for each product. Version information can be checked to see whether a compatibility problem exists. Finally, the product’s vendor information is provided, in case you need to contact the product’s support personnel.

Vendors such as Hewlett-Packard are working to provide enterprise-wide repositories of software configuration information. Tools are needed to compare application versions on different systems and update systems to the same revision level.

## pstat

Occasionally, you may want to write your own application program to get access to information about specific processes. This interface is referred to as *pstat*. Your program can generate output for only the interesting processes, which can be much easier than wading through *top* or *ps* output looking for important information.

Listings *7-2* and *7-3*, respectively, show a program that obtains *pstat* statistics and the output from running the program. The program displays information for the process(es) matching the names that you enter. The *pstat* interface can also show overall system information, as demonstrated in Listing *7-2*.

For the example in Listing *7-3*, the concern is that an application named *memhog* is using too much memory, so the program is being used to check *memhog*’s memory usage at various times, and to track the overall system load. This can be more convenient than running other tools, such as *top* or *GlancePlus*, and sifting through the output.

### Listing 7-2 Program code using pstat.

```c
/* pstat example */
#include <stdio.h>
#include <stdlib.h>
#include <sys/time.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <sys/errno.h>
#include <sys/pstat.h>

convert_status (status,stat)
char *status;
long stat;
{
    switch (stat) {
        case 1: strcpy (status,"sleeping");
                break;
        case 2: strcpy (status,"running");
                break;
        case 3: strcpy (status,"stopped");
                break;
        case 4: strcpy (status,"dead (zombie)");
                break;
        case 5: strcpy (status,"other");
                break;
        case 6: strcpy (status,"idle");
                break;
    }
}

main()
{
    struct pst_status pst;
    struct pst_dynamic dyn;
    struct pst_static mystatic;
    struct timeval temp;
    struct timezone dummy;
    char target[80];
    char status[14];
    int index = 0;
    int duration;
    long prm_id;
    unsigned long now;
    gettimeofday(&temp,&dummy);
    printf ("Enter process name:");
    scanf ("%s",target);
    now = temp.tv_sec;
    while ( pstat_getproc(pst,sizeof (struct pst_status),
	1,index) > 0) {
	if (strcmp(target,pst.pst_ucomm)==0) {
	duration = now - pst.pst_start;
	convert_status(status,pst.pst_stat);
	printf ("PID %8d Status: %s\n",pst.pst_pid,status);
	printf ("Started %d seconds ago\n",duration);

	printf ("Real pages(DATA %d TEXT %d STACK %d)\n",
		pst.pst_dsize,pst.pst_tsize,pst.pst_ssize);
	printf ("RSS %d MAX RSS(hwm) %d\n",
		pst.pst_rssize,pst.pst_maxrss);
	printf ("Number of swaps: %d\n",pst.pst_nswap);
	}
	index = pst.pst_idx+1;
} /* end while loop */

printf ("Overall System Info:\n");
pstat_getstatic(mystatic,sizeof(struct pst_static),
	0,0);
pstat_getdynamic(dyn,sizeof(struct pst_dynamic),
	0,index);
printf ("Run queue len(1- %1f,",
	dyn.psd_avg_1_min);
printf ("5- %1f,",
	dyn.psd_avg_5_min);
printf ("15- %1f)\n",
	dyn.psd_avg_15_min);
printf ("Physical Memory: %d\n",mystatic.physical_memory);
printf ("Active Real Memory: %d Free pages: %d bytes\n",
	dyn.psd_arm,dyn.psd_free*mystatic.page_size);
}
```

### Listing 7-3 Program output showing pstat information.

```
# ./pstate
Enter process name:memhog
PID	24549 Status: running
Started 247 seconds ago
Real pages(DATA 1955 TEXT 3 STACK 3)
RSS 1979 MAX RSS(hwm) 1979
Number of swaps: 0
Overall System Info:
Run queue len(1- 0.000000,5- 0.000000,15- 0.000000)
Physical Memory: 393216
Active Real Memory: 0 Free pages: 0 bytes
#
```

The example in Listing 7-3 shows only memory information, but a variety of additional metrics are also available. Here is a summary of the information available for each process:

- User ID, PID, effective user ID, real and effective group ID, and parent PID
- Number of real pages used for data, text, or stack
- Number of real pages used for shared memory, memory mapped files, and so forth
- Number of virtual pages used for data, text, stack, shared memory, and so forth
- Priority and nice value
- Terminal device ID
- Process group and PRM group ID
- Address of process in memory
- User and system time spent executing
- Time process started
- Process status and status flags
- Processor last used by process
- Command line and executable base name for process
- CPU time used
- Current and high-water mark of resident set size
- Number of swaps, page faults, and page reclaims
- Number of signals or socket messages received
- Number of socket messages sent
- Scheduling policy of process
- Session ID
- File ID of process' root directory, current directory, and executable
- Highest file descriptor currently opened
- Number of characters read and written

More information about the process and system metrics available from this interface can be found in the system include file, /usr/include/sys/psstat.h.

## Fault Detection Tools

This section describes products that can be used to detect application failures. Additional tools for monitoring application performance are discussed later in the chapter.

## IT/Operations

IT/Operations (IT/O) is a sophisticated management product for system operators. Systems in the enterprise can be displayed on maps onscreen, with colors representing their current status. An Application Bank is included for default and customized tools that can be launched from a particular system. Events can be sent from systems throughout the enterprise, and configured recovery actions can then be taken.

IT/O can also be used to monitor specified components on a managed system. Some predefined monitors are provided, one of which has the ability to monitor specific processes. An event is sent to the IT/O console if a process fails. A recovery action can be configured to restart the application.

Although IT/O can detect an application failure and restart the application, it does not have sufficient high availability capabilities to move an application to another system or ensure that only one copy is running. More extensive high availability capabilities are provided by MC/ServiceGuard, which is discussed next.

## MC/ServiceGuard

MC/ServiceGuard is a high availability product from Hewlett-Packard that is used to protect your critical applications and servers. MC/ServiceGuard is most commonly used in a multisystem (cluster) environment. The MC/ServiceGuard software on each system monitors the other systems in the cluster. MC/ServiceGuard can detect the failure of systems, networks, and applications. For example, MC/ServiceGuard can recover transparently from a LAN failure.

After deciding which applications need to be protected, you configure them as packages by using MC/ServiceGuard commands or the graphical interface accessible from SAM. Numerous attributes of the application need to be defined, such as the following:

- Name of application
- Scripts used to start and stop application
- Processes or services that make up application
- Subnetworks used by application
- Alternate systems on which application can run
- Additional resource dependencies

MC/ServiceGuard then monitors these services and dependencies. If a failure occurs, the package is either restarted locally or moved and restarted on another system. Similarly, when a system failure occurs, MC/ServiceGuard software can detect the problem and automatically restart critical applications on an alternate node.

MC/ServiceGuard software detects a variety of error conditions, but does not have a sophisticated notification mechanism for you to learn what happened. Errors are often written to the system log file, which helps retrace what happened.

Because MC/ServiceGuard can automatically move applications to other systems, it may be difficult for you to know the current status of your application. MC/ServiceGuard commands, such as cmviewcl, can tell you the current state of a cluster and its packages. The HP MC/ServiceGuard MIB also contains this information. However, a package can be moved for a variety of reasons, and MC/ServiceGuard doesn't tell you the reason. You may want to check the system log file (/var/adm/syslog/syslog.log) on each cluster system for its specific MC/ServiceGuard activity. An example of the events logged to the system log file during a package failover

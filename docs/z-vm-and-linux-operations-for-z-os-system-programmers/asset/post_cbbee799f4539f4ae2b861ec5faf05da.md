
## Checking system level: `query cplevel` and `query cmslevel`

The QUERY CPLEVEL and QUERY CMSLEVEL commands are useful for ensuring maintenance has been correctly applied on each system. The commands can be used to check the following items:

- Software version level, release level, and release modification level
- Software service level number
- Date and time (translated to the current active time zone) that CP system software was written to DASD
- Date and time CP was last started
- Release and service level of CMS

An example of the commands is shown in Example 5-2.

*Example 5-2 Checking CP and CMS levels*

```
q cplevel
z/VM Version 5 Release 3.0, service level 0701 (64-bit)
Generated at 05/29/07 23:21:12 EDT
IPL at 06/11/08 07:58:34 EDT
Ready; T=01/0.01 11:45:20
q cmslevel
CMS Level 23, Service Level 701
Ready; T=01/0.01 11:45:24
```

## Checking CP load parameters: `query cpload`

Use QUERY CPLOAD, shown in Example 5-3, to display information regarding the last CP IPL. The information displayed includes the location of the CP module that was last used, the location of the parm disk, and how CP was started.

*Example 5-3 Querying CPLOAD*

```
q cpload
Module CPLOAD was loaded from minidisk on volume LX6RES at cylinder 39.
Parm disk number 1 is on volume LX6RES, cylinders 39 through 158.
Last start was a system IPL.
Ready; T=01/0.01 11:46:07
```

## Checking the amount of real storage: `query storage`

The QUERY STORAGE command (abbreviated as Q STO) is used to display the amount of real memory that is available to an LPAR after it is started. See Example 5-4 on page 239.

## Checking the amount of expanded storage: query xstorage

The QUERY XSTORAGE command (abbreviated as Q XSTO) is used to display the amount of real expanded storage configured in a partition. The output of the command also shows the amount of expanded storage in use, and the amount used for minidisk caching (MDC). See Example 5-5.

```
q xstor
XSTORE= 2048M online= 2048M
XSTORE= 2048M userid= SYSTEM usage= 0% retained= 0M pending= 0M
XSTORE MDC min=0M, max=0M, usage=0%
XSTORE= 2048M userid= (none) max. attach= 2048M
Ready; T=0.01/0.01 11:47:27
```

## Checking all processors are available: query processors

The QUERY PROCESSORS command (abbreviated as Q PROC), is used to display the current assignment of processors of the partition.

The MASTER processor is the base processor, used for IPL, ALTERNATE processors are automatically brought online at IPL, and STANDBY processors are available to the partition, but offline. See Example 5-6. The last field in the PROCESSOR lines indicate the type of processor: CP, an IFL, ICF, ZIIP or ZAAP.

```
q processors
PROCESSOR 00 MASTER CP
PROCESSOR 01 ALTERNATE CP
PROCESSOR 02 ALTERNATE CP
PROCESSOR 03 ALTERNATE CP
PROCESSOR 04 STANDBY CP
PROCESSOR 05 STANDBY CP
Ready; T=0.01/0.01 11:51:31
```

## Changing the availability of processors to the system

Under normal circumstances, you bring up and run the system with all the processors in the processor complex or partition. However, if support personnel at your installation instruct you to do so, you may use the VARY ONLINE PROCESSOR or VARY OFFLINE PROCESSOR commands to control whether a processor is available to z/VM. For more information about these commands, see the z/VM: CP Commands and Utilities Reference, SC24-6081⁵

## Checking the system DASD configuration: query alloc

After the system has IPLed, a good practice is to check that the required paging and spooling are available and online. You can also check temporary disk space.

The QUERY ALLOC PAGE retrieves paging space configuration. In Example 5-7, four 3390-03 (each are 3339 cylinders) have been configured as paging devices. Only 13 pages in total are allocated on these paging devices.

Example 5-7 Checking the paging space available in the LPAR

```
q alloc page
VOLID RDEV EXTENT EXTENT TOTAL PAGES HIGH %
START END PAGES IN USE PAGE USED
---------- ---------- ---------- ---------- ---------- ---------- ----------
LX6PAG 1A22 1 3338 600840 0 0 0%
DK8226 8226 0 3338 601020 0 0 0%
DK8227 8227 0 3338 601020 13 26 1%
DK8228 8228 0 3338 601020 0 0 0%
---------- ---------- ---------- ---------- ---------- ---------- ----------
SUMMARY 2348K 13 1%
USABLE 2348K 13 1%
Ready; T=0.01/0.01 11:54:40
```

Similarly, the QUERY ALLOC SPOOL command checks the spooling configuration. In Example 5-8, only one 3390-03 DASD is defined as a spooling device, and 140075 pages are in use, representing around 23% of the total pages available for spooling.

Example 5-8 Checking the spool space

```
q alloc spool
VOLID RDEV EXTENT EXTENT TOTAL PAGES HIGH %
START END PAGES IN USE PAGE USED
---------- ---------- ---------- ---------- ---------- ---------- ----------
LX6SPL 1A21 1 3338 600840 140075 145430 23%
---------- ---------- ---------- ---------- ---------- ---------- ----------
SUMMARY 600840 140075 23%
USABLE 600840 140075 23%
Ready; T=0.01/0.01 11:55:39
```

⁵ http://publibz.boulder.ibm.com/epubs/pdf/hcse4b21.pdf


+   4. All running processes are terminated.
+   5. z/VM disables of the I/O devices.
+   6. The running system is terminated.

Example 5-20 shows the output of a z/VM shutdown process.

## Example 5-20 z/VM shutdown process.

```
00: 14:54:42 HCPWRP963I SHUTDOWN STEP USDAC - JOURNAL USER TERMINATION
00: 14:54:43 HCPWRP963I SHUTDOWN STEP MFRSD - TERMINATE HARDWARE LOADER
00: 14:54:43 HCPWRP963I SHUTDOWN STEP APISD - TERMINATE OTHER PROCESSORS
00: 14:54:44 HCPWRP963I SHUTDOWN STEP ENASD - DISABLE TERMINAL DEVICES
00: 14:54:45 HCPWRP963I SHUTDOWN STEP ISHDN - SHUT DOWN I/O SUBSYSTEM
00: 14:54:45 HCPWRP963I SHUTDOWN STEP TTRAL - TERMINATE CONCURRENT COPY SESSIONS
00: 14:54:46 HCPWRP963I SHUTDOWN STEP SVACV - ACTIVATE TERMINATION SAVE AREAS
00: 14:54:46 HCPWRP963I SHUTDOWN STEP CHMOF - DISABLE CHANNEL MEASUREMENT
00: 14:54:47 HCPWRP963I SHUTDOWN STEP ISHDA - DISABLE ALL DEVICES
00: 14:54:47 HCPWRP963I SHUTDOWN STEP CKPSH - TAKE A CHECKPOINT
00: 14:54:48 HCPWRP963I SHUTDOWN STEP OPRCD - SAVE OPERATOR CONSOLE LIST
00: 14:54:48 HCPWRP963I SHUTDOWN STEP MCWMD - DETERMINE MACHINE CHECK STATUS
00: 14:54:49 HCPWRP963I SHUTDOWN STEP SOVRS - RESET IBM DASD CU CHARACTERISTICS
00: HCPWRP962I VM SHUTDOWN COMPLETED IN 10 SEC
00: 14:54:49 HCPWRP963I SHUTDOWN STEP SVADV - DEACTIVATE TERMINATION SAVE AREAS
00: 14:54:50 HCPWRP961W SYSTEM SHUTDOWN COMPLETE
00: HCPGIR450W CP entered; disabled wait PSW 00020000 00000000 00000000 00000FFF
```

## 5.2.5 z/VM services

z/VM provides several services in the form of virtual machines. A virtual machine is similar to a z/OS Started Task, TSO User, or batch job. Unlike some operating systems, CP does not have the concept of a process. Instead, all CP knows is how to run virtual machines. This means that any extra service function not built directly into CP must be implemented as a service virtual machine.

A service virtual machine is the same as any other virtual machine, except it runs certain software (typically on top of CMS) that provides a service to some or all of the other users on the system.

The following examples are services provided by service virtual machines:

- TCP/IP networking stack
- User directory maintenance (Dirmaint)
- Security manager (RACF)
- Performance data collection and reporting (Performance Toolkit)
- Systems management service (SMAPI)

Service virtual machines in z/VM usually have a user name that corresponds with the service it provides. Table 5-1 lists several common service virtual machines and brief descriptions of the service provided.

Table 5-1 Common service virtual machines

| Guest name | Service provided |
|---|---|
| TCPIP | TCP/IP networking stack and tools like FTP and Telnet |
| DIRMAINT | User directory maintenance |
| DATAMOVE | Disk copying and formatting services for DIRMAINT |
| PERSFVM | Performance recording and reporting |
| RACFVM | Security management for guests, devices and services |
| VMSERVE | Systems management service |
| RSCS | Remote spool device capability |
| PVM | Remote communication and system access |
| EREP | Error recording |
| DISKACNT | User accounting recording |
| OPERSYMP | Symptom recording |
| VMSERVR<br>VMSERVS<br>VMSERVU | Support for Shared File System (SFS) |

## 5.3 Managing a guest operating system virtual machine

Guest support in z/VM allows you to run multiple images of production operating systems. You can use guest support in z/VM to develop, test, manage and migrate operating systems that run on System z alongside your production systems. The following sections discuss guest systems supported and how to operate the virtual machines.

### 5.3.1 Guest support

All of the supported mainframe operating systems can run under z/VM, including z/VM itself. For a list of supported mainframe operating systems, the type of support z/VM offers, and other useful information, refer to notes in z/VM: General Information, GC24-6095. If running on an IFL, then only z/VM and Linux are allowed.

> Tip: z/VM General Information, GC24-6095, also has a list all of supported hardware that can be used with any release of z/VM.

The concept of having each user be a virtual machine is new to z/OS users. Therefore, the next sections explain how to manage them (start, pause, resume, and halt).

### 5.3.2 Starting a guest operating system

Each guest operating system is run from individual z/VM virtual machine user IDs. Logging on to these user IDs is done in the same manner as any other z/VM user ID, and usually comes up running in a CMS environment. From the log on session, a guest operating system can be loaded on that virtual machine's storage and run much the same as though it were running in an LPAR.

In z/VM, starting an operating system this way is still like using IPL (initial program load). When you IPL an operating system, it takes control of the virtual machine's storage; any other operating system that was running before is cleared from memory and no longer controls the virtual machine. Keep in mind that CP will still be running, because CP is not a guest operating system.

In CP, you perform an IPL by using the IPL command. CP can IPL directly from a device, in which case the operating system is read from the data residing on the device. Or CP can IPL from data stored in shared memory known as a Named Saved System (NSS). To IPL from a device, give the virtual device number of the device you want to IPL; see Example 5-21.

## Example 5-21 IPL of the 190 disk

```
IPL 190
z/VM V5.3.0    2007-05-02 16:25
Ready; T=0.01/0.01 09:37:40
```

In Example 5-21 we IPLed, the 190 disk, which by default contains the CMS operating system. At this point CMS is running and any command issued is processed by CMS first.

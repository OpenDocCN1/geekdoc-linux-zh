
- Does the file system break?

**Problem description: failing in mounting file system**

Questions to be answered:
- Is the /etc/fstab description correct?
- Are devices correctly recognized?
- Does not the file system break?

Possible solutions are:

- **Modify the fstab entries.**
    - If there is a mis-setting, modify it.
    - If a problem in a file system occurs, comment it out temporarily or set the fsck flag to off (set it to 0).
- **Re-make initrd.**
    - The devices may not be recognized by coldplug but may be recognized after a re-make of initrd.

*Example 10-8 Message example - failing in fsck*

```
Checking file systems ...
fsck 1.38 (30-Jun-2005)
Checking all file systems.
?/sbin/fsck.ext3 (1) -- /opt? fsck.ext3 -a /dev/dasdd2
fsck.ext3: No such device or address while trying to open /dev/dasdd2
Possibly non-existent or swap device?
fsck.ext3 /dev/dasdd2 failed (status 0x8). Run manually!
?IA..failedblogd: no message logging because /var file system is not
accessible
fsck failed for at least one filesystem (not /).
Please repair manually and reboot.
The root file system is is already mounted read-write.

Attention: Only CONTROL-D will reboot the system in this
maintenancemode. shutdown or reboot will not work.
Give root password for login: ____________________
```

## 10.5.4 Failure to start a service

The following two cases are thought to be causes of failure when starting a service.

**Problem description: problem with automatic start setting.**
Questions to be answered:
- Is the symbolic link file (whose name starts with Sxx) deployed in /etc/init.d/boot.d?
- Is the symbolic link linked with a correct start script?
- Is the symbolic link file (also known as symlink or soft lnk) deployed in /etc/init.d/rcx.d?
- Is the symbolic link linked with a correct start script?

**Problem description: The automatic setting is valid, but the service does not start.**
Questions to be answered:
- Has the required service started?
- Is there problem in the start script?

A possible solution is doing an automatic start setting of the service. It is set so that the service starts when booting by using the `chkconfig` command or the `insserv` command.

![Image](img/f332344337ca8bf6846cb313a66ee0b3_328_0.png)

# Case study: slow responding Web site

In this chapter, we show how to determine the problem behind a slow response time and low transaction rate scenario in a typical three-tier Web-based serving environment, which is also a general problem usually reported by production administrators. Although we are restricted in our lab environment from recreating the problem, effort has been taken to reflect the real-world Web application production environment. The scope of this case study is to provide information about using various Linux and z/VM-based tools and other problem determination experiences in a combined manner.

## 11.1 Three-tier Web application environment

In this scenario we implemented a high-availability solution for a Web-based application with Linux images running on System z.

WebSphere Application Server (WAS) is one of the most common middleware products run on Linux on System z. WebSphere is also one of the most widely used Java-based application servers in the world, and many organizations use Web applications hosted on WAS to connect to data housed on the same mainframe.

To make the environment simpler, we used the Trade 6 application to recreate a Web Serving environment. The application data resides on DB2 for Linux on System z.

> **Important:** We restrict this case study to only problem determination on the utilization of hardware resources. We also assume that the applications (IBM HTTP Server, WAS, and DB2) are optimally tuned to provide maximum performance.

### 11.1.1 Trade 6 Web serving application

The IBM Trade Performance Benchmark sample, also known as the Trade 6 application, is a sample WebSphere end-to-end benchmark and performance sample application. This Trade 6 benchmark has been designed and developed to cover WebSphere’s programming model.

This application provides a real-world workload, driving WebSphere’s implementation of J2EE™ 1.4 and Web services, including key WebSphere performance components and features. The Trade 6 application simulates a stock trading application that allows you to buy and sell stock, to check your portfolio, register as a new user, and so on.

In this book, we use Trade 6 to generate workloads that would impact the system performance. The IBM Trade Application for WebSphere Application Server is available to download for free at:

```
https://www4.software.ibm.com/webapp/iwm/web/preLogin.do?source=trade6
```

The three main Trade 6 components are listed below and shown in Figure 11-1:

- **IBM HTTP server**
    - The HTTP server accepts client requests and delivers static content (HTML pages, images, and style sheets). Dynamic requests are forwarded to the WebSphere Application Server through a server plug-in.
- **IBM WebSphere Application Server**
    - The WebSphere Application Server creates dynamic content using JavaServer™ Pages (JSPs) and Java Servlets. Pages are generated from data extracted from a DB2 database. All Trade versions are WebSphere-version dependent, so Trade 6 only works with WebSphere Application Server V6.
- **DB2 database**
    - The DB2 database contains relational tables regarding simulated customer accounts and stock transactions. We used DB2 LUW v8.2.

![Image](img/f332344337ca8bf6846cb313a66ee0b3_330_0.png)

### 11.1.2 Our Web serving setup

Several options are available when deploying Trade 6 on Linux on System z:

- All components can run in a single Linux guest. This is referred to as a single-tier deployment.
- Each component can run in a dedicated Linux guest. We refer to this as a three-tier deployment.

We chose a three-tier deployment for this book, where we run the IBM HTTP server, the WebSphere Application Server, and DB2 in their own Linux guests (see Table 11-1 on page 317). Our deployment choice is depicted in Figure 11-2. Using a three-tier deployment enabled us to adjust the virtual machine size of each Linux guest more accurately, based on the task that particular guest performs.

![Image](img/f332344337ca8bf6846cb313a66ee0b3_331_0.png)

Figure 11-2 Three-tier deployment

In addition, when measuring utilization, the three-tier deployment option allows us to attribute specific resource usage to a specific task. See Table 11-1.

**Table 11-1 *Linux servers and their configurations***

| Server | Application | Processor | Memory |
| :----- | :---------- | :-------- | :----- |
| LNXIHS | HTTP Server | 1 | 512 MB |
| LNXWAS | WebSphere Appl Server | 1 | 3 GB |
| LNXDB2 | DB2 Server | 1 | 2 GB |

### **11.1.3 WebSphere Studio Workload Simulator**

The WebSphere Studio Workload Simulator for z/OS and OS/390® is an application that allows you to create multiple virtual or simulated users in order to test load and performance. The Workload Simulator consists of two components: a controller and an engine. For high scalability, Workload Simulator’s Engine, which generates the load used during load-testing, is installed on a System z server. The load generated by the engine can be used to test any Web-serving environment (that is, the environment to be tested is not limited to z/OS). In our case, we tested against a WebSphere Application Server that was running on a Linux on System z guest. Workload Simulator supports multiple engines.

## **11.2 Symptoms of the problem**

When we started to put load on the Web-serving environment, at one point of time the workload simulator reported that the HTTP server was not able to accept the page read request, and timed out. See a sample of the report that is generated in Example 11-1.

**Example 11-1 *Report from workload simulator with timed-out messages***

```
04/01/2008    03:09:23

**************************************************************

04/01/2008    03:09:23    WebSphere Studio Workload Simulator
04/01/2008    03:09:23    Version 03353Z
04/01/2008    03:09:23    (c) Copyright IBM Corp. 2002,2003 All Rights Reserved.

**************************************************************

04/01/2008    03:09:23    IWL0075I Reading options from
04/01/2008    03:09:23    /etc/iwl/common/default.conf.
04/01/2008    03:09:23    IWL0039I Script compilation SUCCESSFUL (180 ms)
04/01/2008    03:09:23    IWL0021I Engine name = Jibe
04/01/2008    03:09:23    IWL0030I Initial number of clients = 150
```

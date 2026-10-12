
Interesting because it provides a way to determine exactly which processes use which network ports. Some of this information may be obtained from the * /etc/services* file, but not all network applications or services are listed in this file, nor does each entry disclose exactly which process may use a particular port. Figure 9.26 displays a sample mapping report.

![](img/f265c9d1f2610aca197c430cbfcd51f5_557_0.png)

Figure 9.26 Local usage report (part two).

## IP Protocol Category

Two different reports are included in this category. The first, called *Distribution*, shows up to three separate tables indicating the flow of traffic. The second report, *Usage*, shows network protocol usage from a high-level point of view.

## Distribution Report

One of the most useful of all the **ntop** reports is the IP protocol Distribution Report, which shows the breakdown of network usage by higher-level protocols. It is similar to the **Global Traffic Statistics** report shown in Figure 9.17, but contains a detailed breakdown by transport-layer protocol. It reveals the amount of data (sent/received) by protocol type, such as **snmp** or **ftp**, as shown in Figure 9.27.

![](img/f265c9d1f2610aca197c430cbfcd51f5_558_0.png)

Figure 9.27 Protocol distribution report.

This is an important observation because this report clearly shows which applications are used the most versus those used the least. The report contains three tables that include protocol distribution for Local Traffic, Remote to Local Traffic, and Local to Remote Traffic. Each section or table contains three columns: IP Protocol, Data, and Percentage. The IP Protocol column includes the higher-level protocols that ntop understands and supports. Those protocols that ntop doesn't support are listed under the Other TCP/UDP-based Prot. category. Each protocol has associated Data and Percentage columns that relate the amount of data, expressed in bytes and as a percent of total bytes, in comparison to each of the other protocols.

Using the bar graphs contained within this report, it is relatively straightforward to identify network utilization by protocol or network application. For example, observing the second table shows that, out of all the IP traffic displayed, UDP usage was by far the most significant as compared to TCP traffic.

This report shows high-level protocol or application services, and both the client and server that participated in the traffic exchange. Figure 9.28 displays a sample report that shows ftp, telnet, snmp, finger, and smtp. Also, it lists both the clients and server that were using these protocols and services.

![](img/f265c9d1f2610aca197c430cbfcd51f5_559_0.png)

Figure 9.28 Protocol subnet usage report.

### Using the Command Options

The `ntop` tool supports the command-line options listed in Table 9.10. This software considers a host that hasn't generated or received traffic since its last poll to be an inactive host. If you are interested in viewing inactive hosts as well as active ones, use the `-d` option. This will show both types when generating reports. Also, when `ntop` is running in terminal mode, the `-d` key can be used to accomplish the same purpose. This is useful to display all hosts regarding their activity status. Another handy option is `-i`, which controls the network interface that `ntop` uses to monitor the network. With multi-homed systems, this is an absolute requirement. If it is necessary to monitor the network by percentage, use the `-p` option. This option will display traffic as a percent of total traffic for each system active on the network.

| Option | Description |
|---|---|
| -d | Shows all hosts, not just active ones |
| -F | Defines a flow (filter) that is monitored and reported |
| -l | Shows both local and remote hosts that generate network traffic |
| -i | Specifies an alternate interface to use |
| -n | Shows numeric IP addresses instead of names |
| -r | Controls the delay between screen updates |
| -p | Shows network traffic as a percent |
| -w | Enables Web mode |

### Securing the Web Reports

If you are concerned about security with respect to the reports, no problem! The `ntop` tool supports a rudimentary but very useful security feature that can be implemented quickly and easily. When ntop is run, it searches for a file called .ntop in the home directory of the user starting the process. This file may contain one or more names and associated passwords. When an entry is added to this file, the user is prompted with a login window, as displayed in Figure 9.29.

![](img/f265c9d1f2610aca197c430cbfcd51f5_560_0.png)

In most instances, it is reasonable that ntop be run as the super-user of the system. As a result, an .ntop file can be placed in the directory of the /root file system. To make it as secure as possible, ensure that the file is not readable except by the superuser. The permission of 600 should be sufficient. Assume that we want to provide access to **ntop** for a handful of users. The following sample `.ntop` would serve our purpose:

```
netmgr private
tech-l secret
smartwell lghost99
acartwright 44pleaserad
```

With these entries, any of the four users—`netmgr`, `tech-l`, `smartwell`, or `acartwright`—can obtain access to the **ntop** reports, provided that they each use the associated password string. Thus, `netmgr` would have to use `private`, and so on. Clearly, this security feature is very simple, but it does have its weakness. Namely, someone could capture the login sequence with a probe or host-based software and obtain the name/password pair combination.

## Creating Monitoring Flows

The `-F` option creates new flows within **ntop**. However, the syntax is a little tricky. The general format using this option is as follows:

```text
ntop -F "flow_name=\'filter expression\'[;filter expression]"...
```

When more than one flow will be used, each flow must be followed by the previous one, separated by a single comma with no spaces in front of the comma. The entire string after the option must contain double quotes, whereas the filter expression is contained within single quotes. Assume that two new filters are needed, one to capture all traffic between host `chips` and `dips`, and the other to capture all **tcp** traffic from host `peanuts`. The first flow will be called `chipsdips_traffic`, and the other is `tcp-peanuts`. The following **ntop** command with the associated flows could be used:

```text
# ntop -F "chipsdips_traffic=\'host chips and dips\';tcp-peanuts=\'host\
peanuts and tcp\'" -w 3000
```

In this command, the first flow will capture all traffic either sent from or received by both `chips` and `dips`. The other flow will capture all traffic that contains **tcp** data and is sent or received by `peanuts`. Recall that **ntop** supports many of the `ethereal` and `tcpdump` filter expressions and keyword commands. Therefore, powerful filters can be used to assist with monitoring the network.

## Using Terminal Mode

For those who do not want to use the Web interface, the second display mode provides terminal output similar to the UNIX **top** command. Invoke the **ntop** command without the `-w` option. In this mode, network information is presented in a constantly updated window, as shown in Figure 9.30. This window contains a running status of network utilization sorted by network protocols. Several display options are available that can be used to toggle the information displayed and otherwise control **ntop**. In the window displayed, the network traffic values are represented as a percent. This was enabled by the **p** command. The window only shows a few of the monitored protocols; use the spacebar key to scroll through the entire list of protocols.

![](img/f265c9d1f2610aca197c430cbfcd51f5_562_0.png)

Figure 9.30 Terminal display mode.

By default, **ntop** starts in terminal mode. The information presented with the Web interface is available in the terminal mode, but, of course, the data is formatted differently. To review the different reports, **ntop** defines a number of keyboard commands that will alter the displayed report. The keyword command consists of pressing a single letter key without pressing the Enter key.

For example, the **h** command provides help for the **ntop** tool and displays a list of available keyboard commands. Thus, when **ntop** is running, pressing this key (without the Return or Enter) will display the help menu shown in Figure 9.31.

The user is prompted to press a key to return to the main report screen. Even when **ntop** is displaying the help screen, it is still monitoring and collecting network traffic statistics. As you can see in

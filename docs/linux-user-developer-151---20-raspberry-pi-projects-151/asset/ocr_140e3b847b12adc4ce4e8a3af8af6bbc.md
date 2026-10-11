# Tutorial Netstat troubleshooting

![](bbox=[0.2, 0.17, 0.45, 0.4])

This is a small part of the Netstat man page. Netstat has many options that you can learn just by using them

![](bbox=[0.48, 0.17, 0.72, 0.4])

This is a small part of the output from the netstat -s command, which displays summary statistics for each protocol

![](bbox=[0.2, 0.43, 0.45, 0.58])

If Netstat is not able to understand one of the command line options, it displays a brief help screen

![](bbox=[0.48, 0.43, 0.72, 0.58])

The output of the netstat -a command displays the listening and non- listening ports

# Troubleshoot your network with Netstat

Learn the various command line options of Netstat and troubleshoot multiple network related problems like a pro

Advisor  \nMihalis Tsoukalos is a UNIX administrator, a programmer (UNIX and OS), a DBA and a mathematician. He has been using Linux since 1993

# Resources \nLinux machine \nRoot privileges

Netstat is a command line utility that shows information about the network status of your machine. It’s a powerful tool that can work on the Socket, TCP, UDP, IP and Ethernet levels. Its main drawback is that it only works on the local machine – utilities such as nmap and tcpdump can also display information from remote machines. Nevertheless, we can show information quickly and comprehensively, and its command line options are case-sensitive.

Remember to check your log files for errors or warnings about your network problem and, if needed, raise the logging level to get more information. Once resolved, lower the logging level because log files can easily grow very big. Reading log files is most helpful for application level and hardware related problems. \n\nWhen Netstat isn’t sufficient for solving your network problem, use Wireshark, tshark, tcpdump, nmap or another tool of your choice.
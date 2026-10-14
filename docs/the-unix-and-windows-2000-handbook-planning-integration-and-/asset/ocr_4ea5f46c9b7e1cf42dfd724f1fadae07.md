The netstat -i command will show all configured interfaces and a total column for all interfaces. netstat -I le0 will produce output for network interface card le0.

Figure 14.4 is the output produced on a Solaris 2.6 workstation with the -i switch and an interval of five seconds. The output contains a column for each interface and a total column combining all interface statistics. The first row contains the values since the machine was booted. Each succeeding row contains the activity that has taken place during the interval indicated on the command line. The output is very easy to understand. The input column shows incoming packets and the output column shows outbound packets. You can determine the percentage of collisions by substituting the values into the simple equation colls * 100/ packets for the output column.

Collisions occur when workstations are trying to transmit packets at the same time. Sustained collision percentages above seven percent indicate an overloaded network. You can also determine the percentage of error packets by substituting values into errs * 100/ packets. Values greater than one percent indicate a network problem. Call a professional to investigate.

![](bbox=[0.07, 0.55, 0.89, 0.92])

Figure 14.4 netstat with two options on Solaris 2.6.
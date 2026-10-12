This information can be compared with the switch-side settings to ensure that both are configured and operating in the same mode. As shown in Figure 4-58, the OSA/SF tools show the configured values for the OSA card and the active values.

![](bbox=[0.26, 0.22, 0.88, 0.48])

Figure 4-58 Sample OSA/SF output showing the OSA card port speed settings

# 4.4 Case studies

In this section we see some case studies involving real-life problems.

# Case study 1 - eth0 interface eth0 interface down

In this scenario the deactivation of the eth0 interface causes the eth1 interface to stop functioning.

# Problem

We have a Linux system running on the system with one interface eth0. A new Ethernet interface eth1 was added and the system was rebooted. After the system reboot, the eth0 interface was brought down using the ifconfig command to test the communication using the eth1 interface. But now the eth1 interface cannot communicate. Figure 4-59 shows the scenario.

![](bbox=[0.26, 0.84, 0.88, 0.93])

Figure 4-59 Case study example - eth0 interface down
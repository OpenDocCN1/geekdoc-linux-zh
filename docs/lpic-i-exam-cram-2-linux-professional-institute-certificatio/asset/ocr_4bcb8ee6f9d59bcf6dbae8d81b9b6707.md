# # Exam Prep Questions

1. You are configuring a dial-up connection for a Linux desktop user. What is the actual device filename for the modem that is using I/O address 02e0h? (Choose two.)

+   □ A. `/dev/tty1`
+   □ B. `/dev/ttyS3`
+   □ C. `/dev/modem`
+   □ D. `/dev/cua3`

Answers B and D are correct because the device is using IRQ 3 and I/O address 03e0h; therefore, `setserial /dev/ttyS3` and `setserial /dev/cua3` confirm this. Answer A is incorrect because there must be a capital S in the device filename and it points to the wrong port. Answer C is incorrect because `/dev/modem` is most often a link to an actual device filename, such as `/dev/ttyS1`.

2. A user complains that after using the `setserial` command to configure his modem, it can no longer communicate at a rate faster than 9600 kbps. What are the most likely settings that would cause this problem? (Choose two.)

+   □ A. UART
+   □ B. `1ine`
+   □ C. `spd_normal`
+   □ D. `Baud_base`
+   □ E. IRQ

Answers A and D are correct because `Baud_base` is the setting that reflects the speed of the connection and the UART setting is the type of controller, which, if set to 8250 or lower than 16550, keeps the speed at 9600 kbps or less. Answer B is incorrect because the `1ine` setting has no bearing on the speed of the connection. Answer C is incorrect because `spd_normal` is used to set a requested speed as the actual speed. Answer E is incorrect because an incorrectly set IRQ would keep the connection from occurring altogether.

3. You are configuring a NIC to communicate with the network. Your network administrator assigned you an IP of 192.168.33.104; the netmask is the default for that class, and your interface is the first Ethernet device on the machine. Which of the following sets up this device so a ping to another device will work?

+   O A. `netconfig -ip=192.168.33.104 -mask=C`
+   O B. `ifconfig eth0 192.168.33.104 netmask 255.255.255.0 up`
+   O C. `netstat -a 192.168.33.104/255.255.255.0 on`
+   O D. `route add IP 192.168.33.104 255.255.255.0`
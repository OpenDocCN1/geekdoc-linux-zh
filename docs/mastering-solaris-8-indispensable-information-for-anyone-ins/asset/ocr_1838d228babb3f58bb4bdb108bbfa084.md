# Serial Ports

Solaris supports RS-232-C and RS-423 serial ports as well as parallel (or printer) ports. Serial ports are used to connect modem and terminals to a system. Using a terminal allows you to avoid the cost of a computer monitor and graphics card and still be able to control the boot-up of a system.

You can use the `admin tool` program to graphically manage serial port and parallel port devices such as modems and printers, respectively. Solaris uses the ttymon port monitor to communicate between devices and the operating system. Serial devices issue getty requests, often concurrently, which are passed through the port monitor. These commands may be found on the Sun site (www. sun. com) by searching for “managing terminals and modems”.

Follow these steps to configure a port for a terminal:

+   1. Open `admin tool`, found in the `system_admin` folder, by clicking the Applications drawer of the front panel and then clicking the Applications control. 
+   2. Enter one of the user modes. 
+   3. Enter the default terminal type, the transfer rate in baud, and any flow control or carrier detection.
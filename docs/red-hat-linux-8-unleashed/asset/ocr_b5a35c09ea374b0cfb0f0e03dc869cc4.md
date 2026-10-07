# CHAPTER 4 Post-Installation Configuration

![](bbox=[0.358, 0.101, 0.658, 0.212])

FIGURE 4.6 The redhat-config-soundcard client is used during an X session to configure a soundcard for Red Hat Linux.

# Detecting and Configuring a Modem

More than seven million users in the United States now connect to the Internet with cable DSL service, but for many users a modem is the standard way to connect with an Internet service provider (ISP) using the Point-to-Point Protocol (PPP). Other common tasks for modems include adding or changing your modem after the initial Red Hat Linux installation, you you will need to configure the modem to perform all these tasks.

Red Hat Linux includes several tools you can use to configure and use an internal or external modem in your notebook or PC. Chapter 15, "Internet Connectivity," contains the details about configuring Red Hat Linux to connect to the Internet using a modem. This section covers how to configure Red Hat Linux to recognize and configure modems using serial ports (a standard formerly known as RS232, but now termed EIA32) or USB.

# Configuring a Serial-Port Modem

Linux uses /dev/ttySX, /dev/ttyUSB, or /dev/ttyUSB for serial ports, where X can range from 0 to 15. Many additional ports can be added to a system using multiport or chained USB devices. A PC's internal serial ports are generally recognized at boot time. To see a list of recognized ports for your system, pipe the dmesg output through grep command like:

```
# dmesg | grep tty
ttyS0 at 0x3f8 (irq = 4) is a 16550A
ttyS1 at 0x2f8 (irq = 3) is a 16550A
```

In this example, Linux reports that two serial ports have been recognized. Note that the device matching ttyS0 is /dev/ttyS0, despite the kernel output. The PC's external modem can be attached (most likely using a male DB9 adapter) to it here. Under Red Hat Linux, nearly all modem-based software can use a symbolic link named /dev/modem that points to the desired device. This link is not created by default, but as root, you can create this device manually using the 1n command like:

```
# ln -s /dev/ttyS0 /dev/modem
```

In this example, /dev/modem will point to the first serial port.
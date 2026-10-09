
# The apcupsd Package

The apcupsd package is a package that provides UPS power management functions. During a power outage, it allows the computer to run for a specific period with the support of a UPS. However, the user should save all changes made to the files and shutdown the system before the specified period expires. If the time does expire, then the package automatically performs a controlled shutdown of the system automatically.

# The apcupsd.conf File

The apcupsd.conf file is a configuration file that is required by the apcupsd package to communicate with the UPS. It contains directives that include configuration details about the UPS, which are added to a system. All the directives listed in the following table should be specified in the configuration file.

| Directive | Description |
| :--- | :--- |
| UPSTYPE <i><type of UPS></i> | Specifies the name of the driver. The values could be dumb, apcsmart, net, usb, snmp, or test. |
| UPSCABLE <i><type of UPS cable></i> | Specifies the type of the cable used by the system. |
| DEVICE <i><name of the device></i> | Specifies the device that is used for UPS communication. Usually a serial port or a USB device is used for communication. |
| LOCKFILE <i><path of the lock file></i> | Specifies the path of the directory where the lock file for the USB or serial port needs to be created. |

# System Power States

A Linux system may support several states of power. Some of the power states are listed in the following table.

| Power State | Description |
| :--- | :--- |
| Working | The system is fully usable. |
| Sleeping | The system appears to be off. Power consumption is reduced depending on how the system power is allocated. |
| Soft Off | The system appears to be off and has very low power consumption. |
| Mechanical Off | The system is switched off and there is no power consumption. The system needs a full reboot to be fully usable. |

# How to Configure Power Management

**Procedure Reference: Configure CPU Power Management**

To configure CPU power management:

1. Switch to the `/proc/acpi/processor/CPU{CPU Number}` directory.
2. Verify that power management and throttling are turned on by using the `cat info` command.
3. Display the current power settings by using the `cat power` command.
4. Verify that the appropriate states for your machine are available.
    - If you have a desktop computer, verify that the first two C1 and C2 states are available.
    - If you have a laptop, verify that all three states are available.
5. Display the current throttle settings by using the `cat throttling` command.
6. Enter the `echo -n [throttle_state] > throttling` command to adjust the throttle.

> Inform the students that you can configure power only on systems with multiple processors. Some of the options such as, throttling and power, cannot be adjusted in systems that have only a single processor.

# Throttling Technique

It is a technique by which a system is made to run at a capacity less than the maximum capacity it is capable of, with the intent of saving power.

# ACTIVITY 15-2

## Configuring CPU Power Management

Before You Begin:

1. On srvA, you have logged in as root in the CLI.
2. The first terminal is displayed.

Scenario:

Your manager would like you to check whether the new Linux systems support power management and configure power management on the systems to conserve power.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Verify that power management and throttling are turned on for your CPU. | a. On the terminal, enter `cd /proc/acpi/processor/cpu0` to change to the CPU0 directory. |
| | b. Enter `cat info` to view the current settings of the CPU. |
| | c. Verify that power management and throttling are listed. |
| 2. Display the current power and throttling settings. | a. Enter `cat power` to view the current power setting. |
| | b. Verify that C1 is available. |
| | c. Enter `cat throttling` to view the current throttling setting. |
| | d. Verify that eight states (T0 to T7) are listed and that the asterisk (`*`) is next to T0, the active state. |
| 3. Adjust the throttling state. | a. Enter `echo -n 7 > throttling` to set T7 as the active state. |
| | b. Enter `cat throttling` to view the new throttling setting. |
| | c. Verify that the asterisk (`*`) is next to the T7 state. |
| | d. Enter `echo -n 0 > throttling` to set T0 as the active state. |
| | e. Enter `cat throttling` to view the new throttling setting. |
| | f. Verify that the asterisk (`*`) is next to the T0 state. |
| | g. Enter `clear` to clear the terminal screen. |

# TOPIC C

# Configure Removable Hardware

You addressed the necessary power management options. As a Linux+ administrator, you may need to add additional hardware devices to your system, based on user requirements. In this topic, you will configure removable hardware.

Advancement in technology may require you to constantly upgrade the hardware configuration of your Linux system. Removable devices are a convenient and efficient way to upgrade your Linux machine.

# Removable Hardware

Linux systems allow you to utilize removable devices. Some of these devices are described in the following table.

| Device | Example |
| :--- | :--- |
| Input | Keyboard, pointing device, joystick, scanner, webcam, digital tablet, and digital camera |
| Network | Modem and NIC |
| Output | Printer, sound card, and speakers |
| Storage | CD, DVD, tape drive, floppy disk, zip drive, flash drive, and hard drive |

# The PC Card

The PC card, formerly known as the PCMCIA, is of the size of a credit card and can be used for storage space, network cards, modems, and other purposes. Its standards and specifications are defined by the Personal Computer Memory Card International Association (PCMCIA).

# The PCMCIA Organization

The PCMCIA organization is an alliance of members who promote interchangeability and compatibility among portable computers. The alliance defines the standards for the PC card.

# Card and Socket Services

Card and socket services are loaded into memory when a portable computer is booted. This software comes with the PC and with the cards. These two layers of software detect and support a PC card when it is inserted into the portable computer. They also manage hot-swapping and pass changes in events to higher-level drivers written for specific cards.

Socket services interact with the BIOS to identify the number of sockets available. It can be built into the BIOS or added through software. When the system is turned on, it detects when a PC card is inserted or removed. Socket services work with card services above it, and communicate directly with the PC card's controller chips.

Card services automatically assign system resources when socket services identify that a PC card has been inserted. Card services manage system resources required by PC cards such as IRQs, memory, and I/O addresses. This software management interface also works in conjunction with upper-level software, such as hardware drivers, that may need to be loaded to work with the PC card.

# The cardmgr Utility

The cardmgr utility monitors PCMCIA sockets for card insertion and removal events. When a card is inserted, the utility looks up the card in a database of known cards. If the card is identified, appropriate device drivers are loaded and bound to the card. When the card is ejected, the card's drivers will be unloaded if possible.

The /var/run/stab file contains identification and device driver information for PCMCIA cards. It is created by the cardmgr utility. Device driver lines comprise a series of tab-separated fields. These fields are described in the following table.

| Field | Description |
| :--- | :--- |
| 1 | Socket number |
| 2 | Device class (identifies which script in /etc/pcmcia is used to configure or shutdown the device) |
| 3 | Driver name |
| 4 | Used to number devices when a single card has several devices associated with the same driver |
| 5 | Device name |
| 6 | Major device number, if required |
| 7 | Minor device number, if required |

## Arbitrary commands

Based on the contents of the PCMCIA card configuration database, the cardmgr utility may also execute arbitrary commands when appropriate cards are either inserted or removed. All insertion and removal events, device driver loads and unloads, startup and shutdown commands, and warnings and errors are reported in the system log file. Current card and device information for each socket is recorded in the /var/state/pcmcia/stab or /var/lib/pcmcia/stab file.

Normally, when a card is identified, the cardmgr utility will send a beep to the console. A beep is also generated when a card is successfully configured. A beep of lower pitch is generated if either of these steps fails. Ejecting a card produces a single beep. When the cardmgr utility receives a SIGHUP signal, it will reload its configuration file. When the cardmgr utility receives a SIGTERM signal, it will shutdown all sockets that are not busy and then exit, but drivers for busy sockets will stay loaded. If the PCMCIA_OPTS environment variable is set, its contents will be parsed after the main card configuration file is read.

## The pcmcia File

The pcmcia file stored in the /etc/pcmcia/config directory is a card configuration database. It is read at startup by the cardmgr utility. It defines the resources that are available for use by the card services, explains how to load and initialize device drivers, and describes specific PCMCIA cards.

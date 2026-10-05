
## Alternative connectors

-   Signals are named relative to the perspective of the DTE Device. For example, the name TD (transmitted data) really means “data transmitted from DTE to DCE”. Despite the name, the TD pin is an input on a DCE device. Similarly, RD is an input for DTE and an output for DCE.

-   When you wire DCE equipment to DTE equipment (computer-to-terminal or computer-to-computer), you must trick each device into thinking the other is DCE. For example, both DTE devices expect to transmit on TD and RD. You must cross-connect the wires so that one device’s transmit pin goes to the other’s receive pin, and vice versa.

-   Three sets of signals must be connected in this fashion for DTE-to-DTE communication (if you choose to connect them all). TD and RD must be connected. RTS and CTS must be connected. Each side’s DTR pin must be connected to the BCD and DSR pins of the peer.

-   To add to the confusion, a crossed cable for DTE-to-DTE communication is often called a “null modem” cable. You might be tempted to use a null modem to hook up a modem, but since modems are DCE, that won’t work! A cable for a modem is called a “modem cable” or a “straight cable.”

Exhibit B shows assignments and connections for both null-modem and straight-cables. Only signals used in the real world are shown.

## Exhibit B Pin assignments and connections for DB-25 cables

| Legend | Straight | Null modem |
|---|---|---|
| Frame ground FG | 1 | 1 |
| Transmitted data TD | 2 | 2 |
| Received data RD | 3 | 3 |
| Request to send RTS | 4 | 4 |
| Clear to send CTS | 5 | 5 |
| Data ready DSR | 6 | 6 |
| Signal ground SG | 7 | 7 |
| Data carrier DCD | 8 | 8 |
| Data terminal ready DTR | 20 | 20 |

## 31.2 ALTERATIVE CONNECTORS

The following sections describe the most common modern connector systems, DB-9 and RJ-45. Despite their physical differences, these connectors provide access to the same electrical signals as a DB-25. Devices that use different connectors are always compatible if the right kind of converter cable is used.

## The DB-9 variant

The DB-9 is the most common modern-day embodiment of RS-232. It's a 9-pin connector that looks like a "DB-25 junior" and supplies the eight most commonly used signals. Pin 9 is left unconnected.

## Exhibit C A male DB-9 connector

| Connector | Pin numbers |
| --- | --- |

![](img/579efec8c67772f31ecf34844bbb71a2_1214_0.png)

## Table 31.2 DB-9 Pinout

| DB-9 | Signal | Function |
|---|---|---|
| 1 | DCD | Data carrier detect |
| 2 | RD | Received data |
| 3 | TD | Transmitted data |
| 4 | DTR | Data terminal ready |
| 5 | SG | Signal ground |
| 6 | DSR | Data set ready |
| 7 | RTS | Request to send |
| 8 | CTS | Clear to send |

## The RJ-45 variant

The RJ-45 is an 8-wire modular telephone connector. The use of RJ-45s makes it easy to run serial communications through your building's existing wiring if the wiring plant was installed with twisted-pair Ethernet in mind.

RJ-45 jacks for serial connections are usually not found on computers or on garden-variety serial equipment, but they are often used as intermediate connectors for routing serial lines through patch panels. RJ-45s are compact, self-securing, cheap, and easy to crimp onto the ends of custom-cut cables. An inexpensive crimping tool is required.

Several systems map the pins on an RJ-45 connector to those on a DB-25. Table 31.3 shows the official RS-232 standard, which is used only haphazardly.

## A male RJ-45 connector

Exhibit D

| Connector | Pin numbers |
| --- | --- |
| | Top View |

![](img/579efec8c67772f31ecf34844bbb71a2_1215_0.png)

Table 31.3 Pins for an RJ-45 to DB-25 straight cable

| RJ-45 | DB-25 | Signal | Function |
| --- | --- | --- | --- |
| 1 | 6 | DSR | Data set ready |
| 2 | 8 | DCD | Data carrier detect |
| 3 | 20 | DTR | Data terminal ready |
| 4 | 7 | SG | Signal ground |
| 5 | 3 | RD | Received data |
| 6 | 2 | TD | Transmitted data |
| 7 | 5 | CTS | Clear to send |
| 8 | 4 | RTS | Request to send |

A well-thought-out standard for RJ-45 to DB-25 wiring was created by Dave Yost. If you're planning to use a significant amount of serial cabling, be sure to check it out at youostost.com/RJ45-serial.

## 31.3 HARD AND SOFT CARRIER

UNIX expects to get the DCD signal, carrier detect, go high (positive voltage) when a serial device is attached and turned on. If your serial cable is a DCD line and your computer really pays attention to it, you are using what is known as hard carrier. For certain devices (such as traditional terminals), soft carrier is a great blessing. You can get away with using three wires for each serial connection: transmit, receive, and signal ground. However, modern connections really need DCD. If a terminal is connected to a modem and the carrier signal is lost, the modem should hang up (especially on a long call). You can specify soft carrier for a serial port in the configuration file for whatever you use in conjunction with the port (e.g., gettydefs initab for login terminal or printcap for printer). You can also use stty -clocal to enable soft carrier on the fly. 

### Serial Devices and Terminals

For example, `sudo stty -clocal /dev/ttyS1` enables soft carrier for the port ttyS1.

## 31.4 HARDWARE FLOW CONTROL

The CTS and RTS signals make sure that a device does not send faster than the receiver can process. For example, if a modem is in danger of running out of buffer space (perhaps because the connection to the remote is slower than the serial link between the local machine and the modem), it can tell the computer to shut up until room becomes available in the buffer. Flow control is essential for high-speed devices and is also very useful for serial printers. Systems that not support hardware flow control (either because the serial ports do not understand it or because CTS and RTS are disconnected), flow control can sometimes be simulated with software using the ASCII characters XON and XOFF. However, flow control explicitly supported by high-level software, and then does not work well. XON and XOFF are <Control-Q> and <Control-S>, respectively. This is a problem for emacs users because <Control-S> is the default binding for emacs. To fix the problem, bind the command to another key or use start and stop to change the terminal's idea of XON and XOFF.

Most terminals ignore the CTS and RTS signals. By jumping pins 4 and 5 together at the terminal end of the cable, you can fool terminals that require a handshake before they communicate. When the terminal sends out a signal on pin 4 saying "I'm ready", it gets the same signal on pin 5 saying "Go ahead." With soft carrier, hardware flow control can be set through configuration files or with the stty command.

![](img/579efec8c67772f31ecf34844bbb71a2_1216_0.png)

On Sun, flow control for built-in serial ports must be set up with the eeprom command.

![](img/579efec8c67772f31ecf34844bbb71a2_1216_1.png)

On some HP platforms, you may need to set flow control for built-in serial ports with the Guardian Service Processor (GSP).

## 31.5 SERIAL DEVICE FILES

Serial ports are represented by device files in or under /dev. Even today, many computers have one or two serial ports built in, mainly as a communication mechanism of last resort. In the past, such ports were usually known by names such as /dev/ttyA and /dev/ttyB, but naming conventions have diverged over time, and those ports are now often named /dev/ttyS0 or /dev/tty1.

## seterial: set serial port parameters under Linux

Sometimes, more than one device file refers to the same serial port. For example, /dev/cua/a on a Solaris system refers to the same port as /dev/term/a. However, the minor device number for /dev/cua/a is different:

```
solaris$ ls -l /dev/term/a /dev/cua/a
crw---- 1 uucp uucp 37 131072 Jan 11 16:35 /dev/cua/a
crw-rw-rw- 1 root sys 37 0 Jan 11 16:35 /dev/term/a
```

As always, the names of device files do not really matter. Device mapping is determined by the major and minor device numbers, and the names of device files are merely a convenience for human users.

Multiple device files are primarily used to support modems that handle both incoming and outgoing calls. In the Solaris scheme, the driver allows /dev/term/a to be opened only when DCD is asserted by the modem, indicating the presence of an active (inbound) connection (assuming that soft carrier is not enabled on the port.). /dev/cua/a can be opened regardless of the state of DCD; it's used when connecting to the modem to instruct it to place a call. Each device file is blocked while the other is in.

![](img/579efec8c67772f31ecf34844bbb71a2_1217_0.png)

On HP-UX, device files are not always created automatically. You can use the ioscan command to force the system to look for them, something like

```
hp-ux$ sudo ioscan -C tty -fn
```

You can create the device files with

```
hp-ux$ sudo mksf -H port-from-ioscan-output -d asio0 -a -v
```

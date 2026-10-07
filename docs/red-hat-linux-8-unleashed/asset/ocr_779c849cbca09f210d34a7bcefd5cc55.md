# CHAPTER 4 Post-Installation Configuration

DSR 6 6 in 0 Data Set Ready
GND 7 5 Signal Ground
DCD 8 1 in 0 Data Carrier Detector
DTR 20 4 out 1 Data Terminal Ready
RI 22 9 in 0 Ring Indicator

![](bbox=[0.335, 0.212, 0.664, 0.477])

FIGURE 4.8 KDE's kpppp client can be used to find and configure an available modem.

The sample output is a display of the associated device's port signals. Another tool is the seterial command that can be used to display port statistics and reconfigure a serial port's system interrupt or speed. This can be handy when using some serial devices, such as a cellular phone that requires specific serial-port characteristics. To get information about a specific port, use seterial, along with the device name like this:

```
# seterial -a /dev/ttyS0
/dev/ttyS0, Line 0, UART: 16550A, Port: 0x03f8, IRQ: 4
Baud_base: 115200, close_delay: 50, divisor: 0
closing_wait: skip_test
```

In this example, the characteristics of /dev/ttyS0 are displayed. The seterial command can also be used to configure or fine-tune a port's characteristics using 32 different command-line options and values.

One option for using a legacy serial device as a modem on PC that doesn't have a serial port but supports USB is to use a USB-to-serial converter. These devices provide a serial-port dongle and plug in to a USB hub or port. You can see the output and designated serial port by looking at the output of the dmesg command:
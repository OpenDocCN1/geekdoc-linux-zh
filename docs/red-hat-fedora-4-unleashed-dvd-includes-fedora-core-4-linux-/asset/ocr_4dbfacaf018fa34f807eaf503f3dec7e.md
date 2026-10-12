After you press Enter, you will be prompted for the root password. Enter the password and click OK. The system-config-soundcard will try to automatically detect and configure your sound card. You will then see a dialog you can use to test your sound card settings, as shown in Figure 4.5. Click on the Play test sound button to listen to a sample sound.

![](bbox=[0.277, 0.186, 0.738, 0.38])

**FIGURE 4.5** The system-config-soundcard client is used during an X session to configure a sound card for Fedora.

# Detecting and Configuring a Modem

More than 33 million users in the United States now connect to the Internet with cable or DSL service, but for many users a modem is the standard way to connect with an Internet service provider (ISP) using the Point-to-Point Protocol (PPP). Other common tasks for modems include sending and receiving faxes. If you add or change your modem after the initial installation, you will need to configure Fedora to use the new modem to perform all these tasks.

Fedora includes several tools you can use to configure and use an internal or external modem in your notebook or PC. Chapter 18, "Internet Connectivity," contains the details about configuring Fedora to connect to the Internet using a modem. This section covers how to configure and use modems using serial ports (using a standard formerly known as RS232, but now termed EIA232) or USB.

# Configuring a Serial-Port Modem

Linux uses /dev/ttySX, /dev/ttyUSBX, or /dev/usb/ttyUSBX for serial ports, where X can range from 0 to 15. Many additional ports can be added to a system using multiport cards or chained USB devices. A PC's integral serial ports are generally recognized at boot time. To see a list of recognized ports for your system, pipe the dmesg command output through the fgrep command like so:

```
```
# dmesg | fgrep tty
ttyS00 at 0x03f8 (irq = 4) is a 16550A
ttyS01 at 0x02f8 (irq = 3) is a 16550A
```
```
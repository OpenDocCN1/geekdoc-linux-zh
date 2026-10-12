# Character Devices

In this section, you will select support for devices that communicate with the kernel via a stream of characters. These devices include terminals, serial ports, printers, and others. For most server applications, you will need, at a minimum, support for terminal devices, parallel printer support, and a new option for the 2.2 series of kernels, Unix98 PTY support.

This section also allows you to select support for multiport serial cards, such as Stallion cards or Rocketport cards that support multiple serial devices.

Under this section, the minimum support normally required is to configure console support on a virtual terminal and virtual terminal support. Optional support for the console on a serial terminal is also included here, which is often useful in situations where it is inconvenient to have a monitor attached to the system.

> **Caution**
> 
> Enabling the console on a serial terminal option is not sufficient to get this feature to work properly. In addition, you must specify the device to which you want kernel messages to be sent. This is done by passing the kernel command-line option `console=/dev/ttyW` at the LILO prompt or by adding this option to the append line in your `lilo.conf` file.

Serial port support under Linux includes support for not only the standard four ports supported by the BIOS of most modern PCs, but also support for many multiport serial boards, such as those needed to support a modem pool. This support is also important for serial-based data acquisition systems. Support is also available for IRQ sharing among serial ports that have such support in the hardware.

If you have ever experienced the problem of running out of PTYs on your multiuser systems, the support of Unix98 PTYs will be important to you. Unlike systems based on the Linux 2.0 kernel, which were limited to support for 256 pseudo terminals, the Linux 2.2 kernel can support up to 2048. The Unix98 support works differently than the old BSD-style support. If this options is selected, a program opens a pseudo terminal multiplexer device, `/dev/ptmx`, which dynamically creates an associated slave tty using the `/dev/pts` filesystem. As you might surmise, this requires that you include support for this filesystem later on in the configuration.
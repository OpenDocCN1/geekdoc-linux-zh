
To find external modems that use serial port connections. USB external modems plug into the standard USB port on the workstation and communicate as a normal USB device.

Ubuntu can usually automatically detect an externally connected modem, whether it’s a serial or USB connection. If Ubuntu doesn’t automatically detect your external modem, first check to make sure the modem is turned on when you boot your system. If it did, then check to make sure the cable is secured to the proper port on the workstation.

*Internal modems* are built inside the workstation. Some workstation motherboards contain modems built into them, while others use cards you can plug directly into the motherboard. Ubuntu has somewhat of a checkered past in dealing with internal modems. If Ubuntu automatically detects your internal modem, you’re in good shape. If it doesn’t, you may have to invest in an external modem instead.

> **There’s a special type of internal modem, called Winmodem, that may cause problems for you. Winmodems perform some of the functionality of a modem in software that (as the name suggests) runs on the Windows platform. You must be careful about Winmodems because not all of them can be used by Linux.**

> **The best resource for working with Winmodems in Linux is the linmodems.org web site:** `http://linmodems.org`. This site provides detailed advice on which Winmodems are directly supported in Linux and how to obtain drivers for those that aren’t.

The download speed of dial-up modems is limited to 56 kilobits per second (kbps). Unfortunately, this speed rate is not often achieved because the actual transmission speed of a connection depends on the clarity of the analog signal, which for many telephone lines isn’t all that great. What may be annoying static on your phone line when you talk is death to a modem connection!

## DSL Modem

The DSL modem uses normal telephone lines to communicate to the ISP. However, instead of converting the digital signal to analog, the DSL modem sends a digital signal directly across the telephone line. The telephone line carries both the analog voice signal and the digital signal on the same wires to the telephone provider, which in turn must separate the two signals, connecting the digital signal to its servers and the analog signal to the appropriate telephone exchange equipment.

Your telephone provider must have the proper equipment installed to be able to provide DSL service to your location. Not all areas are converted to support DSL connectivity. Check with your telephone provider to determine whether they support DSL modems in your area.

Three basic types of digital modems can be used on a digital telephone line:

- **Integrated services digital network (ISDN):** The ISDN modem is the oldest technology and is the most sensitive to static. It offers up to 128 kbps of connectivity speed (more than double the speed of a dial-up modem), provided that the end connection is within 3.4 miles of the telephone exchange equipment. Performance degrades the farther away you are from the telephone exchange, which is one reason why ISDN didn’t catch on all that well.

## Part 3: Managing Your Workstation

There are three current standards and one proposed standard in the wireless network card world:

- **802.11a:** Provides up to 54 Mbps of data connectivity but has only a 35-meter range.
- **802.11b:** Provides only up to 11 Mbps but has a larger range than the 802.11a specification.
- **802.11g:** Provides up to 54 Mbps and has a larger range than the 802.11b specification.
- **802.11n (proposed):** Provides up to 248 Mbps, with a range of up to 70 meters.

The benefits of the new 802.11n wireless have made it a commercial success, even before its formal adoption as a network standard.

The downside to wireless network cards is that many of them don’t provide drivers for Linux. Ubuntu can detect and use many wireless network cards, but not all of them.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_371_0.png)

> **The NDISWrapper project is an open-source project for configuring wireless network cards in Linux.** The NDISWrapper software acts as a bridge between the Linux kernel and the Windows drivers provided for a wireless network card. NDISWrapper allows you to use any wireless network card that has drivers for Windows, which is just about every wireless network card available.

> **To use NDISWrapper, you must follow these steps:**
>
> 1. Install the `ndisgtk` package (see Chapter 13, “Software Installs and Updates”).
> 2. Copy the Windows drivers provided for your wireless network card onto your Ubuntu system.
> 3. Start a Terminal session window, then change to the folder that contains the wireless network card drivers using the `cd` command (see Chapter 19, “The Ubuntu Command Line”).
> 4. On the command line, use the `ndiswrapper` command to install the Windows driver using the `.inf` file provided:
>
>    ```bash
>    sudo ndiswrapper -i file.inf
>    ```
>
>    where `file.inf` is the name of the `.inf` file for your Windows driver.
> 5. Load the NDISWrapper into the kernel using the command:
>
>    ```bash
>    sudo modprobe ndiswrapper
>    ```
> 6. Create an alias device for the new network interface:
>
>    ```bash
>    sudo ndiswrapper -m
>    ```
> 7. Exit Terminal and reboot your system.
>
> If all went well, the next time you log into Ubuntu the Network Manager applet should show a list of the wireless access points available.

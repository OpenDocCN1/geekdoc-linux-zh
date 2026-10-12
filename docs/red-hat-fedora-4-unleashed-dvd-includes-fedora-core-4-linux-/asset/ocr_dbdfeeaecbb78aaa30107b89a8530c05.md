+   - Pointing devices—Mice, tablets, and possibly touchscreens
+   - Printers—Various printer models
+   - RAM—Issues regarding types of system memory
+   - Sound cards—Issues regarding support
+   - Specific motherboard models—Compatibility or other issues
+   - Specific PCs, servers, and laptop models—Compatibility reports
+   - Storage devices—Removables, fixed, and others
+   - Video cards—Console issues (X compatibility depends on version of X11R6 or vendor-based X distribution used)

If you have a particular laptop or PC model, you should also check with its manufacturer for Linux support issues. Some enlightened manufacturers now offer a Linux operating system preinstalled, or have an in-house Linux hardware certification program. Laptop users will definitely want to browse to Linux on Laptops at http://linux-laptop.net/.

If you cannot find compatibility answers in various on-line databases, continue your research by reading the Linux Hardware HOWTO at http://www.tldp.org/HOWTO/Hardware-HOWTO/.

At that address, you will find loads of general information and links to additional sources of information. Keep in mind that when PC hardware is unsupported under Linux, it is generally because the manufacturer cannot or will not release technical specifications or because no one has taken the time and effort to develop a driver. If you hit a roadblock with a particular piece of hardware, check the hardware manufacturer’s support web pages, or Google.com’s Linux pages at http://www.google.com/linux. You can then type in a specific search request and hopefully find answers to how to make the hardware work with Linux. This is also a good way to research answers to questions about software issues.

# Preparing for Potential Hardware Problems

Fedora Core will work “out-of-the-box” with nearly every Intel-based Pentium PC motherboard and laptop; drivers for thousands of different types of hardware peripherals are included. But you can sometimes run into problems if Linux does not recognize a hardware item, if Fedora does not correctly initialize the hardware, or if an initialized item is incorrectly configured. For these reasons, some hardware items are prone to creating problems during an install. In the sections that follow, you learn some important pointers for avoiding these problems or resolving those that do occur.

# Controllerless Modems

As you read earlier, most Linux hardware-related installation problems stem from a lack of technical specifications from the manufacturer, thwarting efforts of open-source developers to create a driver. In the recent past, one hardware item that triggered both types of difficulties was the controllerless modem, also colloquially known as a WinModem. The
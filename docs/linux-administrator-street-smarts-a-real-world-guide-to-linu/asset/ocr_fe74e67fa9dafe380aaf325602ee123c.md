# Task 2.4: Configure USB Devices

USB 1.0, the first incarnation of USB, was finalized in 1996. Since then, USB has played an increasingly important role. Today, mice, printers, scanners, digital cameras, CD-RW drives, and many other devices can interface to computers via USB. Thus, being able to configure USB devices to work with Linux is an important skill.

USB was designed to permit relatively painless *hot-plug* operation, meaning that devices can be plugged into the computer and unplugged while the computer operates. Unfortunately, this type of operation is alien to Linux's basic driver model. Thus, to accommodate USB's hot-plug nature, various special utilities and interfaces have been developed. Configuring USB devices means working with these utilities.

# Scenario

To support efforts to digitize old documents and presentations, your employer has purchased a film scanner. This scanner uses a USB interface and must be configured to work correctly with Linux; however, your default Linux configuration prevents ordinary users from accessing the scanner when it's plugged into the computer and turned on. You must reconfigure Linux to enable ordinary users to work with the scanner.

# Scope of Task

This task involves examining configuration and system status files to learn about your hardware and then modifying configuration files to have the system configure hardware in the way you want. If you're lucky, you won't need to engage in the low-level configuration described here; many distributions provide tools that automatically detect and configure a wide variety of USB devices. These tools fail with obscure or very new hardware, though, necessitating manual configuration.

# Duration

This task will take about half an hour to complete. Once you're familiar with the procedure, you should—in theory—be able to perform similar tasks in half that time. In practice, though, adding hardware often involves overcoming unexpected problems. Thus, when you add your own truly unknown hardware, you could end up taking anywhere from a few minutes to several hours to configure it.

# Setup

To complete this task, you need *root* access to a Linux computer. Ideally, you should have a scanner or other USB device that's not accessible to ordinary users in your default configuration. (For this task, I use a Minolta DiMAGE Scan Elite 5400 film scanner and Fedora Core 5 as the example hardware and software.) This example assumes that your system uses the *udev* filesystem for handling device files, which is common with modern distributions. If you lack
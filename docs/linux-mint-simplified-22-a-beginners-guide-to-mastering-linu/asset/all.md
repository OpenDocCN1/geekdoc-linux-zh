![](image_rsrc4AX.jpg)

Linux Mint

Simplified

A Beginner’s Guide to Mastering Linux Mint

by

Mary Bless

Preface

Welcome to the Linux Mint Book! Whether you're a seasoned Linux user or just starting your journey into the world of Linux Mint, this book is designed to be your comprehensive guide. Linux Mint is an operating system designed for desktops and laptop computers. It is meant to work 'out of the box' and comes pre-installed with the programs that most people require.

This book is not just about teaching you how to install Linux Mint, although that's certainly a part of it. Instead, it's about empowering you to take control of your system, to understand how it works, and to customize it to fit your needs perfectly. Linux Mint is known for its simplicity and elegance and we'll explore all of that and more in the pages that follow.

In this book, you'll find everything from the basics of getting started with Linux Mint to advanced topics like monitoring and package management. We'll walk you through the installation process, help you configure your system, and introduce you to the vibrant Linux Mint community. Along the way, we'll provide tips, tricks, and best practices to help you get the most out of your Linux Mint experience.

Whether you're a developer, sysadmin, or simply an enthusiastic hobbyist, Linux Mint has something for you. It's a platform for simplicity and out-of-the-box experiences, and we hope this book will encourage you to dive in and discover everything it has to offer.

So grab your favorite beverage, settle in, and let's go on this journey together. Welcome to the Linux Mint community! Enjoy the ride!

Conventions Used in This Book

Throughout this book, we use certain conventions to help you navigate and understand the content more easily:

Command-line examples: Commands you can run in your terminal are formatted like this:

ls -la.

File paths and code snippets: File paths and code snippets are formatted like this:

/etc/hosts.

Syntax: Syntax of commands are formatted like this:

ls [option] [file/directory]

Feedback

Your feedback is invaluable to us as we strive to improve this book and provide you with the best possible learning experience. If you have any questions, comments, or suggestions, please don't hesitate to contact us at mary@marybless.com.

Mary Bless

Table of Contents

[Table of Contents](#part0004.xhtml)

[Introduction](#part0005.xhtml_a45B)

[System Requirement](#part0006.xhtml_a45C)

[Installation](#part0007.xhtml_a45D)

[Let’s Explore the Desktop](#part0009.xhtml_a45E)

[Customizing the Desktop Environment](#part0013.xhtml_a45F)

[Filesystem Hierarchy](#part0018.xhtml_a45G)

[Managing files and Directories Using File Manager](#part0021.xhtml_a45H)

[Using External Storage Devices](#part0024.xhtml_a45J)

[Using The Terminal](#part0026.xhtml_a45K)

[Navigating Files and Directories Using Terminal](#part0028.xhtml_a45M)

[Using sudo for Elevated Access](#part0032.xhtml_a45N)

[Package Management](#part0034.xhtml_a45P)

[Configuring Repositories](#part0042.xhtml_a45R)

[Install New Fonts](#part0045.xhtml_a45S)

[Managing Users](#part0046.xhtml_a45T)

[Keeping Your System Up-to-Date](#part0056.xhtml_a45U)

[Backing Up Your System](#part0059.xhtml_a45V)

[Network](#part0066.xhtml_a45W)

[Monitoring System Resources](#part0073.xhtml_a45X)

[Firewall](#part0079.xhtml_a45Y)

[Process Management](#part0081.xhtml_a45Z)

[User Permissions and Access Control](#part0085.xhtml_a460)

Chapter 1                  

Introduction

Based on Ubuntu, Linux Mint is a free and open-source Linux desktop and laptop operating system. Its user-friendly installation procedure and comfortable desktop environment make it an easy tool to use. There are numerous free and open-source apps included with Linux Mint. With its distinct Update Manager, sturdy Linux architecture, and cautious software upgrades, Linux Mint is renowned for its safety and dependability. It needs relatively little upkeep. Additionally, Linux Mint welcomes user input to help the project get better.

Here's a brief overview:

History: Clement Lefebvre developed Linux Mint in 2006 with the goal of creating an easy Linux distribution built on the Ubuntu platform. Lefebvre set out to design a desktop experience that was both more sophisticated and user-friendly than anything that was offered at the time. Initially built on top of Ubuntu, Linux Mint separated itself apart with its own default apps, codecs, and desktop layout, which was more conventional.

In 2011, Linux Mint changed its default desktop environment from GNOME to Cinnamon, a variant of GNOME Shell that combines a more classic desktop experience with current innovations. This decision strengthened Linux Mint's reputation as a user-friendly distribution for both novice and veteran Linux users.

Philosophy: Linux Mint adheres to the following principles: simplicity, modernism, user centrality, versatility, and customization. It adheres to the KISS (Keep It Simple, Stupid) principle, intending to provide a fully functional basic system upon which users can build based on their requirements.

Release Model: Linux Mint generally provides two types of releases. Long-Term Support (LTS) and regular releases.

Package Manager: A Linux distribution's adaptability among the multitude of distributions depends on its package manager. Linux Mint, which is based on Ubuntu, relies heavily on the Advanced Package Tool (APT) for package management. APT manages the installation, updating, and removal of packages. It has every feature that makes a strong package manager, including dependency resolution.

Documentation and Community Support: Linux is well-known for its community support and the abundance of documentation available online. Linux Mint is no exception, with considerable documentation available through the Linux Mint Forums, which includes detailed tutorials, troubleshooting hints, and explanations for many components of the system. Furthermore, The Linux Mint project maintains comprehensive documentation that covers various aspects of the operating system.

Linux Mint has earned acclaim for its user-friendly approach and robust feature set, making it a preferred choice for both beginners and advanced users alike.

Chapter 2                  

System Requirement

Linux Mint has very low system requirements because it is meant to be lightweight and efficient. Here are the essential system requirements for Linux mint. In this, we have provided both minimum and recommended values: -

Processor: Any processor from today should work OK. Linux runs well on either Intel or AMD x86_64 (64-bit) architecture.

Memory (RAM): The minimum amount of memory required is approximately 4 GB of RAM, however it is advised that you have at least 8 GB for smoother performance, especially if you intend to use for a graphic intensive environment.

Storage: Linux Mint takes only 10 to 20 GB of disk space. However, you'll need more capacity to store installed packages, user data, and apps. A drive with at least 100 GB of space is suggested, but more is preferable, particularly if you intend to install a lot of software or have huge user data.

Graphics: Linux Mint supports a broad variety of graphics hardware, including integrated and dedicate graphics cards. It includes the most common drivers and supports both open-source and proprietary drivers.

Networking: A internet connection is necessary for both package updates and new package installation. Linux Mint supports both wired (Ethernet) and wireless (WiFi) connectivity. Most common network and WiFi card drivers are supported.

Display and Input Devices: Linux Mint supports a wide range of display and input devices, including monitors, keyboards, mouse, touchpads, and other peripherals. Compatibility may differ depending on hardware manufacturer and driver support. Please check your hardware manufacturer's website before proceeding with installation to ensure compatibility.

Overall, Linux Mint can run on practically any modern computer hardware, ranging from older systems with limited capabilities to high-end PCs with advanced hardware. Its low system requirements make it appropriate for usage on older PCs, virtual machines, and lightweight devices, as well as more powerful hardware that allows users to fully exploit its customization and versatility. The KISS (Keep It straightforward, Stupid) approach makes installation straightforward and transparent.

Chapter 3                  

Installation

Linux Mint works out of the box, with full multimedia support and is extremely easy to use. Installing Linux Mint is a simple process that will have you up and running quickly on your computer. Follow these instructions to make a bootable USB drive, configure your system settings, and start exploring the power of Linux Mint's user-friendly interface.

Here's a basic guide to installing Linux Mint:

Backup your data

Backup your current data if it is already on the system before installation since we will be installing Linux Mint as the only operating system, which will erase everything from the hard drive.

Download Linux Mint ISO: Visit the Linux Mint website and select the Cinnamon Edition. The download page provides both torrent and direct download options. To use the direct download method, click on any available nearby mirror in the list.

The Downloads page.

[https://linuxmint.com/edition.php?id=316](https://linuxmint.com/edition.php?id=316)

Then open any global mirror, such as the one below.

[https://mirrors.cicku.me/linuxmint/iso/stable/22/linuxmint-22-cinnamon-64bit.iso](https://mirrors.cicku.me/linuxmint/iso/stable/22/linuxmint-22-cinnamon-64bit.iso)

![](image_rsrc4AY.jpg)

Create Bootable Media: Once the ISO file has been downloaded, you must create a bootable USB drive or CD/DVD. To transfer the ISO file to a USB device use Rufus or Etcher on Windows, or the dd command on Linux.

Write ISO to USB

We'll utilize the Rufus utility on the Windows workstation where we downloaded the ISO image. To utilize USB as installation media, we require at least 4 GB of USB capacity. Here are the procedures required to write a Linux Mint ISO image on a USB drive using Rufus:

1.  Download Rufus: If Rufus is not already installed on your PC, you can get it from the Rufus.ie official website.

2.  Insert USB Drive: Connect the USB drive to your computer.

3.  Open Rufus: Run Rufus on your computer. It may require administrator access for it to function.

![](image_rsrc4AZ.jpg)

4.  Select USB Drive: Choose the desired USB drive in Rufus by selecting it from the "Device" drop-down menu.

5.  Select Linux Mint ISO Image: Click the "SELECT" button located next to "Boot selection" and proceed to the downloaded Linux Mint ISO image folder. Choose the ISO file.

6.  Partition Scheme and File System: For BIOS, pick "MBR" or "GPT" for UEFI as the "Partition Scheme." Click "File System" and select "NTFS".

7.  Start the Process: Click the "START" button. A warning window may appear, telling you that all data on the USB drive will be deleted. Click "OK" to continue.

8.  Write in ISO Mode: Choose "Write in ISO Image mode" when prompted, then click "OK" to proceed.

![](image_rsrc4B0.jpg)

9.  Wait for Completion: At this point, Rufus will begin writing the ISO image of Linux Mint to the USB drive. The duration of this operation may vary based on the USB drive and computer speeds.

10.  Completion: When Rufus finishes writing the ISO image to the USB device, the progress bar will change to "Ready" Text. You can now close Rufus and safely eject the USB drive from your computer.

![](image_rsrc4B1.jpg)

11.  That's it! You successfully transferred the Linux Mint ISO image to a USB device with Rufus.

Start Installation

Disable the secure boot option: (This is an optional step and may not be necessary in most cases.)

Disabling Secure Boot mode is not required for Linux Mint installation. However, because of the possibility for problems or incompatibility with unsigned bootloaders or kernels, it is suggested that Secure Boot be disabled during installation.

To disable Secure Boot mode during installation, you must open your computer's BIOS/UEFI settings. The BIOS/UEFI settings vary depending on the manufacturer of your computer; see the hardware manual to access the BOIS/UEFI.

![](image_rsrc4B2.jpg)Boot from Installation Media: To boot from the bootable USB device or CD/DVD, insert it into your computer. In order to prioritize the USB drive or CD/DVD, you might need to adjust the boot order in your BIOS or UEFI settings. To find out how to obtain the boot menu, refer to your computer's manual.

Start Linux Mint Live Session: When you boot from the installation media, a menu will appear. Select "Start Linux Mint." It will launch the Linux Mint live session.

In Linux, a live session is defined as executing the operating system directly from bootable installation media (such as a USB flash drive or DVD) rather than installing it on your computer's hard drive. This allows you to use a variety of tools for troubleshooting and manipulating your computer's drives, data, and hardware without having to worry about anything running on it. It also ensures that your system is compatible with running the selected Linux operating system.

Connect to Network: Although an internet connection is not required for Linux Mint installations, it is recommended that you have one to get NTP information, updates, hardware drivers, and other software packages during the installation process. In Linux Mint, you can connect to the internet via Ethernet (wired) or Wi-Fi (wireless), depending on your network configuration and hardware capabilities.

Connect Wi-Fi: To connect to a Wi-Fi network, follow the steps below:

1.  Click on the network icon in the system tray.

![](image_rsrc4B3.jpg)

2.  A list of Wi-Fi networks will appear. Click on the name of your Wi-Fi network. ![](image_rsrc4B4.jpg)

3.  When prompted, enter the password for your Wi-Fi network and click "Connect" to establish the connection.![](image_rsrc4B5.jpg)

Install Linux Mint:  Double-click on "Install Linux Mint" icon.

![](image_rsrc4B6.jpg)

Select Language and Keyboard Layout: Select your desired language and keyboard layout on the following screens.

![](image_rsrc4B7.jpg)Multimedia Codecs: Check the box for multimedia codec. It's beneficial to enable multimedia codecs while installing Linux Mint since it lets you play back common multimedia formats right away, like MP3 audio and H.264 video files, without requiring you to manually install any software or codecs after the installation.

Install Type: The screen options differ depending on the system on which you are installing Linux mint. The first scenario involves installing only one operating system on the computer, which normally takes up the entire disk. Another alternative is to install on a system that already has another operating system, such as Microsoft Windows, and you wish to install Linux Mint alongside it to dual boot the system.

Only OS (Single Boot): Please take a data backup before starting, as this will destroy any data on the drive.

*   Erase the disk: This option automatically partitions the drive.  This option includes the "Advanced features" button, which allows you to choose between LVM and ZFS file system type for the disk partition.

![](image_rsrc4B8.jpg)

*   Something else: This option allows you to do manual disk partitioning. If you select this option, you need to create partitions for the root filesystem ("/"), swap space, and any additional partitions you may require, such as /home. 

Dual boot:

You have three options: you can choose to install Linux Mint alongside an existing operating system (dual-boot), replace the existing operating system, or manually partition the disk. If you're unsure, the option to install alongside an existing OS is usually safe.

![](image_rsrc4B9.jpg)

Once you've selected the option that you want, click "Install Now." The system will ask you for confirmation; select Continue.

![](image_rsrc4BA.jpg)Time zone and time:   The objective of the "Where are you?" screen is to assist you choose time zone. If you are connected to the internet, it automatically selects your location. Otherwise, you click on your current location on the world map.

Set Up User Account: On the "Who Are You" screen, enter your name, computer name, username, and password. It is also possible to select for automatic login without needing to input a password every time. Press Continue.![](image_rsrc4BB.jpg)

Install Linux Mint: Linux Mint will begin installing to your system. This process may take some time depending on your computer's speed and the size of the disk.

![](image_rsrc4BC.jpg)

Completion and Restart: After the installation is complete, you will be prompted to restart your computer. Remove the installation media when prompted.

![](image_rsrc4BD.jpg)![](image_rsrc4BE.jpg)

Login and Configurations: After rebooting, you'll see the Linux Mint login screen. Enter your password and log in to your new Linux Mint installation.

Congratulations! You have successfully installed Linux Mint on a blank disk and are now ready to explore and use your new operating system.

Chapter 4                  

Let’s Explore the Desktop

Linux Mint is a famous Linux distribution recognized for its user-friendly interface and emphasis on offering a familiar desktop environment for users who have switched from other operating systems such as Windows or macOS. This is an overview of the Linux Mint desktop environment. There are various desktop environment options available in Linux Mint, each with a distinct appearance and feel:

Cinnamon: This is Linux Mint's flagship desktop environment. It promises to offer a contemporary, conventional desktop experience with a taskbar, system tray, and customizable panels, similar to that of MS Windows.

MATE: Linux Mint also provides the MATE desktop environment. It is an extension of the well-known GNOME 2 desktop environment, which is straightforward and effective. MATE is appropriate for people who want a more conventional desktop layout or on older hardware.

Xfce: Focusing on speed and efficiency, Xfce is a lightweight desktop environment. It works well for people who want a more straightforward desktop experience without compromising customization possibilities, or for PCs that are older.

In this chapter, we will explore Linux Mint's flagship Cinnamon desktop environment. Originally created for Linux Mint, Cinnamon is a sleek and intuitive desktop environment that can be installed on other Linux distributions as well. It seeks to give people switching from other operating systems like Windows or macOS a comfortable and effective computing experience. Here is a detailed explanation of the cinnamon components:

Cinnamon Panel

![](image_rsrc4BF.jpg)

Usually spanning the bottom of the screen, the panel is the primary Cinnamon interface component. It consists of:

*   Menu

*   Favourites

*   Grouped windows list

*   System Tray

*   Important icons

*   Corner bar

Menu: The Mint Menu, which is located in the left corner of the taskbar, offers access to locations, applications, system settings, and session options. It allows programs to be categorized and includes a search function for convenience.

Favourites: The Favourites menu displays a selection of programs that you commonly use and want to access quickly.

Grouped windows list: This is a window list applet designed to resemble the Windows 7 taskbar (at least partially). Some of the important aspects include:

*   App grouping: this groups the window of each program into a single button

*   Previews: When hovering over a button, a menu can display previews of all windows managed by that button.

*   Pinning programs: Pin your favourite programs to workspaces.

*   Drag 'n' Drop: You can reorder your programs. Drop from the menu and panel launchers. Drag menu items from Cinnamon's menu and panel launcher applet to this applet, and the program will be pinned.

*   Context Menu: There are multiple actions available from the context menus of the buttons. The context menu appears when you right-click any of the icons.

System Tray: Displays icons for background services and system notifications.

Important icons: Right corner of the bar has speaker, network, removable devices, date/calendar, battery and Bluetooth icons. Click any of these icons to open its popup. Sound icon allows you to adjust speaker and microphone volume. Other icons give you the option to adjust network and Bluetooth settings.

Corner Bar: The corner bar is used to display the desktop, desklets, workspace selector, or window selector. Left-clicking the mouse on the corner bar minimizes all windows and displays the desktop, whereas right-clicking brings up the context menu. Hovering over the Corner Bar (like in Windows) allows you to rapidly "peek at desktop"; you may enable or disable this functionality in the corner bar's settings.

![](image_rsrc4BG.jpg)

Clock

The clock is located on the right side of the bar and displays the current time by default. When you hover over it, it shows the date and day of the week.  A right-click provides you the ability to configure it.

Understanding the Menu

![](image_rsrc4BH.jpg)

All Applications

Show all tools and applications installed on the Linux Mint computer, arranged alphabetically.

Categories

The menu is organized into multiple categories, such as Accessories, Graphics, Internet, Office, Sound, and Video. Clicking on a category opens it to display related programs and tools.

Administration and Preferences

Administration and Preferences displays the tools and applications that enable you configure and administer Linux Mint.

Places

The place menu displays the shortcuts for the following things:

*   Home

*   Desktop

*   Documents

*   Music

*   Pictures

*   Videos

*   Downloads

*   Connect to server

*   Mounted device

The descriptions of each item in the place menu are listed below:

Home: The home folder is the directory containing each user's personal files and configuration data. Typically, it is indicated by ~/ or /home/username/, where "username" is the user's name. Inside your home folder (/home/username/), you will find standard directories such as:

Desktop: Typically used for storing users document files.

Documents: Typically used for storing users document files.

Pictures, Videos, Music: Self-explanatory directories for respective media types.

Downloads: Where downloaded files are saved by default.

Connect to server: This dialog box contains a dropdown menu titled Type. This menu allows you to select the type of server you want to connect to. Options usually include:

*   SSH

*   FTP (File Transfer Protocol)

*   Windows Share

*   Custom Location: Allows you to specify a custom URI for connecting to other types of servers.

Mounted device: When you connect or mount a device, it usually displays here, and you can access and interact with these mounted devices.

Recent files: The Recent Files menu automatically displays files that you have recently accessed or opened.

Search Bar

On the top menu, you will find a search bar that allows users to quickly find and launch applications by typing keywords. It also allows you to search for a file in the list of recently opened files.

The search bar in the Linux Mint menu improves productivity by making it easier to find and access applications, settings, and, in some cases, files. It's an effective tool for browsing your system, especially as the number of installed programs and settings grows.

Favourite Bar

On the left side of the menu, you will notice a bar with favourite icons and System actions icons. By default, favourite icons include icons for the file manager, terminal, system settings, software manager, and web browser. However, you can add more icons of your choice by dragging and dropping.

System Actions

System Actions like logout, shutdown, and restart are also easily available through quick links in the favourite bar on the left side of the menu. Below is a description of each action.

*   Log out or switch user

![](image_rsrc4BJ.jpg)Mint provides you option to share your computer with other users. To let other users use your computer, either you press Logout or Switch user. When you pick Logout all your running application will close, on the other hand when you press Switch user all your applications will continue running, and everything will be same when you log back.

To Logout or Switch user, click button and then pick the option you want.

*   Lock

When you are away from your machine for a short period of time, it is recommended to lock your screen so nobody can use it in your absence. When the system screen is in a locked state, all the running applications will continue to run. To log back in, provide your login password to unlock the screen. The system also locks the screen automatically if you leave your computer for a specific time period.

To lock the screen manually, click the click the Lock ![](image_rsrc4BK.jpg) button. You can also use a keyboard shortcut to lock, press the Super + L key. To unlock, press ENTER key on the locked screen and provide your password.

*   Power off

![](image_rsrc4BM.jpg)To switch off your computer or to restart the whole computer, click the system menu on the left side of the menu, click Power Off ![](image_rsrc4BN.jpg)button. A dialog box will open, Select the required button.

*   Suspend

In the case of laptops, Linux Mint automatically changes the system to suspend mode on closing the laptop lid. In the suspended mode, the system uses very little power to save energy. All your applications keep running in suspend mode, but the screen and other non-essential parts of the computer switch off to save power. To change the system to suspend mode manually, click the Power Off button and pick the Suspend option.

Desktop

In Linux Mint, the desktop area performs multiple vital roles, making it a central and customizable component of the user interface.  Through the settings, users can change the desktop background to any number of pictures, solid colors, or slideshows. Users of Linux Mint can customize their experience by using themes that alter the panel, icons, window colors, desktop background, and more. It is possible for users to temporarily store files and quickly access apps and data by placing icons on the desktop.

![](image_rsrc4BP.jpg)

Desklets

Desklets are little programs, sometimes known as mini-applications, that are designed to carry out particular tasks or offer helpful data right on the desktop. They can be altered and configured to suit the preferences of the user and are similar to widgets or gadgets present in other operating systems. Some of the common desklets are:

*   Clock

*   Weather

*   System Monitor

*   Calendar

*   News Feeds

Working with windows

Linux Mint uses windows to display your running applications. This is one of way to run multiple tasks at same time. Whenever you launch any application it opens in new window. In this section we will explore windows.

Window Elements

![](image_rsrc4BR.jpg)

Title Bar: The title bar, located at the top of the window, often displays the application's name and has window management functions (minimize, maximize, close).

Menu Bar: The menu bar contains application-specific menus (File, Edit, View, etc.) that allow you to access program functionalities.

Content Area: The Content Area is where the application's main content is shown and where you interact with it.

Status Bar: Optional; displays information about the application's current status or progress.

Windows Management

Move: To move a window around the desktop, click and drag its title bar.

Resizing: To resize a window, click and drag its edges or corners.
Minimize, Maximize, and Close: Use the title bar buttons to control the window's visibility and behaviour.

![](image_rsrc4BS.jpg)Windows Selector view

When you have multiple applications running in various windows and wish to view all of them in order to select the relevant application window, you can utilize the windows selector view. To open Windows Peek View, right-click on the corner bar and pick "Show the window selector(scale)" from the context menu.

Click the desired application window to switch to that application. To close any running application window, hover over the window and click X button. 

Switch window

![](image_rsrc4BT.jpg)

You can switch the windows using key board. Press Alt key + Tab to open windows switcher. Keep holding the Alt key, release and press Tab key to cycle between open windows.  Shift-Alt-Tab is another shortcut you can use to navigate backward in the focused windows' history. Holding Alt and quickly pressing Tab allows you to use the left and right arrow keys to navigate in the desired direction. Using the scroll wheel while holding down the Tab key is a third technique.

Tile Windows (Snap Windows) ![](image_rsrc4BU.jpg)

To copy files or to compare the content of two windows, you can place two windows side-by-side. In Microsoft Windows, this feature is known as Windows Snap. To snap the window to the left side, press Super + left arrow on selected window, and to snap the window to the right side of the screen, select the window, press Super + right arrow key on the keyboard. To snap a window using the mouse, grab the title of the window and drag it to the left or right side until half of the screen is highlighted.

Settings![](image_rsrc4BV.jpg)

Click on Setting icon in the Mint menu will open settings windows for system and hardware. The settings panel is organized into categories. You can scroll the list of settings with mouse’s scroll wheel. Suppose you want to change the background of your desktop. Click background and select the wallpaper from the list of available wallpapers. To return to the settings window after modifying the desktop, click the back button in the top bar.

![](image_rsrc4BW.jpg)Top bar of the system setting tool also houses search button. Search button offers you to search anything related to settings. For example, to set the date and time, simply type "date" into the search box. The system will show you list of items related to date.

In conclusion, you need to understand how to use Linux Mint's desktop if you want to get the most out of it. It is crammed with helpful features and has an intuitive design. It is easily customizable to match your tastes and working style. Linux Mint guarantees a solid experience for daily work by placing a high emphasis on security and stability. For all your computer needs, the desktop environment of Linux Mint provides a dependable and flexible platform, regardless of your level of experience.

Chapter 5                  

Customizing the Desktop Environment

In Linux Mint, desktop customization is essential for enhancing user satisfaction and efficiency. Through the customization of themes, icons, and fonts, users can establish an aesthetically pleasing and cozy atmosphere that suits their tastes. Customization fosters creativity and individual expression while simultaneously enhancing accessibility and utility. Users can choose from a variety of easy layouts and configurations to maximize workflow productivity. Furthermore, preserving a uniform desktop experience across devices guarantees user-friendliness and comfort. All things considered, desktop personalization in Linux Mint makes computing more efficient, fun, and personalized for users of all ability levels. In this chapter, we shall discuss the following:

*   Themes

*   Icons

*   Fonts

*   Desktop Background

*   Desktop Effects

Themes

Themes in Linux Mint enable users to personalize the appearance of their desktop environment, making it more visually appealing and matched to their preferences. For the Cinnamon desktop environment, Linux Mint still keeps up its own theme repository. By giving users a variety of options to personalize their experience, these themes aim to improve the desktop's usefulness and aesthetic appeal. Below is a summary of the most recent Cinnamon themes that are available in Linux Mint:

Mint-Y Theme:

Mint-Y is the default theme in Linux Mint. It has a modern, minimalistic design that prioritizes aesthetics and practicality. The theme includes variations for controls, window borders, icons, and mouse pointers which are available in advanced settings.

Mint-X Theme

Linux Mint offers an additional theme option called Mint-X. Compared to Mint-Y, it has a more conventional appearance, providing a timeless appeal with delicate gradations and tints. Additional choices for controls, window borders, icons, and mouse pointers are also included in Mint-X.

In addition to these two themes, Linux Mint comes pre-installed with Adwaita and High Contrast, which are not specific to Linux Mint.

Here is an overview of how themes are managed in Linux Mint:

Change Theme

Click Settings in the menu.

In the settings window, locate and click on the "Themes" option.

On the Theme setting screen you have two modes simplified and advanced setting mode. In simplified mode, you can change the style, appearance, and color. The following is an explanation for each item on the screen:

![](image_rsrc4BX.jpg)

Style: You can select the desired theme using the drop-down menu.

Appearance: Appearance refers to the various visual styles and color schemes that can be applied to user interfaces.

Dark Theme: A dark theme often includes a dark backdrop with light-colored text and objects. Dark themes can be easier on the eyes, especially in low-light or nighttime settings.

Light theme: A light theme features a light background with dark text and elements. Light themes are more conventional and commonly utilized in many operating systems and applications. The great contrast between light backgrounds and black text/icons can improve reading, particularly in well-lit areas. 

Mixed Theme: A mixed or hybrid theme has elements from both dark and light themes. Provides a blend of the benefits of dark and light themes, responding to different user preferences.

Color: Determines the color of icons in the start menu, file manager, and other places.

Advanced settings

If you pick Advanced settings, you will have more detailed options for changing the appearance and feel of the desktop environment. Here is the explanation for each item:

Mouse Pointer: Changing the cursor theme allows you to add unique style to your desktop by choosing and using different cursor sets.

Application:  It manages the styling of programs' buttons, checkboxes, radio buttons, sliders, progress, bars, title bar, text fields, and other interaction elements.

Icons: It specifies the appearance of icons displayed on the desktop, file manager, menu, and shortcuts.

Desktop: It controls the appearance of the panel, mint menu, and other desktop components.

![](image_rsrc4BY.jpg)

Add New Theme

![](image_rsrc4BZ.jpg)

On the theme screen, select the Add/Remove tab. On this screen, select the theme you want to add, or use the search bar to find the desired theme. After selecting a theme, click the download icon on the right side of the theme to download and install it. Upon completion, you will notice a tick mark against the installed themes. You can now use this desktop theme in advanced settings.

Fonts

In Linux Mint Cinnamon, font selection involves personalizing typefaces for applications, system interfaces, and particular use cases in order to improve legibility and aesthetic appeal. By using the desktop environment's customization choices and comprehending the usage of fonts, you can create a comfortable and customized computing experience that suits your needs. The steps to change the fonts on your desktop environment are listed below:

Open the Mint menu and navigate to Preferences > Fonts Selection.

![](image_rsrc4C0.jpg)

Document fonts: Text within documents, including word processing documents, spreadsheets, presentations, and PDF files, is typically displayed using document fonts.

Monospace fonts: Frequently utilized in terminals, code editors, programming, and other programs. We normally use to change the terminal font.

Default font: Used to show text within the operating system and application user interfaces. It includes menus, dialog boxes, buttons, tooltips, and other interface elements.

Desktop font: Change the fonts of desktop components, such as shortcut icon text.

Desktop Background

You can easily customize your desktop environment by changing the wallpaper, sometimes referred to as the desktop background. Here's how to control and modify Linux Mint's desktop background:

*   Right-click on the empty area on your desktop, and it will show the context menu.

*   From the context menu, select "Change Desktop Background." This will open the Backgrounds window.

*   Click on a thumbnail to choose a pre-installed wallpaper from the list.

Adding Custom Wallpaper

To add your own image or another downloaded image as a wallpaper:

![](image_rsrc4C1.jpg)

1.  Add The folder: Click the "+" button and navigate to the folder containing the image/images you want to use as your backdrop.

2.  Select the Background: After adding a folder, you will see the photographs in the left pane. Select the image you want to use as your desktop background.

Use the file manager to apply custom wallpaper

The other option is to utilize the file manager. Open the file manager, navigate to the desired .jpg or .png file, right-click it, and select "Set as wallpaper".

![](image_rsrc4C2.jpg)

Desktop Effects

The term "desktop effects" describes visual additions and animations that raise the usability and aesthetic appeal of the user interface. These effects, which improve user interaction and experience, can be anything from faint movements to prominent visual components. To adjust the desktop effects precisely:

*   Launch the Mint menu.

*   Choose the Effects from the Preference category.

![](image_rsrc4C3.jpg)

Every category is self-explanatory and can be customized to your preference.

By personalizing your Linux Mint desktop, you may design a workspace that is both useful and unique. We looked at how changing desktop effects, wallpapers, themes, and fonts improves both appearance and usability in this chapter. You may easily customize every element of your desktop environment to fit your style and workflow preferences by exploring the additional customization options offered by Linux Mint.

Managing desklets

You can add useful or aesthetically pleasing items to your desktop environment in Linux Mint by adding desklets, or desktop widgets. Here's a step-by-step tutorial for customizing your Linux Mint desktop with desklets:

To open the Desklets Manager, click the Mint menu button and then select Desklets from the Preferences category.

Add Desklet

The Desklets Manager window displays a list of pre-installed desklets. To add Desklets to your desktop, select the desklet you want to add and then click the "+" button.

Remove Desklet

To remove a desklet, go to the Desklets Manager and choose the desklet you wish to remove, then click the "-" button.

![](image_rsrc4C4.jpg)

Install Desklet

To install additional, click the "Download" tab, which will display a list of desklets available for download. You can also search for the desklet you want to download and install. To download and install a desklet, select it and then tap the download icon next to it.

![](image_rsrc4C5.jpg)

Once installed, it will be displayed under the Manage tab

In conclusion, changing your desktop environment in Linux Mint provides numerous options for improving the aesthetics and functionality of your workspace. By experimenting with different themes, icons, and fonts, you may design a configuration that not only reflects your own style but also increases your productivity.

Chapter 6                  

Filesystem Hierarchy

What is Filesystem?

A filesystem is a way for operating systems to organize and store data on storage devices including hard drives, solid-state drives (SSDs), USB drives, and optical discs. It offers an organized approach to managing files, folders, and the metadata associated with them. Here are some important components and concepts linked to filesystems:

1.  Files

2.  Directories(Folder)

3.  Metadata

4.  Filesystem types

5.  Partitioning

6.  Formatting

7.  Mounting and Unmounting

8.  Access Control

Filesystem and FHS

FHS is a set of standards for the structure and organization of files and directories in Unix-like operating systems. It standardizes the filesystem hierarchy layout, ensuring consistency between Unix and Unix-like systems. FHS provides the usual root folders, which include /bin, /boot, /etc, /home, /usr, /var, and others.

The FHS directory structure begins with the / (root) directory. Even if the files and directories are stored on different physical or virtual devices, they all appear under the root directory.

FHS defines the directory structure that most Linux distributions use. According to FHS, a program written for one Linux distribution can be easily ported to another. This ensures that only minor or no changes are required. Assume you have a program that stores binary files in the /opt directory. If there is no standard, you must either create the directory or change the program when migrating to another Linux distribution. FHS is also useful for system administration because it eliminates the need to remember the location of configuration and log files if you have multiple Linux distributions in your data center.

File system concepts

Files

*   The fundamental units of data storage within a filesystem are files.

*   Files can include a variety of data types, including text, photos, applications, and documents.

*   Within each directory, each file is identified by a unique name.

Directory (folders)

A directory, sometimes referred to as a folder, is a kind of file used by computers' filesystems to arrange and store other files and directories in a hierarchical structure. Modern operating systems must have directories in order to put relevant files together for easier management and organization. Key information regarding directories is as follows:

*   Containers for grouping and organizing related files.

*   A hierarchical tree-like structure can be formed by directories holding both files and other directories.

Linux Mint has been acknowledged for adhering to the Filesystem Hierarchy Standard (FHS), which specifies the layout and contents of the Linux file system directory. This means that critical folders such as /bin, /etc, /home, /lib, /opt, /sbin, /usr, and /var are used as specified by the FHS rules.

The description of each directory is as follows:

| Directory | Description |
| / | Top directory, all other directories are sub directories of root file system. |
| /bin | This directory primarily contains links (shortcuts) to /usr/bin. Also included are executable files and commands required by both system administrators and normal users. |
| /boot | Files for system boot. |
| /dev | Device driver files. |
| /etc | Configuration files. |
| /home | All users' home directories except the root user. |
| /lib | Libraries and kernel modules |
| /lib64 | 64 bit libraries |
| /media | Mount point for external storage devices. |
| /mnt | Mount point for user mounts. |
| /opt | Third party software. |
| /proc | Temp directory for all running processes. |
| /root | Home directory of root user. |
| /run | Temp file system used by running processes. |
| /sbin | Contains mostly symbolic links to /usr/sbin directory for system executable files. |
| /srv | Services related data. |
| /sys | Symbolic link to the kernel source tree. |
| /tmp | Temporary files. |
| /usr | Contains all the user binaries, their documentation, libraries, header files, etc. |
| /var | Variable files such as logs. |

Metadata

Under Linux, the information that describes the properties of files and directories is referred to as metadata. Typical metadata consists of:

File Permissions: Indicates who has the ability to run, write, and read the file.

Ownership: Identifies the individual or organization in possession of the file.

Timestamps: Indicate the creation, modification, and access dates of the file.

File Type: Identifies the type of file, such as regular, directory, symbolic link, etc.

Size: The file's size expressed in bytes.

Extended Attributes: Additional metadata that can be added to a file to provide information beyond the standard attributes.

Directory (Folder) concepts

Home folder

In a multi-user environment, every user has his own home folder. The home folder holds the user’s personnel files, including documents, pictures, music, and videos.

Path

The "path" is the current location of the file or directory. A path to a file is made up of / and alphanumeric characters. You can specify the path in two ways: relative path and absolute path. 

Absolute Path-name

An absolute path specifies the location of a file or directory relative to the root directory (/). To represent any directory using an absolute path, begin at the root directory (/) and work your way down. After each directory name, add a slash (/) (last one is optional)

To access a file contact.txt in the Documents directory, we will write  /home/shiv/Documents/contact.txt.

Relative path

Relative path is a shortcut that uses the current or parent directory as a reference and specifies the path relative to it. Relative paths use single or double dots.  The current directory is represented by a . (single dot), while the parent directory is represented by ..(two dots).

Files and directories are key components of every file system, with files storing data and directories organizing it in a hierarchical manner. Mastering their management, whether through GUI tools or command-line commands, enables more efficient data handling and system navigation. Understanding paths grants you more control over your files and directories. In the following chapters, we will look at how to manage files and directories in both GUI and command-line modes.

Chapter 7                  

Managing files and Directories Using File Manager

The file manager provides a graphical interface for exploring and managing files and directories. Nemo is Linux Mint's default file manager. Nemo is a fork of the GNOME Files file manager that is designed to be more feature-rich and user-friendly under the Cinnamon desktop environment. Here's a tutorial on how to navigate the filesystem with Nemo.

Opening File Manager

Click the file manager icon in the panel or on the left favourite bar of the Mint menu. Alternatively, you can find it in the mint menu by searching for "files." By default, Nemo opens in your home directory (/home/username).

Understanding the Nemo UI

Understanding the Nemo UI will help you navigate and manage files more effectively. Below are the some of the main components of Nemo File manager:

*   Toolbar

*   Side Bar

*   Side Bar

*   Main Area

*   Context Menu

*   Status Bar

*   Tabs (Optional)

![](image_rsrc4C6.jpg)

Toolbar

Back/Forward Buttons: Navigate backward or forward through previously visited directories.

Up Button: The Up Button moves you up one level in the directory hierarchy.

Location Bar: The location bar shows the current directory path and is situated beneath the toolbar. To quickly navigate to parent directories or any other directory along the path, just click on any portion of the path. The toggle location button, which is located next to the location bar, allows you to manually enter or modify the location.

Location Toggle button: The Location Toggle button allows users to switch between two options for displaying the path or location bar in the file manager window: an editable file path or a clickable breadcrumb trail.

Search Bar: The system will open the search bar when you click the search button. enables name-based file and folder searches.

View Options: Change the layout (icons, list, compact) and sorting options.

Side Bar

Nemo's sidebar offers quick access to frequently used devices and folders. The following elements are included in the sidebar:

Places: Offers quick access to your Desktop, Documents, Downloads, Music, Images, Videos, and more.

Devices: Displays the external attached storage devices, such as USB drives and hard drives.

Network: Offers access to linked servers and network locations.
Recent: Shows directories and files that have recently been accessed.

Trash: Use this shortcut to view and handle files that have been deleted.

File systems: The root directory and other locations are normally accessible through the "File Systems" section.

Main Area

The main area is the central region of the file manager window that displays the contents of the current directory. This section is essential for browsing, organizing, and interacting with files and folders. Files and folders can be displayed in icon/grid, list view, or compact view.

Icon/Grid View: Shows files and folders as icons or thumbnails.
List View: Provides a comprehensive list format of files and folders with columns for name, size, type, and modification date.

Compact View: provides a more compact layout than the list view and normal icons/grid view.

Context Menu

A context menu, also called a right-click menu, is a user interface element that appears when a user right-clicks on an item. It displays a list of actions or commands connected to the specified object or location, giving you easy access to frequently used functions.

A context menu including the following options appears when you right-click on a file or folder in the file manager:

Open: This command opens a file or folder.

Cut/Copy/Paste: Move and duplicate files and folders.

Rename: Modifies the name of the specified file or folder.

Delete: Sends the file or folder to the Trash.

Properties: Displays detailed information about a file or folder, such as permissions and metadata.

Other Options: Shows additional options based on the content that is right-clicked, such as compress, open terminal, create new folder, create document, etc.

Tabs

Nemo (File manager) supports tabbed navigation, which means you can browse numerous directories in independent tabs within the same window. This capability allows users to navigate between directories without launching additional file manager windows.

Status Bar

The status bar at the bottom of the Nemo window displays information about the selected files and folders.

*   Displays the total number of files and folders in the current directory.

*   Displays the overall size of the selected files as well as the available disk space.

Side bar view options: Provides controls for changing the side bar view to tree view, places view, or show/hide side bar.

Zoom Bar: Provides a scroll bar for adjusting the zoon level of the main area.

Basic Operations with Nemo

Opening file or folder

When you double-click on a file, it opens in the default program for that file type. Double-clicking or using the Enter key (on the selected file) will allow you to open the folder and view its contents.

Select file or folder

Simply clicking on any file or folder allows you to select it. Hold down the Ctrl key on your keyboard to select multiple files or directories.

Copying and Moving Files

There are multiple ways to copy/move files

Using Context Menu

Select the file(s) or folder(s), then right-click and choose "Copy" or "Move" from the context menu. Navigate to the destination folder, then right-click and select "Paste".

Copy using keyboard.

1.  Select the file or folder you want copy.

2.  Press the Ctrl + C keys simultaneously.

3.  Navigate to the desired location.

4.  To paste, press the Ctrl + V keyboard shortcut.

Move using keyboard

1.  Select the file or folder you want move.

2.  Press the Ctrl + X keys simultaneously.

3.  Navigate to the desired location.

4.  To paste, press the Ctrl + V keyboard shortcut.

Drag and drop to copy or move files

To copy a file from one source to another using drag and drop use following procedure:

1.  Navigate to the folder containing the file you want to copy (source folder).

2.  Navigate to the target folder where you wish to copy the file by opening a new window.

3.  Position both windows side by side.

4.  Go to the source window.

5.  Click and hold the left mouse button while pressing the Ctrl key on the file or folder you wish to copy. Drag the file or folder to the target window, then release both buttons to copy it. If you wish to move a folder, don't use the Ctrl key when dragging it.

![](image_rsrc4C7.jpg)

Rename a file or folder

To change the name of a file or folder, right-click the folder or file and select Rename from the context menu. Rename the file or folder using the keyboard; select the file or folder and press the F2 key on the keyboard.

Write the new name of the file or folder and press  Enter key.![](image_rsrc4C8.jpg)

Delete

If the file or folder is no longer required, you can delete it.

Select the file or folder to delete.

Right click on the mouse and select Move to Trash from the context menu.

Or

Press Delete key from the keyboard.

The files will be moved to the trash. If you accidentally delete a file or folder, it can be easily restored from the trash.

Restoring a file from the Trash

Restoring a file from the trash is a simple operation. Click the Trash icon on your desktop or in the file manager's sidebar. Go through the Trash to find the file or folder you wish to restore. Right-click the file or folder and then pick Restore from the context menu.

Empty Trash

To reclaim the space used by deleted files:

1.  Right click on the trash icon on the Side bar.

2.  Select Empty Trash from the context menu.

3.  Press Empty Trash on the confirmation popup.

To permanently delete the file without moving it to the trash

1.  Select the file or folder you want to delete.

2.  On your keyboard, hold down the Shift key while pressing the Delete key.

It will prompt for confirmation. Press the Delete button. ![](image_rsrc4C9.jpg)

Sorting and Viewing Options

The file manager displays files and folders in icon view by default. To switch from icon view to list view or compact view, use the view buttons on the file manager's Tool bar.  

You can also use the keyboard commands Ctrl + 1 to go to icon view, Ctrl + 2 for list view, and Ctrl + 3 to get to compact view.

To sort the list of files and folders.

1.  Toggle the view to a list view.

2.  Click on the heading of the column to sort the list. Press the same heading again to sort the view in reverse order.

![](image_rsrc4CA.jpg)

In the list view, when you right-click a column, the view options popup menu appears, allowing you to select the Visible Columns.

![](image_rsrc4CB.jpg)

In Linux Mint, using Nemo to navigate the filesystem makes it easier to manage files and folders. It lets you conduct basic file operations, search for files, and personalize the file manager to your liking. Mastering these navigation skills can help you work more productively and efficiently with files in Linux Mint.

Chapter 8                  

Using External Storage Devices

Using external storage devices via the graphical user interface (GUI) in Linux Mint is typically straightforward. Here’s a guide on how to handle external storage devices using the GUI tools provided by Linux Mint:

Plug and play

Attach an external storage device to a USB port on your computer, such as an SD card, external hard drive, or USB drive. Linux often mounts external drives automatically; you should receive a notification and see the device on your desktop. You can see it in the sidebar if you are in the file manager. Click on it to access its contents. ![](image_rsrc4CC.jpg)

Unmounting the Device

To safely remove a USB device from a Linux system, make sure it is unmounted properly before physically unplugging it. This prevents data loss and file system corruption. Here's how to accomplish it:

Right-click on the device icon in file manager and select "Eject" or "Unmount". You can also unmount by clicking on the small mount icon next to the mounted device.

Another option is to unmount the USB device from the panel by right-clicking on the removable device icon and selecting Remove "Removable drives". Once you get the confirmation message, you can safely unplug the USB device.

![](image_rsrc4CD.jpg)

Format USB drive

A USB drive can be made usable by formatting it, which removes existing data or installs a new file system. For ordinary use, you can use a file system like FAT32, or for Linux, ext4\. The drive's performance is enhanced and any problems are resolved through formatting. Additionally, it clears the disk of all previous data, leaving it empty and ready for usage.

Using the GUI

There are several ways to format a USB storage drive, and you may use either a GUI or a command line interface. In this method, we will use the USB Stick Formatter(MintStick), a graphical application offered by Linux Mint.

![](image_rsrc4CE.jpg)

1.  Plug your USB drive into your computer.

2.  Start the USB stick formatter tool from the mint menu, located in the Accessories category.

3.  The USB stick formatter window will display a list of storage devices. Select your USB stick from the list.

4.  Select the preferred file system (e.g., FAT32 or ext4).

5.  Change the Volume Label if required.

6.  Click on the “Format” button.

7.  Confirm the action by entering the authentication password and pressing Authenticate. This will delete all data from the USB stick and format it with the specified file system.

8.  On completion, you will receive a confirmation window.

Writing ISO image

An ISO image is a single file that contains a complete copy of the data on an optical disk, such as a CD, DVD, or Blu-ray, including the file system and all files and directories. The term "ISO" refers to the ISO 9660 file system, which is used with DVD media and CD-ROM.

An ISO image of a Linux OS is a file that contains a complete copy of the Linux operating system, including installation files, settings, and, in many cases, a bootable environment.

The Linux Mint includes a program called USB Image Creator. It is used to convert an ISO image into a bootable USB device. This is helpful for running Linux Mint in a live session straight from the USB stick or for installing it on a computer.

![](image_rsrc4CF.jpg)

Here's how to use USB Image Creator:

1.  Download the image file.

2.  Insert your USB drive.

3.  Open the USB Image Creator from the Mint Menu’s Accessories category.

4.  Select the ISO file.

5.  Select the USB drive you wish to use. Be careful to choose the correct drive, as all data on it will be erased during the process.

6.  Press the write button.

7.  You will get Authentication window and warning about data deletion. Press Authenticate to begin the process of transferring the ISO to the USB device in bootable format (if the ISO file is bootable).

8.  Wait for the process to complete. The time required will vary according to the size of the image and the speed of your USB device. Once the process is finished, your USB drive should be ready for use.

Using external storage devices is simple and intuitive in Linux Mint. Files may be accessed quickly with the file manager thanks to the automatic detection and mounting of devices like USB drives and external hard drives. All things considered, Linux Mint's interaction with external storage devices is smooth, giving you both control and ease when it comes to handling your data.

Chapter 9                  

Using The Terminal

The terminal is an application that allows you to access the Command-Line Interface (CLI) and interact with your system by typing text-based commands, which is faster and more efficient than using a mouse. It allows you to manage files, launch applications, and complete tasks without using complex graphical interfaces. The command line is important for troubleshooting, remote system access, and script-based automation of repetitive activities. It's also an excellent method to learn more about your computer and enhance your technical skills. The terminal and virtual terminals are the two primary methods for gaining access to command-line interfaces.

Terminal ![](image_rsrc4CG.jpg)

With the terminal, you can perform commands and effectively administer your system from within your graphical desktop environment. To open it, use the Ctrl + Alt + T shortcut, search for "Terminal" in the Mint Menu, or right-click in the file manager and select "Open Terminal Here."

Virtual Terminal

A virtual terminal is another way to access the command line interface. The virtual terminal provides several command-line sessions that are independent of the graphical user interface. It enables users to switch between command-line instances, which is beneficial for multitasking, system administration, and troubleshooting. Virtual terminals come in handy when the graphical environment is unresponsive for carrying out various tasks or troubleshooting problems. ![](image_rsrc4CH.jpg)

Ctrl + Alt + F1 through F6 can be used to access virtual terminals. Ctrl + Alt + F7 (or F8) can be used to return to the Graphical desktop.

Tips and tricks

Here are a few helpful tips for utilizing the terminal effectively:

Tab Completion: When you press Tab while typing a command or file name, it will autocomplete if there is just one option or display a list of possible completions. This can save time and prevent mistakes.

Command History: Use the Up and Down arrow keys to navigate through previously typed commands. This allows you to repeat or alter commands without having to type them again.

History Search: To search through your command history, use Ctrl + R and begin typing a portion of the command. Press Ctrl + R again to cycle through matches.

Using terminal remotely

A remote terminal allows you to control another computer via the network or internet as if you were sitting directly in front of it. The most common tool for this is SSH (Secure Shell), which allows you to safely access to a remote machine and run commands, manage files, and perform administrative functions. Telnet is another option, although it is less secure and hence not advised for critical jobs. You can use these tools to traverse the file system, modify documents, and even transfer data between machines, all from your own location. Not only Linux machines, you can also use your Windows 10/11 computer to manage other systems remotely using SSH or telnet. SSH is favored for security since it encrypts data and protects it from prying eyes. This configuration is ideal for remotely managing servers, developing software, and providing technical support. ![](image_rsrc4CJ.jpg)

You can use the PuTTY program on your Windows system to connect to any Linux machine remotely.  PuTTY is a robust, open-source terminal emulator created by Simon Tatham. It supports a variety of network protocols, including SSH (Secure Shell), Telnet, SCP (Secure Copy Protocol), and raw socket connections, making it an important tool for system administrators, developers, and IT professionals. The software allows users to connect securely to remote servers, offering a command-line interface to execute commands, manage files, and perform system administration duties from a distance.

In conclusion, learning the Linux Mint terminal is an effective method to maximize the capabilities of your system. The terminal offers a simple and effective way to manage files, execute commands, and customize your environment. In the following chapter, we'll look at how to use the terminal to explore the system.

Chapter 10              

Navigating Files and Directories Using Terminal

In this lesson, we'll look at Linux commands for manipulating files and directories. Navigating and manipulating files and directories via the command line is an essential ability in Linux that gives users complete control over their file system. This guide will teach you through the important commands for reading, creating, and changing files and directories. Whether you're a beginner or seeking to brush up on your skills, mastering these terminal commands will boost your efficiency and confidence in managing your Linux system. Mastering these commands, which range from file listing to document editing, will lay the groundwork for advanced tasks.

To access files and directories with command-line tools, first open the terminal windows described in the last chapter and use the following commands:

cd

The command "cd" stands for "change directory." It is utilized to move from the current directory to the target directory.

Syntax

cd directory_name

Example

cd john

To move one level up

cd ..      

To move two levels up

cd ../..    

Move to the home directory

To navigate to a user's home directory, use the cd (change directory) command. There are several ways to accomplish this:

Using no argument with cd command

cd

Using ~ (tilde) symbol

cd ~

Using $HOME environment variable

cd $HOME

After running one of these commands, you'll be in your home directory, which is usually /home/username.

Navigate to a sub-directory inside your home directory

You can use both ~ and $HOME to navigate within your home directory.

cd ~/Downloads/

This command will move you to the Download folder in the user's home directory.

To navigate to the same Download subdirectory using $HOME

cd $HOME/Downloads/

Switch to another user’s home directory.

You can easily switch from your current working directory to another user's home directory depending on your current login privileges.

cd ~john

Change to the root directory

Change directly from the current working directory to the root directory

cd /

Switch to the previous directory.

cd -

Assume you are in the /etc directory and have switched to the /tmp directory. If you type cd -, you will be directed back to the /etc directory.

Changing directory with relative path

A relative path is a way to specify the location of a file or directory relative to your current working directory, rather than from the root of the filesystem.

$ pwd

/home/shiv

$ cd Documents                   

$ pwd

/home/shiv/Documents   

Changing directory with absolute path

An absolute path specifies the exact position of a file or directory in the filesystem, beginning with the root directory.

$ pwd

/home/shiv

$ cd /home/shiv/Documents

$ pwd

/home/shiv/Documents

ls

The ls command is used to display a folder's contents. It will display a list of all the files and directories in the current or specified folder.

Listing file and directory with permissions

The ls -l command returns a thorough, long-format list of files and directories, including file permissions, ownership, size, and modification time. It is a helpful tool for obtaining a thorough picture of the contents and properties of files in a directory.

Syntax

ls -l

Example![](image_rsrc4CK.jpg)

Listing files and directories in a human-readable format

The ls -lh command displays files and directories in a comprehensive, human-readable format. The -l option provides detailed information about each file, whereas -h format file sizes in a more understandable manner, making it easier to read file sizes at a glance.

ls -lh

Listing all files and directories, including hidden files

The ls -a command displays a list of all files and folders in the current directory, including hidden ones. By default, ls displays only non-hidden files and directories; however, with the -a option, it includes those that begin with a dot (.), which are considered hidden

ls -a

Recursively listing files and directories

The ls -R command displays a recursive list of the current directory and all of its subdirectories. This means that it shows files and folders not only in the selected directory, but also in every directory and subdirectory below it.

ls -R

Display ls command help page

ls --help

pwd

The pwd command is an abbreviation for (print working directory). It displays the user's current working directory or location. It displays the absolute path, which is the full path from the root / directory.

Syntax

pwd

mkdir

You can create your own directory with the mkdir command.

Syntax

mkdir directory_name

Example

mkdir john

To create multiple directories

Syntax

mkdir directory1 directory2 directory3

Example

mkdir dir1 dir2 dir3

Add a directory and its subdirectory.

The -p option in the mkdir command stands for "parents" and allows you to create a directory together with any required parent directories that do not already exist. This is very useful when you wish to create a nested directory structure with a single command.

Syntax

mkdir -p directory/subdirectory

Example

mkdir -p development/task1

This example creates the development directory and the task1 subdirectory within it.

rmdir

To delete a directory from your system, use the rmdir command.

Syntax

rmdir directoy_name

Example

rmdir john

Note: The rmdir command will only work if the directory is empty. If the directory contains files or other directories, the command will fail and output an error.

Delete the directory and its subdirectory

A directory and its subdirectory will be deleted simultaneously by this command, but only if they are empty. This command allows for a more streamlined cleanup of nested empty directories.

rmdir -p development/task1

mv

The mv command is a useful tool for managing files and directories. It enables you to move and rename files and directories efficiently.

To move file from one directory to another location

Syntax

mv source destination

Example

 mv file1.txt /home/shiv/

Renaming files or directories

The mv command is commonly used to move files, but it can also be used to rename folders and files.

Syntax

mv oldfoldername newfoldername

Example

mv development development1

rm

For the removal of files and directories, the rm command is an effective tool. It's flexible, but you have to exercise caution when using options like -r for recursive removal and -f for forcible deletion.

Remove file

To delete (remove) a file or directory in Linux, use the rm command.

Syntax

rm filename

Example

 rm biodata.txt

Remove multiple files

Syntax

rm file1 file2 ...

Example

 rm biodata.txt happy.txt

Remove directories

Use the -r flag to remove directories and their contents recursively.

Syntax

rm -r directory1 directory2

Example

 rm -r dir1 dir2

Force remove (Ignore confirmation prompts)

Use the -f flag to override any confirmation prompts.

Syntax

rm -f file1 file2 ...

Example

rm -f file1.txt file2.txt

Remove files recursively and forcefully

Use this command with caution, as it will delete files and directories recursively without prompting.

Syntax

rm -rf directory

Example

rm -rf dir1

touch

The touch command is used to create new empty files or to change the timestamp on existing files.

Create a new empty file

Syntax

touch filename

Example

touch file1.txt

Update timestamp of an existing file

Syntax

touch filename

Example

touch myfile.txt

Viewing and Editing Files

Viewing and modifying files from the terminal is an essential ability in Linux. Here is a detailed overview to the various commands and tools available in practically all Linux flavors for viewing and editing files:

Cat

The cat command is used to view, concatenate, and create files. Its simplicity makes it perfect for swiftly reading file contents or consolidating multiple files into a single one.

Display content of file.

To display the contents of a file using cat command.

Syntax

cat filename

Example

cat example.txt

View line number

Appends line numbers to the output, which is useful for debugging or reviewing large files.

Syntax

cat -n filename

Example

cat –n example.txt

Concatenate multiple files

Syntax

cat file1 file2

Example

cat example1.txt example2.txt

Displays the contents of example1.txt followed by example2.txt.

Redirect output to another file

Syntax

cat file1 > file2

cat example1.txt > newfile.txt

This command copies the contents of example1.txt to newfile.txt, overwriting newfile.txt if it already exists.

Append output to another file

Syntax

cat file1 >> file2

cat  example1.txt >> newfile.txt

This command appends the contents of example1.txt to newfile.txt.

Less

The less command allows you to view file contents page by page.

Syntax

less filename

Example

less example.txt

Here are some basic navigation commands you can use in less command output:

Scroll Down: Use the Down Arrow key or j to navigate down one line at a time. To move down one page at a time, use Space or F.

Scroll Up: Use the Up Arrow key or k to advance one line at a time. Press b or Page Up to advance one page at a time.

Forward Search: hit /, then type your search word and hit Enter. Use n to go on to the next occurrence of the search word.
Search backwards: hit ?, input your search phrase, and then hit Enter. Use N to return to the previous occurrence of the search word.

Head

The head command displays the beginning of a file or input data. By default, it displays the first ten lines, but you can change this. It is handy for fast previewing the beginning of files or data streams.

Syntax

head filename

Example

head example.txt

Specify the number of lines

head –n 20 example.txt

Shows the first 20 lines. Replace 20 with the desired number of lines.

Tail

The tail command displays the end of a file or data stream. It's especially beneficial when monitoring logs or huge files and need to view the most recent items.  By default, tail shows the last 10 lines of a file, but this can be customized.

Syntax

tail filename

Example

tail example.txt

Specify the number of lines

You can specify the number of lines of file to display with the -n option.

Syntax

tail –n <n> filename

Example

tail –n 20 example.txt

Displays the last 20 lines of the example.txt

Real-time monitoring

The tail command with the -f option continually outputs new lines added to the end of a file. This is useful for monitoring log files or other files where content is dynamically appended.

Syntax

tail –f filename

Example

tail –f example.txt

Aside from these commands, Linux has a number of text editors for editing files, the most popular of which are nano and vi.

In conclusion, Command-line tools are essential for examining files and directories in Linux because of their efficiency, flexibility, and power. They offer exact control over file management, allowing users to navigate, manipulate, and query files fast.

Chapter 11              

Using sudo for Elevated Access

The sudo (SuperUser DO) command allows you to access restricted files and operations. By default, Linux blocks access to certain system components in order to protect sensitive files. The sudo command allows you to run applications with another user's security rights (by default, as the superuser). It asks for your personal password and confirms your command request by verifying a file called sudoers that the system administrator has configured. It is a method that allows you to delegate some administrative responsibilities to less privileged users without providing the administrator's password.

The sudo command is critical for conducting administrative activities safely because it allows users to run commands with superuser capabilities. It ensures that only certain commands are executed with elevated permissions, lowering the possibility of unintended system changes. Sudo logs all elevated commands, which ensures accountability and transparency. It streamlines system administration by allowing users to complete important operations without having to switch to the root account. Overall, sudo improves security and efficiency, making it an essential tool for successful Linux Mint administration.

Example of a privilege command that modifies system configuration:

Install a package

sudo apt install gzip   

Change hostname

sudo hostnamectl set-hostname host2021

Run command as different user.

To execute a command as a different user, use sudo with the -u argument. It enables you to run commands with privileges of another user account, which is useful for tasks that require certain user permissions without switching accounts completely.

Syntax

sudo -u user command

Example

sudo -u user2 hostnamectl

Use sudo in interactive mode

The sudo with -i option opens an interactive shell with root privileges. It starts a new shell session as the root user, allowing you to execute administrative actions without having to prefix each one with sudo.

sudo -i

Example

![](image_rsrc4CM.jpg)

Changing the sudo Configuration

sudo's configuration is saved in the /etc/sudoers file. The sudoers file is a useful tool for controlling administrative access. Properly configuring and managing it helps ensure that users have the appropriate level of access while maintaining system security. To change the sudo configuration, use the visudo command.

sudo visudo

It essentially launches the vi or nano editor and modifies the /etc/sudoers file. The visudo command must be run by a user with administrative rights.

sudo visudo

The /etc/sudoers file contains a list of users and the commands that they can execute.

user host=(users) [NOPASSWORD:]commands

Example

%operators​ localhost = (apache) /usr/sbin/

The sudo command is essential for managing system privileges in Linux Mint, since it provides a secure means to do administrative duties without giving full-time root access. Sudo improves security and accountability by allowing users to precisely control the commands they can run with elevated capabilities. Its setting via the sudoers file guarantees that permissions are properly maintained and logged. Mastery of sudo is required for effective system administration, ensuring that activities are completed safely and efficiently. Overall, sudo is a critical component of secure and productive Linux management.

Chapter 12              

Package Management

Package management is a collection of Linux utilities for installing, updating, configuring, and uninstalling software packages from a Linux-based operating system. These tools assist users and administrators in managing the software ecosystem on their computers efficiently. The majority of manage management tools assist in solving dependencies. Software dependencies are other software components or libraries that a software package requires to perform properly. Not only that, package management tools also help in the following ways:

Dependency Tracking: Package management technologies keep dependency databases to help you quickly resolve dependencies when installing, updating, or uninstalling packages.

Version Compatibility: Manages version compatibility between packages and dependencies.

Conflict Resolution: Address any conflicts that may emerge when multiple packages request different versions of the same dependency.

Dependency Removal: When you remove a package, the package management determines whether any other packages rely on it. If not, it removes the package and any dependencies that are no longer required.

Examples of package management systems:

*   APT and DPKG are used in Debian based distributions such as Ubuntu, Linux Mint, MX Linux, and others as deb package extensions.

*   RPM and YUM/DNF are used in Red Hat based distributions such as Fedora, CentOS, and Oracle Linux. It employs the .rpm package.

*   Pacman is used in Arch Linux and its derivatives.

*   Portage is Gentoo Linux's package management system. It employs a source-based package management method.

*   ZYpp is the package management library used by SUSE Linux distributions including openSUSE and SUSE Linux Enterprise.

The features, capabilities, and Linux distributions that these package management solutions work with may differ, but their common goal is to simplify the handling of software packages on Linux machines.

Advanced Packaging Tool

APT is the package manager for Linux Mint and other Debian based variants. It's an extremely useful application for installing, upgrading, and managing software packages on your system. APT allows users to effortlessly install software from the Linux Mint repositories, which are a massive collection of packages managed by the Linux Mint, Ubuntu and Debian community. APT also manages package dependencies, ensuring that all required components are installed when installing new applications. APT uses .deb files as a package format. The APT databases are normally located at  /var/lib/apt/. The repositories are defined in the  /etc/apt/sources.list and /etc/apt/sources.list.d/  .

Here's a brief summary of APT main features and aspects:

*   Package Management: APT command-line interface allows users to install, uninstall, and update packages with simple commands.

*   Repositories: APT is configured to access Linux Mint, Ubuntu and Debian by default, allowing users to simply install packages from the official repositories. It is also possible to use custom repositories.

*   Dependency Resolution: APT includes a sophisticated mechanism for automatically handling dependencies when installing or deleting packages.

*   Transaction Safety: APT provides a powerful transactional mechanism that helps to prevent system corruption and ensures that package installations and upgrades are dependable and secure.

*   Configuration Files: APT uses a straightforward system to manage configuration files, enabling package upgrades while preserving any previously made tweaks.

Package Extension

Package files in Linux Mint normally have the .deb extension. This extension indicates that the package is a Debain based package. Packages for Debian are frequently saved in repositories, which are collections of packages that can be found online or on physical media like CD-ROMs. Typically, packages come in a pre-compiled binary format, which makes installation simple and eliminates the need to assemble any software. A .deb file typically includes:

Control files: The package's name, version, dependencies, maintainer details, and installation scripts are all described in the control and md5sums files.

Data archive: Holds the actual files to be installed on the system, such as configuration files, libraries, binaries, and any other resources needed by the package.

Repository
A repository is a collection of Linux software that may be present locally or remotely. The repository can be used to either install new software or update existing applications. The list and location of the repository can be found in the /etc/apt/sources.list file, or they can be created in the /etc/apt/sources.list.d directory. To add a repository, add an entry to /etc/apt/sources.list; one source per line.

Example

deb http://packages.linuxmint.com virginia main upstream import backport #id:linuxmint_main

deb http://archive.ubuntu.com/ubuntu jammy main restricted universe multiverse

deb http://archive.ubuntu.com/ubuntu jammy-updates main restricted universe multiverse

deb http://archive.ubuntu.com/ubuntu jammy-backports main restricted universe multiverse

/etc/apt/sources.list.d
To add new repositories, create files in the /etc/apt/sources.list.d directory. The format of files in /etc/apt/sources.list.d is the same as the sources.list file, and the file names must finish with .list.

Flatpak

Sometimes, installing extra software that isn't available in deb format is necessary to satisfy particular demands and requirements. Here's where Flatpak's universal packaging structure comes in handy, making it simple to install and use apps on Linux. With the use of the cross-distribution framework Flatpak, developers can bundle programs together with their dependencies so that they can be installed and used on many Linux distributions.

It is also known as "Linux application sandboxing" because it creates a secure and isolated environment for apps to execute, akin to virtualization but without the overhead of a full virtual machine. Linux Mint supports Flatpak, making it easier to access a wide range of applications not available in the traditional package repositories.

FlatHub

Flathub is a key repository for Flatpak applications, offering a centralized platform to access a diverse array of software for Linux distributions. It simplifies application installation by providing a consistent interface across various systems, making it easier to manage and run applications regardless of the underlying Linux distribution. This is a repository where developers can upload their programs and make them available to all users globally. You can then explore and install apps from Flathub using either the command-line tool or the graphical user interface.

Software Management

There are numerous tools available for working with the Linux Mint package management system, ranging from simple graphical interfaces for novice users to command-line applications that system administrators may simply automate. The majority of these tools will be discussed in this chapter.

Software Manager

The easiest way is through the software manager. The Mintinstall Software Manager or simply Software Manager, is a graphical tool for managing software on Linux Mint. In the Software Manager, you can install, remove, and update the software.

Launch Software Manager

Select the Mint Menu button. Choose the Software Manager icon from the favourites on the left side of the menu. ![](image_rsrc4CN.jpg)

Interface

There are three parts to the interface. At the top, there is a search bar where you can search for any package to install or uninstall. The second part displays the featured program, which you can install by clicking on any of them. The third section presents software categories.

![](image_rsrc4CP.jpg)

Install Software

Search and install

Another option for installing software is to search for it by name. Let's say you want to install VLC Player on your computer. This is a well-known music and video player. The procedure to search and install is:-

1.  Write VLC in the search bar.

2.  From the list of available software, Click the software to install. In our example, it is VLC.

3.  On the software description screen, press Install.

4.  Provide your password and press Authenticate on the authentication screen.

5.  The installation process will start. The progress bar will display the installation progress.

Install through the category

In the category area, applications are classified depending on their functionality. You can click on any category to explore the list of available software. Suppose you click on "Graphics". It will show all software related to painting, drawing, and photography.

1.  ![](image_rsrc4CR.jpg)Click the required software from the list.

2.  Some software offers both Flathub and deb packages; you can select the package type from the source dropdown menu.

3.  Press Install on the software description screen.

4.  On the Authentication screen, provide your password and press Authenticate.

5.  The progress bar will show the percentage of completion. 

Remove installed software.

At some point in time, you may need to delete the installed application to free up space on the disk. To remove the installed application:

1.  In the search bar, type the name of the software you want to remove. For example, you want to remove VLC, which you installed in the earlier segment. Write VLC in the search bar. From the list, look for the required software name. Installed software is marked by a small green tick in the upper right corner.![](image_rsrc4CS.jpg)

2.  Click the installed software.

3.  Click the Remove button on the software description screen.![](image_rsrc4CT.jpg)

4.  This process requires authentication. Provide your password and press Authenticate. The removal process will start. On completion of the removal process, the remove button will be converted to an install button on the application description screen

Sudo

When you perform commands that require administrative privileges (root access) on Linux, you normally use the sudo command or switch to the root user. Sudo command is useful for performing tasks that require administrative rights, such as installing software or modifying system configurations. When you use sudo, you’ll be prompted for your user password. This is the same password you use to log in to your Linux system.

In the next section, we will explore command-line utilities for software management. As it changes the whole system, we will need to add the sudo command as a prefix to most of these commands.  Here is an example of how to use the sudo command:

sudo apt install package1.deb

Package Management via Command Line

The apt (Advanced Package Tool) command-line software is a robust package management tool for Debian-based Linux distributions, such as Linux Mint. It streamlines processes such as package installation, updates, and system maintenance. Here's a comprehensive look at several elements of software management with apt.

Update

Update package database

The update option of apt refreshes the local package index by retrieving the most recent information from defined repositories. This ensures that your system is updated with the most recent package versions.

sudo apt update

Upgrade installed packages

After refreshing the package index, this command analyses your system for outdated packages and installs newer versions of those packages. It just upgrades existing packages and does not install or remove them.

sudo apt upgrade

Comprehensive upgrade

To update the system to the most recent versions of the packages and to intelligently manage the changing dependencies, we utilize the dist-upgrade option. In order to meet new dependencies, it might install new packages and uninstall old ones.

sudo apt dist-upgrade

Querying packages

The apt command offers thorough information about both software available for installation and software that has already been installed. It also allows users to search for specific packages, read their details, and track their current status.

Search for packages

The search option searches the repositories for packages that match the provided package name. It shows both the installed and available packages.

Syntax

apt search package_name

Example

sudo apt search foo

List all packages

To list all packages, you can use the list option of the apt command.

sudo apt list

List installed packages

To list all installed packages, use the list option of the apt command with the --installed argument.

sudo apt list --installed

Displays detailed information

To display detailed information about a specific package. It reveals essential details such as the package's version, description, dependencies, and maintainer. This command is useful for understanding what a package does and checking its attributes before installation or management.

Syntax

apt show package_name

Example

apt show libreoffice

Searches for packages that provide a specific file or command

Syntax

aptfile search/find command/file_name

Example

sudo aptfile update

sudo aptfile search bin/vim

Installing packages

Installs a package and its dependencies

To install the packages on Linux Mint, use apt with the install option and specify the package name from the repositories. You can install multiple packages by listing them one after the other.

Syntax

apt install package_name

Example

sudo apt install vim

Install the downloaded debian package

You can use the dpkg command to install a Linux Mint package that you have downloaded. This is a detailed how-to:

Go to the directory: Open a terminal and go to the location where your downloaded package file.

cd ~/Downloads

Install the package: Run the dpkg command with the -i flag to install the downloaded package. Replace PackageName.deb with the full name of your package file.

sudo dpkg –i foo.deb

If the package requires dependencies that are not already installed, it will prompt you to confirm their installation. Enter Password (if prompted).

Removing packages

When a package is no longer required and must be removed. the following commands removes the specified package from the system.

Removes a package

Remove the given packages and all of their dependencies (assuming they are not required by other packages or were not explicitly installed by the user).

Syntax

apt remove package_name

Example

sudo apt remove vim

To remove a package and its configuration files

Syntax

apt purge package_name

Example

sudo apt purge vim

Clean Cache

apt caches downloaded packages in the  /var/cache/apt/ directory. You can clean the cache using the clean option of the apt command.

sudo apt clean

Verify installation

After the installation procedure is complete, you can verify the successful installation of the software.

Syntax

apt list -a PackageName --installed

Example

sudo apt list -a vim --installed

Aptitude

Aptitude is a text-based and command-line interface for APT (Advanced Package Tool), which is mostly utilized for Linux distributions based on Debian, such as Linux Mint, for package management. Compared to apt, it offers a UI that is more interactive and user-friendly. You will get a menu-driven interface if you launch Aptitude without any command-line arguments. Aptitude is best suited for use in a non-graphical terminal environment. Entering the following command at a terminal prompt will launch Aptitude's menu-driven interface for regular users.

sudo aptitude

![](image_rsrc4CU.jpg)Two pans, top and button, will appear when you run aptitude. Categories like installed packages, not installed packages, virtual packages, etc. are contained on the top pan. The package-related specific information is displayed in the bottom pan. Aptitude's user interface is intuitive, making it simple to handle packages.

Use these keys to access the aptitude after executing it:

*   '?' for help

*   Use Ctrl-T or F10 to bring up the menu.

*   To navigate, use the 'up, down, left, and right' keys.

*   Use 'Enter' key to select or open and close a single level.

*   The bracket keys to recursively open and close levels are '[' and ']'.

*   To install, update, or uninstall a package, press the '+' or '-' key.

*   To preview or confirm an action, press the 'g' key.

*   To exit, press the 'q' key, which also closes the window that is now active.

*   To search ahead or backward, use the forward and backward slashes ('/' and '\').

Installing Packages

To install a package, navigate to the "Not Installed Packages" category using the keyboard arrow keys and the Enter key.

Highlight the selected package and press the + key. The package entry should become green, indicating that it has been tagged for installation. Now, hit ‘g’ to see a summary of package actions. Press g again install the package. Once finished, hit Enter to return to the menu.

Remove Packages

Locate the package in the Installed Packages package category, then use the arrow key and ENTER key to highlight it in order to remove it. When the package is highlighted, hit the - key to designate it for removal. In order to remove the package, press g twice. When finished, hit ENTER. To go back to the main menu, press q.

Update the Package Index

To update the package index, hit the U key.

Upgrade Packages

To upgrade packages, first update the package index, then hit the U key to mark all packages as updated. Now, press g twice to download and upgrade the packages. After finished, press ENTER. Press q to return to the main menu.

Dpkg

dpkg is a low-level package management program that allows you to install, uninstall, and manage Debian packages directly, providing detailed control over package files. While higher-level programs like as apt and apt-get are more widely used, dpkg offers more precise control. However, dpkg does not automatically resolve or manage dependencies between packages; users must manually ensure that all required dependencies are addressed. Normally, dpkg is used to install software from .deb files stored on your computer. For example, if you manually downloaded a software package, you would install it using dpkg. Apt, on the other hand, is a utility for managing software from online repositories. It simplifies the process of installing, updating, and removing software by automatically handling dependencies. Here is summary of dpkg commands

Install Package

To install a Debian (.deb) package that you have already downloaded in the current directory, use the following command.

Syntax

sudo dpkg -i <package.deb>

Example:

sudo dpkg -i foo.deb

This installs the .deb package. If there are dependencies that are not met, you might need to resolve them manually.

List Known Packages

The -l option displays a list of all packages installed on your system. It is handy for viewing the current package inventory and versions.

dpkg -l

Remove Package

To remove the installed software while retaining its configuration files. This command is important if you want to save settings for future usage.

Syntax

dpkg -r <package>

Example

sudo dpkg -r foo

Purge Package

To completely remove the software and its configuration files. Use purge option if you want to completely remove the package from your system.

Syntax

sudo dpkg -P <package>

Example:

sudo dpkg -P foo

Check if the package installed

To check whether a package is installed, use the -s tag:

Syntax

dpkg -s <package>

Example:

dpkg -s foo

Show package information

To display extensive information about an installed package, such as version, status, and description. This command is also useful for checking if a package is already installed.

Syntax

dpkg -I <package.deb>

Example

dpkg -I foo*

Summary

These are just a few commands and examples of the many commands and options available for managing packages, repositories, and troubleshooting issues. Package management tools are essential in Linux Mint, since they ensure smooth program installation, updates, and security. Learning package management tools ensures efficient software management, enhancing system stability, security, and troubleshooting capabilities in Linux Mint and other Linux distributions. The apt manual (man apt command), which offers thorough documentation on all available commands and their options, is a great resource to consult whenever you need more guidance.

Chapter 13              

Configuring Repositories

Repository

A repository, sometimes abbreviated as "repo," is a central area where data is saved and handled. In the context of package management, a repository is often defined as a site where software packages, source code, and related metadata are saved and organized.

The following procedures can be used in Linux Mint to manage repositories via the graphical user interface (GUI):

Click the Menu button, select Administration, and then click "Software Sources" to access Software Sources. The Software Sources application will launch as a result.

![](image_rsrc4CV.jpg)

Authentication: When asked, provide your administrator password to authenticate.

The Software Sources window is divided into two panes. The left pane contains a list of items, each of which corresponds to a different component of repository management. The right side displays the description and setup of each item. The descriptions of each item in the left pane are as follows:

*   Official Repositories: This tab includes repositories maintained by Linux Mint for stable software updates.

*   PPA: A PPA (Personal Package Archive) is a repository on Launchpad where developers can distribute software packages directly to users.  Users can install packages in the same way they install normal packages, and they'll automatically receive updates as they become available.

*   Additional Repositories: By selecting the "Add" or "Remove" buttons, you can add or delete third-party repositories here.

*   Authentication Keys: Managing authentication keys involves adding, removing, and verifying keys. Authentication keys verify the integrity and origin of packages to prevent tampering and ensure that the software comes from a legitimate source.

*   Maintenance: Here, you can configure the settings for automatically updating the repository cache and removing unused packages.

Adding Repositories

To add a new repository, go to the Additional Repositories section on the left side pane and then click the "Add" button on the right side panel. Enter the repository URL in the text box and click the Ok button.

 ![](image_rsrc4CW.jpg)

![](image_rsrc4CX.jpg)Removing Repositories

Select a repository from the list of Additional Repositories and click the "Remove" button. Press the Yes button on the confirmation popup.

Applying Changes

After making your changes, you may be prompted to update the package cache; hit Ok to update the changes.

![](image_rsrc4CY.jpg)

PPA

Adding PPA Repositories

To create a new PPA repository, select the PPA in the left pane and then click the "Add" button. Enter the repository's URL and press Ok. On the repository description window, press OK again.

![](image_rsrc4CZ.jpg)

Removing PPA Repositories

Select a repository from the list of PPA repositories and click the "Remove" button. Press the Yes button on the confirmation popup.

![](image_rsrc4D0.jpg)

Authentication Keys

Add Authentication key

Generally, when you add a new repository, you must also include authentication keys. To add a new key, click the Import button and select the already downloaded key file provided by the repository maintainer. Press Open button.

![](image_rsrc4D1.jpg)

Alternatively, you can utilize the "Download" option to add a key by fingerprint.

Remove authentication keys

To remove a key, select it from the list and click on the Remove button.

![](image_rsrc4D2.jpg)

Configuring repositories using CLI

Apt (Advanced Package Tool) is a robust command-line tool for managing packages and repositories in Linux Mint and other Debian-based distributions. Repositories are servers that hold packages and updates for your system. Apt saves a list of repositories or software channels in /etc/apt/sources.list and any files with the suffix .list under the directory /etc/apt/sources.list.d. These files can be manually edited from the command line to add, remove, or temporarily disable software repositories. It is recommended that you keep a backup of the file before altering it.

To store a backup copy of the original file:

sudo cp /etc/apt/sources.list.d/official-package-repositories.list /etc/apt/sources.list.d/official-package-repositories.list.backup

Here is the example :

![](image_rsrc4D3.jpg)

Description of the file

*   All the lines beginning with hash (#) are comments

*   deb: These repositories hold binaries or precompiled packages. Most users require access to these repositories.

*   deb-src: repositories include the packages' source code. Useful for developers.

*   http://packages.linuxmint.com: The URI (Uniform Resource Identifier) or location.

*   main upstream import backport: The section names or components.

Adding Repositories

You can add additional repositories by creating a file with the extension .list in the /etc/apt/sources.list.d directory using the same format as described in the previous section.

After defining a new repository, refresh the package cache with the following command:

sudo apt update

Using add-apt-repository command

APT repositories can be added with the Python program add-apt-repository. You can also use the command to remove an existing repository.

sudo add-apt-repository ppa:fossfreedom/arc-gtk-theme-daily

Refresh cache

sudo apt update

This configuration of repositories gives you access to a greater selection of updates and software packages for your Linux Mint system. When adding third-party repositories, exercise caution though, as these can contain packages that haven't been thoroughly examined by the Linux Mint maintainers.

Chapter 14              

Install New Fonts

Adding fonts to a Linux system can substantially improve the appearance and usefulness of your desktop environment. Fonts are important not just for visual appeal, but also for readability and compatibility with different languages and scripts. Whether you're a graphic designer, developer, or simply someone who appreciates a well-designed user interface, having a varied font selection allows for greater customization and personalization. Installing additional typefaces can enhance document display, web design, and user experience, making your system more adaptable and adapted to your individual requirements. Here's a basic overview of how to add fonts to your Linux system.

Using the software manager to install fonts

![](image_rsrc4D4.jpg)

From the main menu, select Software Manager. Use the search option to locate fonts by name, or go through categories such as "Fonts." Click the "Install" button after selecting the font package you wish to install.

![](image_rsrc4D5.jpg)

Manual Installation

If you have font files (usually .ttf,.otf, or other formats), you can install them manually. First, open the terminal and then copy the downloaded font files into one of the system font directories.

*   For system-wide installation, copy the files /usr/share/fonts/ directory, as it requires administrator permissions, you will need to use the sudo prefix command.

*   For user-specific installation, copy the font files to the user's home directory (~/.local/share/fonts/ or ~/.fonts/). If the directory does not exist, create it first.

user1@Mint:~/.local/share/fonts$ cp ~/Downloads/Rostack.otf .

After copying, update the font cache using the following command.

fc-cache -fv

Conclusion

In this chapter, we learned how to install new fonts on a Linux system, which enhances visual appeal, readability, and overall functionality. By adding fonts, you can improve document appearance and personalize the user experience to better fit your requirements.

Chapter 15              

Managing Users

In Unix-like operating systems, such as Linux Mint, users and groups are basic concepts. They are critical to the system's management of resource allocation, permissions, and access control.

User and group management refers to the activities and procedures involved in setting up, configuring, managing, and monitoring user accounts and groups on a computer system. This method is critical for limiting access to system resources, guaranteeing security, and enabling user collaboration. Here is a summary of user and group management:

User Management

Account creation: Account creation involves creating new user accounts on the system.

Account configuration: Account configuration entails defining user attributes such as username, user ID (UID), home directory, login shell, and password.

Password management: Password management entails creating, modifying, and enforcing password restrictions for user accounts.

User privileges: Granting users suitable privileges, such as administrative (root) access or limited access to specific resources.

User deletion: The process of removing user accounts from the system that are no longer required.

User Authentication: Implementing authentication measures to check users' identities during login.

Group Management

Group creation: Creating new groups to organize users and control their access to resources.

Group configuration: Configuring group properties such as group name and group ID.

Group membership: Adding or deleting users from groups for controlling access permissions.

Group ownership: Assigning group ownership to files and directories allows you to control access privileges.

Special groups: Managing special-purpose groups (such as sudo, audio, and video) with unique privileges and permissions.

Access Control

Permission assignment: Permission assignment is a broad topic that covers granting read, write, and execute permissions to users and groups on files, directories, and other system resources.

File System permissions: Managing file system permissions to limit access to sensitive data and system files.

Effective permissions: Identifying users' effective permissions based on individual permissions and group memberships.

Monitoring & Auditing

User activity monitoring: User activity monitoring is the process of monitoring user login sessions, commands executed, and resource access for security and auditing purposes.

Logging: Keeping track of user and group activity for troubleshooting, compliance, and forensic analysis.

Enforcing Security rules: Implementing security rules and best practices for user authentication, password management, and access control.

Enforcing Resource limitations: Creating quotas and limitations for users and groups to avoid abuse and ensure equitable resource distribution.

In any computing environment—whether it's a single-user system, a multi-user server, or a networked enterprise environment—effective user and group administration is crucial for preserving system integrity, security, and efficiency.

Users

A user is a person who logs in to the system and uses it for different purposes. On a Unix-like system, every user account has a distinct username and user ID (UID). Users have certain account-specific permissions and settings, and they have the ability to own files and processes.

User Characteristics

Each user typically has several characteristics and attributes associated with their account. Here are some of the key characteristics:

*   Username: The name that appears on the screen when a user logs in and uses the system.

*   User Identification (UID): a unique number linked to every user account. It gives the user a special identification within the system.

*   Home directory: The user's directory, which contains its configuration settings and files.

*   Password: During the authentication procedure, passwords are used to confirm the user's identity.

*   Login shell: This is the command interpreter or shell that the user uses to log into the system.

Users management

In Linux, graphical user interfaces (GUIs) can be used alongside command-line tools to add and manage users. GUIs offer a more user-friendly approach to user administration duties.

Create users

The system creates one user during installation; to add more users, use the command line or a graphical user interface (GUI), whichever is more convenient for you.

Using GUI

1.  Click the Menu button, select Administration, and then "Users and Groups". This will launch the User and Group Management tool. When prompted for authentication, provide your administrator password.

2.  At the user tab. Click the Add button.

3.  A dialog box will appear in which you can enter the information for the new user:

![](image_rsrc4D6.jpg)

Account type: Select whether the user will be Standard or Administrator (with sudo rights).

Full Name: User's Name or Description

Username: Fill in the preferred username for the new user.

4.  Press the Add button.

5.  Once added, the new user will appear in the list of users in the Users.

Setting user password

Once you've created a user, you should assign it a password.

1.  Select the user whose password you want to change from the list of users.

2.  Click on the “No password set”.

![](image_rsrc4D7.jpg)

3.  ![](image_rsrc4D8.jpg)It will open a dialog box. Enter the new password for the user in the provided fields. Press the Change button.

Using command line

Using the useradd command and the desired username will allow you to create a new user.

Syntax

useradd -m user_name

Here the -m flag creates a home directory for the user.

Example

sudo useradd -m user2

Setting user password

Run the passwd command to assign a password to the newly created user.

Syntax

passwd user_name

Example

sudo passwd user1

Deleting users

When a user is no longer required, you should remove them. Deleting a user in Linux Mint removes unnecessary access, improves security by eliminating potential dangers associated with inactive accounts, and optimizes system resources by freeing up storage and configuration space allotted to the user. Here's how to do it in GUI and CLI mode:

1.  Select the user you want to delete from the list of users

2.  Click on the "Delete" button. Confirm the deletion when prompted.

![](image_rsrc4D9.jpg)

Once confirmed, the user account will be removed from the system.

Using CLI

To delete a user from the system, you can use the userdel command:

Syntax

userdel user_name

Example

sudo userdel user1

Listing users

To list all defined users on the system

Syntax

cat /etc/passwd

Example

sudo cat /etc/passwd   

Modify user properties

To modify user settings (password, group membership, username, etc.) using the GUI.

1.  Select the user you want to modify from the list of users.

2.  You can alter a number of parameters in the right pane, including:

Account type: Switch from Standard to Administrator or vice versa.

Username: Change it if necessary.

Password: Select the "Password" to modify the user's password.

Groups: Select or deselect groups by clicking on the "Groups" popup to manage group memberships. ![](image_rsrc4DA.jpg)

3.  After making the necessary changes, click "OK"

Using CLI

To edit user characteristics such as username, home directory, shell, and so on, use the usermod command on the command line.

Change username

Syntax

usermod -l new_user_name old_user_name

Example

sudo usermod -l myuser user1

Lock user account

Syntax

usermod -L user_name  

Example

sudo usermod -L user1

Unlock locked user

Syntax

usermod -U user_name  

Example

sudo usermod -U user1   

Disable password expiration

A clearly specified password expiration policy is an important aspect of system security. Setting a password expiration date ensures that passwords are updated on a regular basis, lowering the risk of unwanted access caused by compromised or expired credentials. In certain scenarios, you might need to disable or adjust automatic password expiration policies. This could be due to special operational needs, user convenience, or other corporate policies. To disable password expiration for the specified user:

Syntax

chage -M -1 user_name

Example

sudo chage -M -1 user1

Change User ID (UID)

Changing a user ID is sometimes necessary to resolve conflicts, reorganize system accounts, or align with organizational standards. To change userid of a user:

Syntax

usermod -u new_uid user_name

Example

sudo usermod -u 1091 user1

Change home directory

To change a user's home directory in Linux, update the user's account settings to point to the new location. This method is beneficial in a variety of situations, including moving user accounts, restructuring file storage, and renaming home directories. This is how you do it:

Syntax

usermod -d /path/to/new_home user_name

Example

sudo usermod -d /home/myhome user1

This command changes the user's home directory to /home/myhome.

Change default shell

The shell, or command-line interface, is an essential component of the Linux operating system, giving users a powerful means of interacting with the system. In Linux, changing a user's default shell means modifying the shell specified for the user account. The default shell controls the command-line environment with which the user interacts when logging in. Here's how you can change the user's default shell:

Syntax

usermod -d -s /path/to/new_shell user_name

Example

sudo usermod -s /bin/csh user1

This command changes the shell to c shell.

Add user to additional groups

By default, a user belongs to a primary group whose name is the same as their username. Using the -aG option with usermod, you can add a user to more groups. This allows users to access resources or perform actions associated with those groups

Syntax

usermod -aG group_name user_name

Example

sudo usermod -aG group2 user1

Monitoring User Activity

Monitoring user activity on a Linux system is critical for security, troubleshooting, and compliance reasons. You can monitor user behavior with a variety of methods and tools, including:

System logs

The system logs, placed in /var/log, include useful information about user activity, such as login/logout events, authentication attempts, and system events. The most important logs for user activity monitoring are:

*   /var/log/auth.log: It keeps track of authentication-related events, such as successful and unsuccessful login attempts.

*   /var/log/syslog, /var/log/messages: Contains general system activities, such as user login and logout events.

You can filter and analyze log entries via tools such as grep, tail, and less.

last command

The last command shows a history of login sessions, together with the timings, durations, and terminal sessions of each login.

Example

 last

who command

The who command shows details about the users that are presently logged in to the system, such as their usernames, terminal sessions, and login times.

Example

 who

w command

The w command provides comprehensive details on users who are currently logged in, such as their usernames, terminal sessions, login times, idle times, and current processes.

Example

 w

Process Monitoring

You can monitor processes that are running and find out who is running them with the use of programs like ps, top, and htop.

Syntax

ps aux | grep user_name

Example

ps aux | grep user1

Groups

Groups enable administrators to provide permissions to a group of users rather than handling rights individually. This method makes it easier to manage access privileges for files, directories, and other system resources.

Creating groups

Creating groups in a Linux system is an essential part of user management and access control. Groups assist to organize users and manage rights in a more effective and scalable manner. To add a user in GUI mode, follow the instructions below:

1.  Open the Users and Groups management tool. Enter your administrator password when prompted to authenticate. ![](image_rsrc4DB.jpg)

2.  Click on the "Groups" tab to view the list of existing groups.

3.  To create a new group, click the Add button.

4.  In the dialog box, provide the new group a name.

5.  Click "OK" to create the new group.

Using CLI

To create a new group on the command line, use the groupadd command followed by the group name.

Syntax

groupadd group_name

Example

sudo groupadd group1

Adding users to groups

With the -aG option, the usermod command can be used to add a user to a group.

Syntax

usermod -aG group_name user_name

Example

sudo usermod -aG group1 user2

Deleting Groups

Removing a group in Linux helps keep the system clean, secure, and organized by deleting obsolete or superfluous groups, streamlining group management, and guaranteeing correct access control. To remove a user in GUI mode: 

1.  Open the Users and Groups management tool. Enter your administrator password when prompted to authenticate.

2.  Select the group you want to delete from the list of group.

3.  Press the Delete button to remove the group. 

Using CLI

Using the groupdel on the command line, you can remove a group when it is no longer needed.

Syntax

groupdel group_name

Example

sudo groupdel group2

Listing groups

To list all defined groups on the system.

Example

sudo cat /etc/group    

User and Group Configuration Files

User and group information is managed through configuration files located primarily in the /etc directory. Here are the main files related to user and group management:

/etc/passwd

The /etc/passwd is a plain text file. It contains information about each user on the system like user ID, group ID, home directory, shell, and more. Each line represents a user account and consists of seven fields separated by colons (:)

Syntax

Username:password:UID:GID:GECOS:home_directory:login_shell

*   username

*   password: An 'x' character, indicating that the encrypted password is stored in /etc/shadow.

*   UID: User ID.

*   GID: Primary group ID.

*   GECOS: User information like full name, phone number, etc.

*   home_directory: The user's home directory.

*   login_shell: The user's default login shell.

Example

![](image_rsrc4DC.jpg)

/etc/group

The /etc/group is plain text file. It contains information about each group on the system, including group name, group ID (GID), and a list of users who are members of the group. Each line represents a user account and consists of several fields separated by colons (:). This file contains the password hash as well as other password-related properties such as password expiration and account locking information.

Syntax

group_name:password:GID:user_list

Here's what each field represents:

*   group_name: The group's name.

*   password: A password that is encrypted and is typically used to verify a group member's identity. To indicate that the password is kept in the /etc/gshadow file or another authentication method, it is often set to 'x' or '*'.

*   GID: The group ID, which is the group's numerical identity.

*   User_list: A list of usernames belonging to the group, separated by commas.

Example

![](image_rsrc4DD.jpg)

/etc/shadow

The /etc/shadow file is another crucial system file found on Unix-like operating systems, including Linux. Unlike /etc/group, which stores group information, /etc/shadow contains encrypted password information for user accounts. This file is essential for system security because it stores user passwords in encrypted form, as well as other account-related information like password expiration dates and account lockout policies. It's typically accessible only to privileged users, such as the administrator (root) user. Each line in the /etc/shadow file represents a separate user account and contains several fields separated by colons. The typical format of a line in the /etc/shadow file is as follows:

username:password:lastchg:min:max:warn:inactive:expire:flag

Here's what each field represents:

*   username: The username of the user.

*   password: The encrypted password for the user account.

*   lastchg: The last password change date, represented in days since January 1, 1970 (Unix time). This field is usually used to enforce password expiration policies.

*   min: The minimum number of days required between password changes i.e. the number of days left before the user is allowed to change her password again. An empty field and value 0 mean that there are no minimum password age.

*   max: The maximum number of days that a password can be valid before being changed

*   warn: The number of days before the password expires that the user is reminded that his or her password must be changed.

*   inactive: The number of days following the password expiration date before the account is disabled.

*   expire: The date of expiration of the user account, expressed as the number of days since Jan 1, 1970.

Example![](image_rsrc4DE.jpg)

To summarize, User and group management are key components of Linux system administration that ensure secure and efficient access control. Administrators create and edit user accounts and groups to control rights, enforce security policies, and simplify resource access. Key duties include adding and deleting users, updating user information, and managing permissions for users via group memberships.

Chapter 16              

Keeping Your System Up-to-Date

Updating installed packages to the most recent versions is critical for following reasons: -

Security: Software upgrades frequently include remedies for vulnerabilities in security. Keeping your packages up to date ensures that your system is protected from known security threats. Failure to upgrade could expose your system to exploitation.

Bug fixes: Updates regularly feature bug fixes and performance enhancements. Updating guarantees that you have access to the most recent bug fixes, which improve the stability and efficiency of your system.

Compatibility: Updated packages may improve compatibility with other software or system components. Keeping your packages up to date helps to avoid compatibility difficulties caused by utilizing obsolete software versions.

New Features: Updates may include new features or updates to current software. By updating frequently, you may take benefit.

Update using Update Manager

Mintupdate, commonly known as Update Manager, is a GUI utility for handling system updates. The update manager has a user-friendly interface. It categorizes updates based on their kind, such as kernel, software, and security updates. Users can initiate updates with a single click, and the tool displays notifications and a history of installed updates. Customization options allow users to tailor update preferences to their specific needs. Update manager appears as an icon in the system tray (systray) on the panel, providing an easy way to monitor and handle updates. If fresh updates are available, the icon changes to show a red indication. If you hover over it, it will display the number of available updates. Overall, mintupdate helps you maintain your system secure and up to date.

![](image_rsrc4DF.jpg)

When you click this icon, it will launch the update management GUI window. You can also open Update Manager from the Mint menu's Administration category. The Update Manager will initiate an automatic check for updates upon opening. In the event that it doesn't, you can start a check by clicking the “Refresh” button.

![](image_rsrc4DG.jpg)

The main window will show the available updates. Updates are typically divided into security updates, software updates, security updates, and desklet updates, among other categories.

Click on the “Install Updates” button to begin the installation process. You may be asked to enter your password. This is necessary to authorize the update procedure.

After installing updates, you can review the update history by selecting view option on the menu and select “History of Updates”.

Installing latest or other versions of kernel

The kernel is the central component of an operating system, managing hardware resources and facilitating communication between hardware and software. It handles memory management, process scheduling, and device control, serving as a link between applications and hardware.

Kernel updates are critical for supporting new hardware since they provide drivers and fixes that fix compatibility concerns. Support for new hardware may necessitate kernel updates, as new components or devices may not be recognized or function properly with earlier kernels. Tools like Update manager simplify the process of applying these updates, ensuring your system remains compatible with the most recent hardware and benefits.

It's crucial to use caution even though upgrading to the most recent kernel can offer new features and better hardware support. Before updating, it's a good idea to review release notes and user reviews as new kernels may bring unforeseen issues or instability. To prevent any data loss, make sure you backup critical data. Moreover, maintain earlier kernels installed as backups in case the new kernel presents problems.

To install an alternative kernel, do the following:

1.  In the Update Manager box, choose "View" from the menu.

2.  Select the "Linux Kernel" option to view available kernel versions. You will see a list of installed and accessible kernels. Newer kernels should also appear on this list. ![](image_rsrc4DH.jpg)

3.  Choose the latest or required kernel version from the list. There will generally be options for installing or upgrading. Click the "Install" button to begin the installation procedure.

4.  You may be asked to enter your password.

5.  After installation, restart your system to use the updated kernel. You can do this by selecting "Reboot" from the menu.

Change preferences

In Update Manager, you may customize update options to your specific requirements. Click the "Edit" menu item in the Update Manager box. Select "Preferences" from the dropdown menu. The preferences are handled via a tabbed window interface. The tabs include Options, Packages, and Automation.

Update Using Command line tool

You can use terminal commands to do system updates, upgrade packages, and manage kernels. Here's how you do it:

The first step you should take is to update the package database. This is a critical step before executing system upgrades or installing new packages, since updating the package database synchronizes this information with the Linux Mint repository, ensuring that your system has the most recent information on available packages and their versions.

Use apt command to synchronize the package database with the Linux Mint repositories.

 sudo apt update

Update installed packages

To update installed packages to their latest versions in Linux Mint, you can use the apt command line tool. Below are the commands to update all installed packages. The first command updates the package cache, and the next command does a system update.

sudo apt upgrade

If there are any kernel updates, reboot the machine to apply them.

Chapter 17              

Backing Up Your System

Backup

Backups are an essential component of system management, helping to protect data, recover from disasters, mitigate risks, ensure compliance, secure system upgrades, provide user support, and preserve institutional knowledge. Backups serve as an insurance policy against data loss, providing peace of mind to stakeholders and protecting the organization's assets.

System administrators are responsible for implementing and managing backup methods that assure the integrity and availability of organizational data and systems. Here's how you can perform backups:

Manual Backup

Manually copy critical files and directories to an external device or cloud storage with commands such as cp or rsync. To take a manual backup involves following steps:

1.  What: First, determine which files and directories contain critical data, configuration files, or user settings that you want to backup.

2.  Where: Choose an external storage device, such as a USB drive, hard drive, network storage, or cloud storage service, to save the backup.

3.  How: To copy selected files and directories to the backup destination, use command line programs such as cp or rsync.

Full System Backups

Create full system backups on a regular basis using software such as clonezilla or dd to restore the entire system in the event of a catastrophic failure.

Automated Backups

Set up automated backup routines with cron jobs or systemd timers to perform regular backups without requiring manual involvement.

Testing backup

Periodically test your backups to ensure they work and can be successfully restored. Evaluate file restoration, system recovery, and data integrity.

Disk space cleanup

To free up disk space, regularly delete useless files, temporary files, and cached data. du, df, and ncdu are useful programs for analyzing disk consumption and identifying huge files.

GUI backup tools

MintBackup and Timeshift are two essential backup tools bundled with Linux Mint. Both are distinct programs in Linux Mint, serving separate functions.

MintBackup

MintBackup is a program in Linux Mint for protecting crucial files and settings. It allows you to backup individual folders and files, ensuring that your images, documents, and sensitive information are safe. You can keep these backups on external disks or in cloud storage, making them easy to recover if your computer fails. MintBackup's intuitive interface makes it easy to use without requiring technical knowledge.

To use MintBackup in Linux Mint to backup your data and configurations, follow these steps:

1.  MintBackup can be launched from the Applications menu in Linux Mint. Look for "Backup Tool" or simply type in "MintBackup".![](image_rsrc4DJ.jpg)

2.  When MintBackup opens, it displays two sections: personal data and software selection.

Backup personal data

1.  Click the “Back up now” button.

2.  Select the location to save the backup. The default backup location is a folder, but it can alternatively be an external device such as a USB stick.

![](image_rsrc4DK.jpg)

3.  It will then prompt you to specify which files and directories to exclude.

![](image_rsrc4DM.jpg)

4.  On the next screen, you'll have options for what you wish to back up. Typically, you can pick certain directories (such as Documents, Pictures, etc.).

![](image_rsrc4DN.jpg)

5.  MintBackup will compress the selected files into an archive format (like a .tar.gz file) and save it to the specified location. After completing the backup, you will get a confirmation screen.

![](image_rsrc4DP.jpg)

Restore

To restore, click the “Restore” button.

It will open screen to select the backup to restore.

Option for overwrite exiting files :

*   No, only restore missing files: Useful in case files are deleted.

*   Yes, overwrite changes and restore the content of any existing files: Useful for when a file is corrupted or when you need an older version of a file or files.

Choose the option that meets your requirements and press the Forward button.

 ![](image_rsrc4DR.jpg)

After completing the backup, you will get a confirmation screen.

Timeshift:

Timeshift is another tool included in Linux Mint that focuses on backing up your entire system. It periodically takes snapshots of your filesystem so that, in the event that something goes wrong, you can return your system to a previous state. Timeshift is very beneficial for maintaining system stability and recovering from software issues or updates that cause problems on your Linux Mint system. It provides functionality similar to the System Restore feature in Windows and the Time Machine tool in Mac OS. It works in BTRFS and RSYNC modes.

RSYNC: Snapshots in RSYNC mode are made with hard links and rsync. Disk space is saved between snapshots because common files are shared. With the use of a file manager, each snapshot represents a complete system backup.

BTRFS: Snapshots are taken in BTRFS mode by utilizing the built-in capabilities of the BTRFS filesystem. BTRFS snapshots are only supported on systems that use the BTRFS filesystem and have a subvolume layout similar to Ubuntu (@ and @home).

Setting up Timeshift

When you first launch Timeshift, an authentication prompt will appear, followed by an application setup prompt.
Timeshift will prompt you to select the sort of snapshot you want to take. You can choose between Rsync and Btrfs.

If your file system supports Btrfs, it is widely recommended due to its efficiency in managing snapshots. ![](image_rsrc4DS.jpg)
Next, you'll need to decide where to save the images. This might be a different partition, an external disk, or any other appropriate location with adequate space to store the snapshots. For best results the snapshots should be saved to an external device. Connect the external device before launching Timeshift if you wish to take a backup there. ![](image_rsrc4DT.jpg)

![](image_rsrc4DU.jpg)Next, it will ask for a backup schedule. Timeshift supports multiple levels of snapshots. Snapshot levels refer to various strategies or procedures for creating and managing your system's snapshots. These levels enable you to control how and when sanpshots are taken, based on your specific requirements and preferences. It allows hourly, daily, weekly, monthly, and boot snapshots. You can also specify the number of snapshots to be retained for each level. Boot snapshots are made every time the system boots up, providing an extra degree of backup. Boot snapshots are created with a 10-minute delay to ensure that system initialization is unaffected.

Manual Snapshot

To create a manual snapshot, select the Create button.
Timeshift will then generate a snapshot of your system. This process could take some time, depending on the size of your system and the speed of your storage.

![](image_rsrc4DV.jpg)

User Data

Timeshift is intended to protect system files and settings. It is a backup application that is not intended to protect user data.

The whole contents of users' home folders are excluded by default. This offers two advantages:

*   You don't have to be worried about your documents being overwritten when you restore an earlier snapshot to recover the system.

*   Your music and movie collection in your home directory will not take up space on the backup device.

System Restore

If you have a problem with your system, you can use Timeshift to restore it to its former stable state.

Open Timeshift, select a snapshot from the list of available snapshots, and then click "Restore.

*   Snapshots can be restored from either the current system (online restore) or another system with Timeshift installed (offline restore).

*   If the main system is not bootable, you can boot from installation media on USB or DVD as a live session, start Timeshift on the live system, and restore a snapshot on the main system.

*   Restoring backups from the running system requires a reboot to complete the restore process.

Command line tools to backup

You can manually back up your files using command line tools.

Backing up with command-line tools in Linux allows you greater freedom and customization. Here's a simple instruction for performing backups using common command-line tools.

Tar

Tar is a simple and versatile utility for backup and restore.

The Linux command 'tar' stands for tape archive and is used to create and extract archive files. The tar program in Linux is a useful tool for archiving files and directories. The Linux tar tool allows us to create compressed or uncompressed Archive files, as well as manage and alter them.

Syntax

tar [options] [archive-file] [file or directory to be archived]

Where options are

| -c | Create a new archive. |
| -x | Extract files from an archive |
| -v | Verbose mode (shows files being archived). |
| -f | filename of the archive. |

You can also use compression software like gzip, bzip2, and xz to compress tar archive files. Use these options while creating extracting tar files:

| -z | Use gzip compression. |
| -j | Use bzip2 compression. |
| -J | Use xz compression. |

Backing Up

Open the terminal and execute the tar command. If you wish to take backups on the external media, it should be linked first. To build a backup tar archive, use the tar command with the -c option.

tar -cvf backup1.tar file1.txt file2.txt

To create an archive of directories

tar -cvf backup1.tar Documents/

To create an archive in compressed format

tar -cvzf backup1.tar.gz Documents/

Restoring

To restore (extract) a tar archive, use the -x option with the tar command.

Example

tar -xvf backup1.tar

To extract an archive in compressed format

tar -xvzf backup1.tar.gz

Tar may be used to append files to an existing archive, allowing you to add new files without having to recreate the entire archive using -r option. Here's how you can accomplish it:

tar -rvf backup1.tar newfile.txt

In conclusion, system administrators and users looking for dependable data backup solutions in Linux-based systems favour tar because of its strong backup capabilities, which include its capacity to efficiently archive, compress, automate, and handle incremental backups.

By completing these tasks on a regular basis, you can guarantee that your Linux Mint system remains stable, secure, and reliable. Make maintenance a part of your daily routine to avoid potential problems and data loss.

Chapter 18              

Network

What is a computer Network?

A computer network is a group of computers and computing devices that are linked together. This link provides communication between the different computers and devices in that group. Computers and devices can use wire, fibre optic, or microwave as a medium of communication. There are many types of networks, but we will focus on TCP/IP as it is the most popular protocol in use both on local area networks (LAN) and wide area networks (WAN), such as the internet. We generally classify networks into wireless and wired networks, which are two major types of computer networks defined by their connection techniques.

Wireless networks: Wireless networks employ radio waves to connect devices. It allows devices to connect to the network without the usage of physical cords. Wireless networks are popular in homes, businesses, and public locations because they are simple, flexible, and mobile to connect. We commonly use WiFi for wireless networks.

Wired networks: Wired networks use wires to connect devices. Ethernet cables, coaxial cables, and fiber optic cables are common types of cables used in wired networks. Wired networks frequently offer faster and more consistent connections than wireless networks, making them excellent for applications that require high bandwidth or low latency.

In Linux Mint, you can configure wired and wireless networks using a variety of graphical user interface and command-line tools. Here's how to configure networking:

Establishing a Wireless connection.

When your wireless network is connected, it will show a Wi-Fi icon on the panel.

If you see the network icon with a cross, it signifies you are not connected to any network.

![](image_rsrc4DW.jpg)

To connect to your home or office wireless network, follow the below procedure: -

*   Click the network icon with a cross to expand the collapsed menu, which will display the available networks.

*   Select your Wi-Fi network name.

![](image_rsrc4DX.jpg)

*   If the network is password protected, it will ask for the password. Provide your password and press Connect.

![](image_rsrc4DY.jpg)

Once your network is connected, the panel will display a Wi-Fi icon.

![](image_rsrc4DZ.jpg)

Wired network

Connecting to a wired network is easy; just plug the network cable into your computer. The system will automatically configure the system for the available network. Once the system connects to a wired network, the network icon appears on the panel.

![](image_rsrc4E0.jpg)

Later in this chapter, we will learn how to configure a wired network manually.

Command line network management

Before proceeding with network configuration, it is advisable to identify the devices present in the system.

Identify network interfaces

To identify your network interfaces, open a terminal and run the command below:

sudo ip link

This command will list all network interfaces, including their names and statuses. To identify your network interfaces, look for interfaces beginning with en, wl, or ww. Once you've found the relevant interface, you can utilize its name to perform additional configurations, such as networking or troubleshooting connectivity.

![](image_rsrc4E1.jpg)

Naming convention

Historically, Ethernet devices were designated as ethX (e.g., eth0, eth1). However, with the introduction of predictable network interface names, newer Linux distributions, like Linux Mint, have adopted a more uniform naming convention based on variables such as the device's physical location or attributes.

Predictable network interface names are a consistent approach of naming network interfaces in Linux, making it easier to identify interfaces even after system reboots and hardware modifications.

The naming scheme usually follows this pattern:

| en | for Ethernet |
| wl | stands for wireless LAN. |
| ww | stands for Wireless Wide Area Network |
| p | for PCI bus. |
| o | onboard gadgets. |
| sN | stands for slot number. |

Example

enp0s3: Ethernet interface, PCI bus 0, slot 3.

wl0: Wireless LAN interface.

IP Address Assignment Types

In order for devices to connect and uniquely identify themselves to one another over networks, IP (Internet Protocol) addresses are essential. IP addresses are mostly assigned using two methods: static and dynamic. Each approach has its own set of benefits and applications. Let's examine these to learn how they work and when to use them.

DHCP

DHCP stands for Dynamic Host Configuration Protocol. It is a network administration protocol for IP networks in which a DHCP server dynamically provides IP addresses and other network setup parameters to network devices such as PCs, cellphones, and IoT devices. DHCP makes network management easier by automatically assigning IP addresses and network configuration settings to devices, eliminating the need for human configuration.

Static Address

Static address assignment, as opposed to dynamic assignment via DHCP, involves manually specifying a device's network parameters, such as its IP address, subnet mask, default gateway, and DNS server addresses. This strategy is commonly used with devices that require a continuous and unchanging network setup, such as servers, printers, or network appliances.

Now you understand that both dynamic and static IP address assignment methods have advantages and are appropriate for various network settings and use cases. Understanding the differences enables network managers to select the best solution depending on their individual needs and network equipment.

Manual Wired network configuration.

Most of the time, wired network settings are automatic, but in other circumstances, you must specify the IP address manually, especially in the office environment. This type of configuration is known as "static IP address configuration."

To configure static IP address:-

1.  Click the network icon on the panel.

2.  Click Network Settings.

![](image_rsrc4E2.jpg) ![](image_rsrc4E3.jpg)

3.  It will bring up the network settings window.

4.  The Wired field indicates the status of the network. Make sure the button is in the ON position.

5.  Click the gear icon.

6.  Click IPv4 in the left pane of the window.

![](image_rsrc4E4.jpg)

*   Choose Manual as the addresses from the dropdown menu.

*   Provide an IP address.

*   Enter Netmask,

*   Enter Gateway.

*   If required, set DNS to manual and provide a server IP address.

*   Press “Apply”.

Hostname

A hostname is a label that identifies a computer networked device. It is used to identify the device on the network. Hostnames are typically alphanumeric and can include hyphens but not underscores. Hostnames are commonly used in conjunction with IP addresses to locate and connect with networked devices.

Hostnames on a local network or on the internet are translated to IP addresses using DNS (Domain Name System) servers. For example, when you enter a domain name (such as "example.com") into a web browser, your computer requests a DNS server to resolve the domain name to an IP address, allowing it to connect to the right server.

On a small network with a few workstations, the hostname is commonly specified through the operating system's network settings.  It can also be specified manually in configuration files. A computer on a home network may have a hostname such as new-laptop, Guest-PC, or myPC.

You normally have the option to specify the hostname (Computer Name) during the Linux Mint installation, but if you wish to change it afterward, follow these steps:

You can view and set the hostname using the hostname command.

To check current hostname

hostname

To change or set new hostname

Syntax

sudo hostnamectl set-hostname new-hostname

Example

 sudo hostnamectl set-hostname My-LinuxMint

Next edit the /etc/hosts file:

sudo nano /etc/hosts

Replace any occurrence of the existing computer name with your new one.

![](image_rsrc4E5.jpg)

To save the file, use the Ctrl + O key and Press ENTER.

To exit Nano, use CTRL + X.

Reboot the system

sudo reboot

Important network commands

Below are some of the useful network commands that can be used in most modern Linux distributions, including Linux Mint.

| Command | Description |
| ip | This command is a multipurpose command for network configuration. It can be used for displaying, configuring, and managing network interfaces, routing, and addresses.Example 
ip link

Ip addr show

 |
| ipconfig | Despite being deprecated, ifconfig is still widely used for basic network interface configuration and display. However, it is recommended that you utilize IP instead.Example 
ipconfig -a

 |
| ping | The “ping” command is a powerful tool that allows users to check the status of their internet connection and diagnose network-related issues.Exampleping google.com |
| traceroute or tracepath | tracepath is used to trace the path to the destination and discover MTUs along the way.Exampletracepath -n www.google.com |
| netstat | This command shows network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.Examplenetstat –nao |
| ss | Similar to the netstat command, ss is a useful tool for investigating sockets, network connections, and routing tables.Exampless –tuln |
| nmap | A network scanning tool is used to discover hosts and services on a computer network.Examplenmap -sP 168.12.1.0/24 |
| dig | The dig command in Linux is used to retrieve Domain Name System (DNS) information.Exampledig google.com |
| tcpdump | tcpdump is a command-line tool that captures and analyzes network traffic flowing through your system. It is commonly used to debug network issues and as a security tool.Example 
tcpdump -i eth0

 |
| ethtool | ethtool is used to query and control network device driver and hardware parameters, primarily for wired Ethernet devices.Exampleethtool eth0 |
| iwconfig | The iwconfig command is used to configure and display information about wireless network interfaces. Exampleiwconfig wlp0s20f3 |
| arp | Displays the current ARP cache entries, showing the IP addresses and their corresponding MAC addresses.Examplearp –a |

These are some of the most useful commands for network troubleshooting, monitoring, and configuration on Linux systems like Linux Mint. Understanding their use and options might assist you with managing and diagnosing network issues.

Finally, learning network management on Linux Mint is critical for maintaining a stable and efficient computing environment. Administrators can optimize network performance and handle connectivity issues by understanding fundamental concepts like IP configuration and network interfaces. Users can successfully maintain and improve their network configurations by employing tools and commands for network diagnostics, service management, and communication security.

Chapter 19              

Monitoring System Resources

System monitoring is the ongoing activity of keeping an eye on and evaluating different parts of a computer system to make sure it is secure, performing as intended, and operating correctly. It entails employing hardware or software components used to monitor system resources to gather data on important metrics including CPU consumption, memory usage, disk I/O, network traffic, and system uptime, among others.

There are multiple uses for system monitoring:

Performance Monitoring

Through the process of monitoring system resources, you can pinpoint apps or processes that are using up too much RAM, CPU, or disk I/O. This enables you to adjust your system or application's performance to maximize its efficiency.

Problem Solving

Determining and fixing system problems is made easier with an understanding of resource utilization. For example, monitoring tools can help identify whether a computer’s delayed response is triggered by a high CPU load, low memory, or other resource limitations.

Capacity Planning

Consistent observation yields data throughout time, which is often essential for capacity planning. As part of a continuous capacity planning program, system capacity is monitored. Long-term resource monitoring is used in capacity planning to calculate the rates of change in system resource usage. Knowing these rates of change allows for more precise long-term planning with reference to the acquisition of more resources.

Security Monitoring

Monitoring tools can also be useful in spotting anomalous behavior, such as sudden increases in network traffic or strange processes that are using resources, that may point to a security breach. Additionally, it displays data on successful and unsuccessful login attempts, root login successes and failures, deleted and created user accounts, sudo attempts, and the total number of services.

A variety of third-party and built-in tools are available in Linux Mint to track different system metrics. These tools accommodate a variety of tastes and requirements, from graphical programs that display data in an easy-to-understand manner to command-line utilities that offer comprehensive performance measurements.

Check the disk usage

When using a system, it's essential to keep an eye on disk usage to ensure optimal performance and prevent running out of space. Linux offers multiple ways for you to check disk usage:

One of the options is the graphical program known as Disk Usage Analyzer (Baobab). In order to start the "Disk Usage Analyzer":

*   Click the Mint Menu button.

*   To launch, select "Disk Usage Analyzer" from the Administration category.  

![](image_rsrc4E6.jpg)

The opening window displays summaries of all devices attached to the system.

*   Click any device to view details for all directories. 

*   You can delve deeper into directories to discover their sizes and subdirectories.

*   The graphical view on the right allows you to quickly identify huge files or folders that may be taking up a lot of space.

*   The graphical display can be switched between ring chart and tree map chart.

![](image_rsrc4E7.jpg)

*   You can also scan individual folders. Click on "Scan Folder" from the menu to choose the location you want to analyze.

![](image_rsrc4E8.jpg)

Using Command Line Tools

Linux also provides   a wide range of command-line tools to monitor disk. Here are some of the more often used ones:

Using the df command

The df command displays information about the total and available space on a file system. This command retrieves the information from `/proc/mounts` or `/etc/mtab`. By default, df command shows disk space in Kilobytes (KB). You can use the options to display size in MBs or GBs. The most commonly used option is the -h option, which makes the output human-readable by utilizing units like GB and MB.

Open the terminal, type df -h, and click Enter.

df –h

![](image_rsrc4E9.jpg)

Using the du command

The du (disk usage) command is a useful tool for estimating and reporting the disk space used by files and directories.

Syntax

du /path/to/directory

Example

Use the -h option to display sizes in KB, MB, or GB, which will make the output easier to read.

du –h /media/user1/DATA/

To get a summary of disk usage in human readable format:

du -sh /usr/

Using lsblk command

The lsblk (list block devices) command displays a complete overview of your system's block devices, including hard drives, SSDs, partitions, and USB drives. It's excellent for analysing the structure of your disks, including their sizes, kinds, and mount points.

Syntax

lsblk [options] [device]

Example

lsblk

![](image_rsrc4EA.jpg)

Check memory usage

It's critical to keep an eye on memory use to make sure your computer has enough resources to run apps efficiently and prevent crashes or slowdowns.

Linux Mint provides both graphical and command-line tools to monitor memory. The system monitor is a graphical application that allows you to easily monitor memory use and other system resources, including CPU load and disk activity, without the need for command-line functions.

System Monitor

To launch System monitor:

1.  Click the Mint Menu button.

2.  To launch, select "System Monitor" from the Administration category.

Three tabs appear when system monitor opens: filesystems, resources, and processes. The description for each tab is given below:

Resources Tab

The Resources Tab displays a high-level summary of your system's resource utilization, which includes CPU, memory, and disk activities. It shows real-time graphs of CPU load, memory consumption, and disk I/O.![](image_rsrc4EB.jpg)

Processes Tab

The Processes Tab displays a list of all currently active processes, including their process ID (PID), user, CPU use, memory consumption, and other information. It allows you to sort processes based on various parameters (such as CPU or memory utilization) and search for specific processes. To sort, select the required column header.

![](image_rsrc4EC.jpg)

File Systems Tab

The File Systems tab displays information about mounted file systems, such as their utilization, available space, and mount points. It's useful for tracking disk space utilization and detecting full partitions.

![](image_rsrc4ED.jpg)

Display memory usage using command line

The free command is a Linux program that may be used to check for memory RAM on your system or to view the memory statics of the Linux operating system. To check your system's memory use, run the free command with the -m or -g options for outputs in MB or GB, respectively.

sudo free –m

Other useful command line tools

There are numerous other command line tools that can be extremely useful while monitoring a system. These tools are not limited to statistics for a single resource, but can be applied to several resources. Let's look at some of the most popular tools that can be utilized with Linux Mint and other Linux variants. 

Top

Top command line tool presents a versatile utility for real-time system monitoring. To view real-time system resource utilization, including CPU, memory, and process information, open a terminal and enter the following command:

sudo top

htop

It is an enhanced version of the top command, offering more features and a more user-friendly interface. While "top" gives you basic information about a process, including its ID, CPU and memory utilization, and status, "htop" gives you more information about the process, like who started it, what command was used to start it, and when it started.

htop

Vmstat

The vmstat command-line utility displays a variety of system statistics. The information presented includes memory, paging, processes, IO, CPU, and disk scheduling.

Syntax

vmstat [delay [count]]

delay: delay between updates in seconds.

count: number of updates.

Example

# vmstat 1 5

The above command will display the vmstat output five times every one second.

Network

Netstat

The netstat command provides network status and protocol statistics. You can display the status of TCP and UDP endpoints in a table format, routing table information, and interface information. To inspect network connections and routing tables, use netstat. For more precise information, add flags like -a or -t.

Example

# netstat –a

SS

One of the most useful commands in Linux for inspecting sockets is ss, or socket statistics. Knowing how to utilize the ss command is essential for incident responders analyzing network connections and data, particularly when observing and investigating possibly malicious activity. Enter ss command with options to filter output

# ss -t

The command above only shows TCP sockets, which makes it easy to focus on a certain type of connections.

Disk

iostat

The iostat command in Linux monitors system input/output data as well as CPU consumption for devices and partitions. It is handy for tracking disk performance and throughput. This will help to identify high disk utilization. If iostat is not already installed, run the following command to do so.

sudo apt install sysstat

Example

iostat -x

The above command displays detailed statistical information.

Overall System Monitoring tool

You can use nmon, an interactive monitoring program that shows CPU, memory, network, and disk consumption. Press different keys to see different statistics.

If nmon is not already installed on the system, you can install it using the apt command:

# apt –S nmon

Now you can run the nmon command.

# nmon

These are some of the most essential monitoring tools, but if you want more advanced functionality, you may always install the following tools:

*   Conky

*   Prometheus

*   Ganglia

*   Sematext

*   Zabbix

*   Elastic Stack

*   ManageEngine

System monitoring is an important aspect of system administration. The tools mentioned in this chapter provide comprehensive insights into system resources, network activity, and I/O performance, allowing users to monitor and optimize system performance effectively in Linux Mint environments. Users have a variety of alternatives to select from based on their monitoring needs, whether they are using command-line utilities for rapid checks or graphical tools for in-depth examination of the system as part of system diagnostics. In a nutshell "prevention is better than cure".

Chapter 20              

Firewall

A firewall in Linux is a software-based network security system that monitors and regulates incoming and outgoing network traffic in accordance with established security rules. It serves as a barrier between a trusted internal network and untrustworthy external networks, such as the internet.

The UFW (Uncomplicated Firewall) is used to manage firewall in the Linux Mint operating system. GUFW provides a graphical interface for managing UFW. It simplifies the process of configuring firewall rules with an easy-to-use interface. To launch GUFW, open the Mint Menu and select "Firewall Configuration" from the Preferences category. It will request you for a password for authentication.

![](image_rsrc4EE.jpg)

Here is a basic interface overview:

Status: Turn the firewall on or off.

Rules Tab: Use the graphical interface to add, modify, and delete rules.

Rules Tab: Use the graphical interface to add, modify, and delete rules.

Profiles

Profiles are a collection of predefined firewall rules or configurations that simplify the management of files. Profiles give varying levels of security and network management based on common scenarios.

GUFW provides certain preconfigured profiles.  These profiles automatically create rules that allow or deny traffic on specified ports and protocols, making it easy to secure your system for popular services such as OpenSSH, HTTP, and HTTPS. The preconfigured profiles on GUFW are:              

Home This profile allows outgoing connections and denies incoming connections. It allows all outgoing connections and only necessary incoming connections from services like SSH or web connections.

Office You mostly trust the other computers on your network. Only selected incoming connections are accepted. For use at work areas.

Public The most restricted profile blocks all incoming connections while allowing all outgoing ones. Use this profile when connecting to a public Wi-Fi network to safeguard the system against threats.

In addition to the three basic profiles, you can manage rules and create custom configurations that function as profiles. To build a custom or remove an existing profile, follow these steps:

1.  Go to Edit -> Preferences.

2.  Click the plus button (+) to add a new profile.

3.  Locate the new profile in the list. Double-click the name to enter a custom name for the profile.

![](image_rsrc4EF.jpg)

Once a new profile is created, you can add rules to it.

Add new rule

To add a new rule, do the following:

1.  Select the profile for the rule.

2.  Select the Rules tab.

3.  Click the plus (+) button to open the firewall rule window.

The "Add a Firewall Rule" window consists of three tabs, the descriptions of which are provided below:

Preconfigured

The easiest and most user-friendly method for adding new rules. This allows you to add rules depending on predefined services. A service includes a set of preconfigured local ports, protocols, and destinations.

![](image_rsrc4EG.jpg)

Simple

A quick and simple method for adding a firewall rule with additional options Include rules based on services and port.

Advanced Allows total control over the rules for controlling traffic from specific IP addresses, subnets, and interfaces.

Using one of these tabs, you can easily define new rules for your customized profile.

Conclusion

GUFW provides an intuitive graphical interface for setting firewall rules on Linux Mint, making network security simple to manage. It makes it easier to create, remove, and configure firewall rules by using predefined profiles. GUFW is ideal for those who prefer a simple approach to firewall control and is appropriate for basic to intermediate installations.

Chapter 21              

Process Management

Every task done by the Linux OS has a process associated with it. A task may consist of one or more processes. In the simplest terms, a process is an executed program. Further processes are executed in the form of threads. A thread is the basic unit to which the operating system allocates processor time. The idea is to achieve parallelism by dividing a process into multiple threads. The primary difference between a process and a thread is that threads within the same process run in a shared memory space, while processes run in separate memory spaces. Processes have the following properties:

*   The context switches on them determine the priority of the process.

*   Each process provides the required resources to execute the program.

*   Each process starts with a single thread known as the primary thread.

*   A process can have multiple threads.

Here's an overview of some essential characteristics of Linux processes:

*   Process state

*   Process identification

*   Process control

*   Process prioritization

*   Process synchronization

*   Process management

*   Process creation

Process state

The Linux process can have various states. These states define what you can do with that process:

*   Running & runnable: When a new process starts, it is placed in the running or runnable state.

*   Sleeping: Waiting for another process to complete (such as an I/O operation).

*   Stopped: Suspended or halted.

*   Zombie: intermediate state after completion of execution but still has an entry in the process table.

Process identification

A Process ID (PID) is a unique identifier assigned to each active process in an operating system. Each process has its own process ID (PID) and works in a separate memory space. It separates concurrent processes, making them easier to manage and allocate resources.

Process control

The Linux operating system has various tools for controlling foreground and background processes. One of the most popular tools is the shell, which provides a command-line interface to the operating system. The shell allows the user to initiate, terminate, pause, and restart front and background processes. Here's how you can manage processes in both modes:

Foreground Processes

A foreground process is any command or task you run directly and wait for it to complete, or you can manually stop it. 

1.  Start a Foreground Process

To start a foreground process, you just run a command or script on the command line.

Example

cp asp.txt /home/.

2.  Pause a process

You can pause a running foreground process by pressing the Ctrl +z key on your keyboard. This will suspend the process and put it in the background.

3.  Resume a paused foreground process

To resume suspended processes from the background, enter the fg command followed by the job number. You can get the job number with the jobs command.

Syntax

fg %[job_id]

Example

fg %1

Background Process

Background processes are processes that run behind the scenes. Unlike a foreground process, the shell does not have to wait for a background process to finish before it can run more processes. The maximum number of processes that can run in the background depends on the amount of available memory.

1.  Start a background process

You can use “&” sign after the command to send the process to background.

Example

ping 8.8.8.8 > /dev/null &

2.  List background processes

Use the jobs command to list background processes.

jobs

3.  Bring the command to the foreground

To bring the background process back to the foreground, use the fg command.

Syntax

fg %[job_id]

Example

fg %1

Terminate process

If you are running a command in the terminal and want to stop it, use Ctrl + c on your keyboard.

Using command line tools

You can use command line or GUI tools to end a process initiated by you or another user, whether it's running in the foreground or background. Here's an overview of some of the most important commands for terminating processes.

Kill

The kill command sends signals to processes. It can be used to end processes graciously or forcefully.

Syntax

kill [options] <PID>

Example

kill %22

You can specify the signal to send. If no signal is specified, SIGTERM (15) is sent by default.

| Signal Name | Signal Number | Action |
| SIGTERM | 15 | Terminate (gracefully) |
| SIGKILL | 9 | Terminate (forcefully) |
| SIGINT | 2 | Interrupt |
| SIGHUP | 1 | Hangup |
| SIGSTOP | 19 | Stop (pause) |
| SIGCONT | 18 | Continue (resume) |

Terminate a process gracefully

Syntax

kill PID

Example

kill 44

Terminate a process forcefully

Syntax

kill -9 PID

Example

 sudo kill -9 44

Pkill command

To terminate a process, use the command pkill, followed by its name. In this command, you use the process name instead of the process ID.

Syntax

pkill command_name

Example

pkill -9 my_script

Detach processes from the terminal session.

Every command in Linux launches a process, which is automatically terminated when the user logs out or exits the terminal. You can use the disown and nohup commands to prevent the system from terminating your process when you close your shell or log out.

nohup

nohup, which stands for "no hang up," is a command that allows Linux systems to continue running programs even after closing the shell or terminal.

Syntax

nohup command &

Example

 nohup ./myscript.sh &

Disown command

The other way to continue running programs even after closing the shell is to detach a background command from your shell by using the disown command.

Syntax

disown [options] [job]

Example

 disown %1

Process concepts

The following are the concepts associated with the process that you should be aware of:

Init

Init is the first process that starts when the system boots and runs until the system is shut down. It automatically becomes the parent or grandparent of all of the processes that start on your Linux system. It also automatically adopts all orphaned processes. The kernel starts Init process during booting; if the kernel is unable to do so, a kernel panic will happen. PID 1 or Process ID 1 is assigned to Init process.

Daemon process

A daemon is a background service process that monitors the system or provides functionality to other processes. The system loads several daemons to ensure proper system operation. For example, the chronyd daemon is used by system to sync time and date. The letter d at the end of the process name typically identifies a daemon process, such as chronyd, dhcpd, or httpd.

User process

A process executed by a Linux shell is referred to as a user process, also called an interactive process like ls command at the command line. User processes also include processes that you start when you are in a graphical user interface, such as when you launch the Firefox web browser.

Parent and child processes

Any process that initiates or spawns another process is referred to as a parent process. A child process is one that is started by another process. A parent process has complete control over all of its child processes. For example, if you start Firefox, you can use the ps command to see how many processes it has started. Each of these processes is known as a child process.

The ps command

The ps command is used to generate a list of all processes that are currently running on a system and display extra details about each one.

To list all process running on the system.

ps –ef

Example

# ps -ef

UID         PID   PPID  C ​STIME ​TTY     TIME ​​CMD

root          1       0        2 ​16:11 ​?        00:00:03 ​​/usr/lib/systemd/systemd root          2       0        0               16:11              ?       00:00:00                            [kthreadd]

root          3       2        0 ​16:11 ​?        00:00:00 ​​[rcu_gp]

root          4       2        0 ​16:11 ​?        00:00:00 ​​[rcu_par_gp]

root          5       2        0 ​16:11 ​?        00:00:00 ​​[kworker/0:0-events]

root          6       2        0 ​16:11 ​?        00:00:00 ​​[kworker/0:0H-

The ps -ef command output shows the following columns: 

| UID        | Username |
| PID | Process ID |
| PPID | Parent Process ID |
| C | CPU utilization by the process |
| STIME | Start Time |
| TTY | Terminal |
| Time | Total CPU time used by the process |
| CMD | Command |

Display all processes for all users

# ps aux

Show all processes that belong to a specific user.

Syntax

ps U username

Example

sudo ps U shiv

List the details of a particular process using the process id.

Syntax

ps -l PID

Example

sudo ps -l 97

Find Parent Process ID (PPID)

You occasionally need to know the parent process of an active process. This is typically necessary when a process is using the machine excessively. There are two primary methods for determining the PPID of an active process:

•                    pstree command

•                    ps command

pstree

The pstree command, a command-line tool, displays active processes as a tree.

Syntax

pstree -p

You can check the parent process with the ID of any process in this tree.

Syntax

pstree -sp pid

Example

# pstree -sp 1043

The pstree command can also be used with a username to display all processes that the user has started.

Syntax

pstree username

Example

# pstree shiv

Process scheduling

The scheduler is part of the kernel, which selects the process to run next. The purpose is to run the processes according to their priorities. The nice and renice commands aid in the execution process by changing the scheduling priorities.

The nice command allows you to set the priority of a new process, whereas the renice command can be used to modify the priority of an already running process.

The niceness of -20 is the highest priority, and the niceness of 19 is the lowest priority. A process's priority is by default set to 0.

Syntax

nice -n priority command

Example

# nice –n 19 cp –r /as /map

Display nice value of processes

# ps –al

or

# top

To change the priority of running process

Use the ps command to find the process ID before using the renice command to modify the process priority.

Syntax

renice –n new_priority PID

Example

sudo renice -n -5 2234

Note: To modify a process' priority to a higher one, you require administrator access.

To summarize, knowing process management is critical for comprehending the fundamental operation of current operating systems. Computing is built around processes, which orchestrate program execution and coordinate system resources. Understanding the process lifecycle, from creation to termination, as well as the various synchronization, communication, and scheduling techniques, provides insight into how operating systems manage concurrency, ensure data integrity, and maximize resource consumption.

Chapter 22              

User Permissions and Access Control

Linux is a multi-user operating system that can be accessed by many users simultaneously. Therefore, it becomes utterly necessary that users do not touch each other’s data. For the security and sanity of the data and system files, the operating systems deploy different types of security systems. Linux divides authorization into two levels.

•                    Ownership

•                    Permission

Ownership

Ownership defines who can access the file or directory. Every file is owned by a specific user (or UID) and a specific group (or GID).

Change ownership

The chown command can be used to change the ownership of a file or directory.

1.  List the owner and group of files and directories

To view the owner and group of files and directories, use the ls -la command.

# ls –la

Change the owner of a file.

Syntax

chown username  filename

Example

# chown user2 example.sh

To change the group ownership of a file or directory

You can use the chown or 'chgrp' commands to alter the group ownership of a file or directory.

Syntax

chown :group  filename

Example

sudo chown :data2 notes.txt

Using chgrp

Syntax

chgrp group file/directory

Example

sudo chgrp data2 notes.txt

Change the Owner and Group of a File

You can also change the group and owner of the file simultaneously.

Syntax

chown username:group  filename

Example

sudo chown shiv:data2 asp2

Recursively Change the file ownership

To recursively change ownership of the directory and its files.

Syntax

chown -R user:group directory

Example

sudo chown -R user2: /home/timetable

Permissions

There is a standard set of access permissions for all files and directories. Permission defines the action allowed on the file or directory. These actions, also known as "permission sets," are read, write, and execute. There are two ways to represent the permissions:-

•                    Symbol

•                    Numbers

Symbols

To represent the file permissions following symbols are used:

| Symbol | Permission |
| r | Read |
| w | Write |
| x | Execute |

Execute permission for a directory allows the user to access its contents.

Numeric representation of permissions

Numeric mode refers to the use of numbers to denote Linux file permissions. In numerical form, a three-digit value denotes specific file permissions (for example, 774). We refer to these as octal values. Owner permissions are represented by the first digit, group permissions by the second, and other user permissions by the third. Each permission has a numeric value assigned to it:

| Number | Permission |
| 1 | Execute |
| 2 | Write |
| 4 | Read |

To represent the net permissions, we can use the sum of numerical representations of permissions.

The chart of numeric and symbol permissions is shown below:-

| Sum | Symbol | Permission |
| 0 | - | No permission |
| 1 | --x | Execute permission |
| 2 | -w- | Write permission |
| 3 | -wx | Write and Execute permission |
| 4 | r-- | Read permission |
| 5 | r-x | Read and Execute permission |
| 6 | rw- | Read and Write permission |
| 7 | rwx | Read, Write and Execute permission |

Permission groups

Each file or directory has three permission groups. The scope of permissions for each file and directory is defined by these permission groups. The table below shows the permission groups and their scope.

| Permission | Symbol | Scope |
| Owner | u | By default user who creates the file or directory becomes the owner of the file or directory. |
| Group | g | Members of the group that owns the file or directory |
| Others | o | Grants permissions to other users. Practically, it means everybody else. |

Permission management command line

Use the chmod command to manage the permissions of files and directories.

Add permissions

Syntax

chmod +permssions filename

Example

chmod +x para.sh

This command will add execute permission to the file.

Remove permissions

Syntax

chmod -permssions filename

Example

# chmod -x para.sh

You can also add or remove multiple permissions at the same time. Below is an example of this:

# chmod +xw para.sh

Removing permissions for group

Syntax

chmod g-permission filename

Example

# chmod g-xw para.sh

Remove permission for others

Syntax

chmod o-permission filename

Example

# chmod o-xw para.sh

Like that, you can add and remove permissions for groups and others at the same time.

# chmod go-xw para.sh

Change permissions using numeric values

This is the most popular way to change permissions.

Syntax

chmod permissions filename

Example

# chmod 700 hello.txt

This will give all permissions to the user and remove all permissions from others and groups.

User file creation mode mask

The user's file creation mode mask (umask) variable determines how file permissions are configured for newly created files and directories. The umask command allows the user to define which permissions should be removed by default from the base permission value of newly created files or directories.

Check umask value

# umask

0022

First digit of the output is sticky bit, and the remaining digits represent the numerical permissions.

To change the current session umask value. 

# umask 0044

When setting umask, you can skip the sticky bit value and enter the new value in three digits.

Determine the net permissions

After applying the umask to determine the effective permissions, subtract the umask value from the default permissions. Here's how you can accomplish it:

*   Default value: The system default permission values are 777 (rwxrwxrwx) for folders and 666 (rw-rw-rw-) for files.

*   Umask Value: Determine the current umask value. Supposing the current umask value is 002.

*   Subtract: Now subtract the umask value from the default permissions.

Example

777 – 002 = 775 (rwxrwxr-x)

When you set the umask at the command prompt, it only affects that particular shell session and does not persist over reboots or new shell sessions. To set values permanently, you can set them system-wide or for specific users. To permanently enforce a system-wide default for all users, use the /etc/profile  file; for individual users, change the  ~/.profile or  ~/.bashrc file. 

Object types

The first column of the  ls -al  output shows the object type.

![](image_rsrc4EH.jpg)

Object types are listed below:

| Code | Object type |
| – | Regular file |
| d | Directory |
| l | Symbolic link |
| c | Character device |
| b | Block device |
| p | named pipe (FIFO). |
| s | socket. |

ACL

Access control lists (ACLs) provide an additional, more flexible permission mechanism. ACL allows you to grant permissions to any user or group on any file or directory. It extends the traditional Linux file permissions to provide more fine-grained control over access to files and directories.

An ACL can provide the following types of permissions: 

*   Permissions provided to particular users based on their usernames or user IDs are known as user-specific permissions.

*   Permissions designated for particular groups based on their group names or group IDs are known as group-specific permissions.

*   Newly created files and directories inside of a directory are subject to the default permissions.

To display the current ACL of a file or directory, we use the getfacl command.

Syntax

getfacl file / directory

Example

# getfacl hosts

The commands setfacl and chmod can be used to set or modify the ACL of a file or directory.

Syntax

setfacl [option] file_owner:file_permission filename

Where options are

| -m, –modify | Modify the ACL. |
| -x, –remove | Remove the permission. |
| -b, –remove-all | Remove all permission. |
| -d, –default | Apply default permissions to newly created files and folders. |
| -R, –recursive | Recursively apply modifications to all files and directories. |

Example

Set file permission to users on a specific file.

# setfacl -m u:user1:rw acct.txt

Remove all permission on a specific directory

# setfacl -x u:user1 acct.txt

In essence, file permissions provide users control over who can access their files and directories and are an important part of Linux operating systems. Users can guarantee the security and privacy of their data by comprehending the ideas of read, write, and execute rights for owners, groups, and others. In addition to safeguarding sensitive data, properly managing file permissions also contributes to the stability and integrity of the system. A thorough understanding of file permissions will enable users to maintain system security and make informed choices as they traverse and interact with their filesystems.

Final Thoughts

As we conclude our tour through Linux Mint, I hope this book has shed light on the powerful, user-friendly features that make this distribution an excellent choice for both novice and seasoned users. You've now mastered the fundamentals of installation and configuration, as well as advanced customization and troubleshooting, giving you the tools you need to fully utilize Linux Mint's capabilities.

Remember that the open-source community values curiosity and collaboration. As you continue to use and explore Linux Mint, don't be afraid to jump into forums, participate in debates, and share your own experiences. Every problem you face presents an opportunity to learn and improve.

Thank you for accompanying me on this voyage. May your Linux Mint journey be rich with exploration and efficiency.

Happy Linuxing
# **Hardware Configuration**

**CHAPTER 9**

# CHAPTER OBJECTIVES

+   - Reconfigure the X windowing system with automated utilities
- Determine when swap space needs to be increased
- Add and configure printers
- Install and configure add-in hardware

+   - Load, remove, and edit list modules
- Manage print spools and queues
- Create and manage local storage devices and file systems
- Download and install patches and updates

# ■ X WINDOWING SYSTEM

The X system is the GUI system for Linux and Unix. The current version is 11 release 6.6. It is most commonly called X11 or just X. You may also see it written as XWindows, which is incorrect, but gets the meaning across.

X is the foundation software for GUI interfaces. It provides functionality for the mouse cursor, drawing windows, and moving windows. X does not provide any other functionality, such as buttons, menus, or title bars. These windowing features are provided by other software.

X is based on a client/server model. The X server displays information on a graphical display and sends back user input from a keyboard or mouse. An X client is a program that relies on an X server for interaction. These programs usually run on the same computer, but they do not have to. An X client can connect to a remote X server relatively easily.

# The Video Adapter

Video cards basically accomplish the same task on any machine. They provide the hardware link from software that wants to communicate to a display device. Many different video adapters are available, and the type you have installed is not always easy to determine.

Video adapter manufacturers use a video chipset as the core of a video adapter. The chipset must be identified to the Linux kernel before a GUI can work. The video chipset can be discovered in a number of ways.

Linux will auto-detect the video card during installation in most cases. In some cases the video card cannot be detected. For example, if you have a new machine with the latest video chipset, Linux may not detect it.

If you are installing a new video card, you may have the manufacturer’s documentation. Or, if the card is a popular model, you will probably be able to find documentation online. If you have to search online for the video documentation, you need to know what chipset your card uses. Figure 9–1 shows a video chipset from nVIDIA. The information on the chip can be used when searching www.nvidia.com for a driver.

these BIOS-related limitations into account. However, if you decide to use fdisk instead, it is your responsibility to ensure that you keep these limitations in mind.

## A Note About Kernel Drivers

During installation of Red Hat Linux, there are some limits placed on the file systems and other drivers supported by the kernel. However, after installation there is support for all file systems available under Linux. At install time the modularized kernel has support for (E)IDE devices, (including ATAPI CD-ROM drives), SCSI adapters, and network cards. Additionally, all mice, SLIP, CSLIP, PPP, PLIP, FPU emulation, console selection, ELF, SysV IPC, IP forwarding, firewalled and accounting, reverse ARP, QIC tape and parallel printers, are supported.

Please Note: Because Red Hat Linux supports installation on many different types of hardware, many drivers (including those for SCSI adapters, network cards, and many CD-ROMs) are not built into the Linux kernel used during installation; rather, they are available as modules and loaded as you need them during the installation process. If necessary, you will have the chance to specify options for these modules at the time they are loaded, and in fact these drivers will ignore any options you specify for them at the boot: prompt.

After the installation is complete you may want to rebuild a kernel that includes support for your specific hardware configuration. See Building a Custom Kernel for information on building a customized kernel. Note that, in most cases, a custom-built kernel is not necessary.

## If You Have Problems...

If you have problems before, during, or after the installation, check the list of Red Hat Linux Frequently Asked Questions. You can find the FAQ at: http://www.redhat.com/knowledgebase/index.html In many cases, a quick check of the FAQ can quickly get you back in action.

## One Last Note

Please read all of the installation instructions before starting; this will prepare you for any decisions you need to make and should eliminate potential surprises.

## 3 Starting the Installation

This chapter explains how to start the Red Hat Linux 6.0 installation process. We’ll cover the following areas in this chapter:

- Getting familiar with the installation program’s user interface;
- Starting the installation program;
- Selecting an installation method.

By the end of this chapter, the installation program will be running on your system, and the appropriate installation method will have been selected.

## The Installation Program User Interface

The Red Hat Linux installation program uses a screen-based interface that includes most of the on-screen “widgets” commonly found on graphical user interfaces. They may look a little different than their more graphical counterparts; Figures 3-1 and 3-2 are included here to make them easier to identify. Here’s a list of the most important widgets:

- **Window** — Windows (also referred to as dialog boxes in this manual) will appear on your screen throughout the installation process. At times, one window may overlay another; in these cases, you may only interact with the window on top. When finished with that window, it will disappear, allowing you to continue with the window that was underneath.
- **Text Input** — Text input lines are regions where you can enter information required by the installation program. When the cursor rests on a text input line, you may enter and/or edit information on that line.
- **Check Box** — Check boxes allow you to select or deselect a particular feature offered to you by the installation program. When the cursor rests within a check box, pressing [Space] causes the check box to toggle between a selected and unselected state.

## The Installation Guide for Red Hat Linux 6.0

- Text Widget — Text widgets are regions of the screen that are devoted to the display of text. At times, text widgets may also contain other widgets, such as check boxes. It is possible that a text widget may contain more information than could be displayed at one time. In these cases, the text widget will have a scroll bar next to it; if you position the cursor within the text widget, you can then use the [uparrow] and [downarrow] keys to scroll through all the information available.

- Scroll Bar — Scroll bars provide a visual indication of your relative position in the information being displayed in a text widget. Your current position is shown by a # character, which will move up and down the scroll bar as you scroll back and forth.

- Button Widget — Button widgets are the primary method of interacting with the installation program. By “pressing” these buttons, you will progress through the series of windows that make up the installation process. Buttons may be pressed when they are highlighted by the cursor.

- Cursor — Although not a widget, the cursor is used to select (and interact with) a particular widget. As the cursor is moved from widget to widget, it may cause the widget to change color, or you may only see the cursor itself positioned in or next to the widget. In Figure 3-1, the cursor is positioned on the Ok button. Figure 3-2 shows the cursor on the first line of the text widget at the top of the window.

![](img/46f4935125ba89e12897afbe9d77a097_63_0.png)

# Figure 3-1: Installation Program Widgets

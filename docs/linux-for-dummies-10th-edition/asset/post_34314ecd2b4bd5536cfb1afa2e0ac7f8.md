
## Partitioning using Linux tools

If you're in a situation where you don't currently have Windows installed on the hard drive but would like to partition the hard drive first, you can use Linux tools to do the work for you. The easy solution is to boot your PC using a Live distribution and use the disk management tools available. Plenty of Live distributions include disk management tools by default, but by far the most popular is the KNOPIX Linux distribution.

The KNOPIX Linux distribution was the first to create a live Linux version, even back before there were DVDs (it was called a LiveCD!). What keeps KNOPIX at the top of the list of popular Linux distributions is the myriad of utilities it includes by default. It tours itself as a rescue disk — a way to boot your PC if things go horribly wrong with the existing operating system, and be able to troubleshoot and possibly fix issues.

Follow these steps to partition your hard drive using KNOPIX:

- 1. **Download the latest KNOPIX CD or DVD ISO image from the KNOPIX website at www.knopper.net.**
- 2. **Burn the ISO image onto a bootable CD, DVD, or USB stick using a standard ISO image burning tool.**

Jump to the “Creating a boot disk” section* for quick instructions on how to do this, then come back here.

- 3. **Boot your PC using the KNOPIX LiveDVD.**

At the *boot: prompt, press the Enter key to start KNOPIX.

- 4. **Select Graphical Programs  startxide from the main menu.**

The KNOPIX graphical desktop environment comes up. It’s a fairly bare-bones graphical desktop so it can run on just about any PC, but it gets the job done.

- 5. **From the KNOPIX graphical desktop, click the Terminal icon in the taskbar at the bottom of the desktop.**

A Terminal session starts that provides access to the command prompt (I talk more about that in Chapter 16).

- 6. **At the command prompt in Terminal, enter the command: sudo gparted.**

The GParted application is a popular disk management tool for Linux. It provides an interface similar to the Windows disk management tool, as shown in Figure 2-4.

![](img/577d3bff979ee86b07f9836e0df274ce_43_0.png)

FIGURE 2-4: The Linux GParted disk management tool main window.

![](img/577d3bff979ee86b07f9836e0df274ce_43_1.png)

FIGURE 2-5: The GParted Resize/Move dialog box.

- 7. **Right-click inside the partition you need to shrink.**
- 8. **Select Resize/Move from the pop-up menu.**

The Resize/Move dialog box opens, as shown in Figure 2-5.

- 9. In the Resize/Move dialog box, either drag the right end of the partition graphical box to resize the partition, or enter a new value in the New Size text box.

The colored portion of the box indicates where the existing data in the partition is stored. You should be able to move the end of the partition down close to that area.

- 10. Click the Resize/Move button to initiate the resizing process.

After the hard drive is partitioned you can exit the tool and shut down KNOPIX. And that’s all there is to it! After you’ve resized the partitions, you’re ready to move on to the next step in preparing your PC for Linux — checking your hardware, as described in the next section.

## Double-Checking Hardware Compatibility

If you’re installing Linux on hardware you already own, just give it a try and then see what doesn’t work. Parts of this section address fixing hardware problems in a general sense. In other chapters, more specific items such as sound cards (Chapter 13), wireless cards (Chapter 9), and so on, are addressed. So, if you run into trouble, start in the specific sections dedicated to particular tasks, and then come here for more general help if you still haven’t solved the problem.

The biggest hardware incompatibility problem areas are wireless network cards and the very latest whiz-bang multimedia hardware such as video cards and sound cards. You can check hardware compatibility lists before installing or purchasing new hardware, but they are of limited use because the hardware world changes so quickly.

If you’re interested in looking, first try the support website for your particular Linux distribution, such as the Red Hat Enterprise Linux listings at `access.redhat.com/ecosystem/search/~/category/` for the CentOS or Fedora distributions, or the Ubuntu listings at `certification.ubuntu.com/` for any of the Ubuntu distributions.

Keep in mind that hardware compatibility lists usually focus on business equipment instead of home items, so just because you don’t see something listed there doesn’t mean it won’t work.

![](img/577d3bff979ee86b07f9836e0df274ce_45_0.png)

Don't worry about items being *Certified* (heavily tested to make sure they work properly) or not. *Supported* and *Compatible* are fine most of the time for a home user. Ultimately, the best way to tell if a piece of hardware is supported is to do a web search. Many go to Google and do a web search on the make and model of the hardware, plus the word **Linux**. If specific drivers are required to support the hardware you can often find additional installation information by adding your Linux distribution name to the search. Such a search is likely to show you what problems and successes people have run into with that particular piece of hardware.

If even thinking about computer hardware gives you dizzy spells, don't worry, you can find plenty of information on the Internet. A great place to start is www.tomshardware.com. Other places to look for information on how various devices work in Linux include

- Other Linux-oriented websites: Quite a few websites are devoted to helping Linux users support hardware. The old standard was the generic Linux hardware list at www.tldp.org/HOWTO/Hardware-HOWTO/. More up-to-date websites are available, such as linux-hardware.org.
- Vendor websites: Many hardware vendors do support Linux, but they don't make it easy to find information about it. In general, search the vendor's forums (if they have them) for the piece of hardware, the FAQ for the hardware, or follow the Support links to look for downloads for Linux. Don't download what you find if there are downloads. The point is to look and see if they exist. The *driver* (the software that tells the operating system how to use the hardware) available for download might actually be included in your Linux installation. Only download the driver from the vendor if this is the only way you can get it.

![](img/577d3bff979ee86b07f9836e0df274ce_45_1.png)

If worse comes to worst, you might not find any information on the hardware in question involving Linux. However, again, this doesn't mean that the hardware won't work. Try it anyway if you already have the item. You find that it works fine. Or, you might not be able to use the very latest features, whereas the rest works just fine. (For example, with a latest-generation video card, the newest fancy features might not work, but you can still use it as a generic SVGA at the very least.)

- The dreaded manuals: When possible, keep your computer manuals (especially those for your video card and monitor) handy, just in case you need them to answer a question asked by the installer — most people don't have to deal with this at all, but some do.

### Laptop Considerations

The current distributions of Linux do very well on relatively new laptops. (See www.linux-laptop.net for an excellent research site on how Linux gets along with various makes and models.) If your laptop is a common brand, you shouldn't encounter any problems installing Linux. However, some laptops resort to exotic hardware to squeeze all those fancy features into such tiny boxes. Sometimes Linux won't work with the extra fancy features on those laptops, such as touch screens, clickable mouse pads, and keyboard lights.

If you plan to purchase a laptop for Linux, check out its hardware specs (such as network cards) to make sure they're not Windows-specific. If the built-in or default hardware for the laptop is Win-labeled (or you discover while researching the machine that it contains a Win product, even if it isn't properly labeled), you might be able to switch the offending hardware with an external device that plugs into the laptop using USB. Most current laptops contain at least one USB slot to give you a place to connect an external network card or sound card. As long as you stick with a common brand of external USB device, it should work well with Linux.

If you need to find out exactly what hardware is in your machine, you have the following options:

- Use an existing operating system to document your hardware. If your computer is already running Windows, you can collect a lot of information from the Windows environment. In Windows 10, right-click the Start menu icon in the taskbar, and then choose Device Manager. The Device Manager dialog box, shown in Figure 2-6, appears.
- Download a PC hardware-detect tool. Some hardware detection tools are also available on the Internet, such as Dr. Hardware. The Dr. Hardware tool contains lots of information about what's inside your machine. This tool is shareware, and the usage and fee information is available from the Gebhard Software website (www.dr-hardware.com/).
- Access the Basic Input/Output System (BIOS), or for newer PCs the Unified Extensible Firmware Interface (UEFI) information. Stored in a small area of memory and retained by a battery, this is sometimes referred to as CMOS (Complementary Metal-Oxide Semiconductor), which indicates the type of computer chip that can store and retain information. The amount of information stored in the BIOS or UEFI can range from very little to quite a lot. Some newer systems may display several screens of information about the computer's hardware.

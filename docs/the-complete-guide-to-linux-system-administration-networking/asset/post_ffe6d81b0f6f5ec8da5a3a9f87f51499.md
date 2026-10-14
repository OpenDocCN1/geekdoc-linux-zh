
9. Click Cancel to close the Communications Port (COM1) Properties dialog box. Choose File, then Exit to close the Device Manager. Click Cancel to close the System Properties dialog box.

10. Double-click the Display icon in Control Panel. (If you are using Category view, click the Back button, then click Appearances and Themes, then click Display.)

11. Click the Settings tab in the Display Properties dialog box.

12. Notice the number of colors and the resolution of your current Windows display. Linux can operate at the same level, or perhaps better (higher resolution or more colors), depending on what hardware you have on your computer.

13. Click the Advanced button in the lower right of the dialog box. The information shown depends on the type of video hardware installed in your computer. In many cases, an Adapter tab is available that contains detailed information about your video card, including the manufacturer, model name, and amount of video memory installed.

14. Use the Cancel button(s) to close all open dialog boxes so that you see only Control Panel again. Close the Control Panel.

## Project 8-2

In this project, you install the Fedora distribution. To complete this activity you should have an Intel- or compatible-based computer with a bootable CD-ROM drive. The computer should have a minimum of 32 MB of memory (Red Hat Software lists 256 MB as the minimum for Red Hat Enterprise Linux, but a minimal installation does not require that much memory). The installation requires between 510 MB and 6.3 GB of hard disk space. The packages groups marked in Table 8-4 require about 3.4 GB of hard disk space. See the notes in Table 8-4 if you do not have this much hard disk space available.

Installing Linux is the most involved project in this book. Because so many variations exist in available computer hardware, the steps you have to follow may differ slightly from the steps given in this project. Every effort has been made to alert you to important variations and prepare you to answer any questions that come up.

These steps assume that you are installing Linux on a desktop computer (not a laptop), on an IDE hard disk, and that you do not need additional special hardware drivers (though comments are provided regarding such drivers).

- 1. Insert the Fedora CD 1 in your CD-ROM drive and turn on your computer.
- 2. After a few moments, a welcome screen appears.
  a. Press Enter to immediately start the installation in graphics mode.
  b. If you have previously had trouble with the graphics mode, type the word text and press Enter.
  c. If you tried the installation previously and the system appeared to crash during the
start-up phase, you can try entering linux noprobe and pressing Enter. This prevents the installation program from probing hardware, which causes problems on a few systems.

3. Assuming that you pressed Enter without typing any text or simply waited, the system pauses for several moments, then probes your video card and monitor. After a few moments, the graphical installation program begins and you see the CD Found screen shown in Figure 8-19. (To reach this first screen after pressing Enter in Step 2, may take as much as four full minutes, depending on your computer's speed.)

![](img/43f64015de86d989e30eff5bb284fb96_409_0.png)

Figure 8-19 The CD Found screen

4. Because many people download Fedora or purchase CDs from download service companies, you have the option of validating your Fedora CDs in this first screen. This process takes several minutes—if you have not had problems with your CDs, you can use the Tab key to select Skip and press Enter to continue. If you are installing across a network, you do not see this screen. Instead, you need to enter information about how to access the installation sources on your local network. For example, you need to enter the IP address of the server where the files are located.

5. After the CD is tested (or when you skip that step), the first graphical installation screen appears. On the left side of the screen you see help text. You can review this area at any time during the installation to see detailed information on the choices presented at that point in the installation. A Release Notes button also has late-breaking information about the product that you should review.

On the lower-right side of the screen are two buttons labeled Back and Next. You use these buttons to navigate through the installation program, choosing Next to proceed to the following screen or Back if you wish to return to a previous screen to make a change or review something.

If you are using the text mode installation program instead of the graphical installation program (which is the focus of these steps), you see the Back and Next buttons. You can navigate between buttons using the Tab key.

If you are using the graphical installation program but your mouse does not work (it normally works immediately), you can use the Tab and Enter keys to choose the Next button; the fourth screen of the Installation program lets you configure your mouse correctly.

6. Choose the Next button to continue past the Welcome screen. The Language Selection window appears with a list of language options. Click on a different language than U.S. English if appropriate and then choose Next. The language changes immediately to match your selection.

7. The Keyboard Configuration window appears. If you are using a non-U.S. keyboard or a special keyboard such as a Microsoft Natural keyboard, select the appropriate items for your keyboard. Choose Next to continue.

8. The Mouse Configuration window appears. (Figure 8-20) Your mouse is probably already working, but you can select your model from the list shown if it was not correctly auto-detected and highlighted. If the mouse model you select uses a serial port interface, you can then select the appropriate serial port in the box below the list of mouse models. The list includes both the Linux device name (on the right) and the better-known port name (on the left). Click on the appropriate line to select it.

You may want to also select the Emulate 3 buttons check box at the bottom of this window. Some functions in Linux use the middle button of a three-button mouse. If you are using a two-button mouse, checking this box causes Linux to act as if you pressed a middle mouse button anytime you press both mouse buttons at the same time. Click Next to continue.

If your mouse was not working when you first saw the Mouse Configuration window, it should begin working when you click Next. If it does not, use the back button on the following screen to return to the Mouse Configuration screen and reconfigure your mouse.

> NOTE Depending on the type of monitor you are using, you may see a Monitor Configuration window after the Mouse Configuration window. Review the information on this screen, but in virtually all cases, the default information shown is acceptable and you can simply click Next to continue.

![](img/43f64015de86d989e30eff5bb284fb96_411_0.png)

# Figure 8-20 The Mouse Configuration window

9. If you are installing Fedora on a system where Fedora has already been installed, the Upgrade Examine window appears. Although you could select the Upgrade an existing installation option, choose the Install Fedora Core option to perform a complete installation from scratch. Click Next to continue.

10. The Installation Type window appears. (See Figure 8-21.) Selecting Personal Desktop, Workstation, or Server makes the installation simpler. But to help you learn more, select Custom so that you will be shown a list of package groups to select from later on. Click Next to continue.

11. The Disk Partitioning Setup window appears. (See Figure 8-22.) This window tells you that the installation program can automatically set up partitions on your system or let you determine manually how Linux will be installed. If you were installing Linux on a new computer or one with no valuable data on its hard disks, the automatic option makes installation very easy. But once again, to learn more, select the second item, Manually partition with Disk Druid. Then click Next to continue.

12. The Disk Setup window appears. The top part of the screen shows a representation of your hard disk as a horizontal bar divided into labeled partitions. The bottom part of the screen lists partitions by their Linux device names (such as /dev/hda1) and also gives their sizes, partition type, and other information. Between these two areas of the window are buttons you can use to set up partitions.

  a. If you feel at any time that you have become confused or selected the wrong thing, click the Reset button. The partition table will be reread from the hard disk. Nothing is written to the hard disk until you click the Next button and confirm your partition changes.

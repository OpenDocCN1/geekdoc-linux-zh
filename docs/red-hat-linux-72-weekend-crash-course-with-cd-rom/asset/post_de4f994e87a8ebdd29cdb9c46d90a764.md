
## Troubleshooting the Red Hat Linux Installation

**Session Checklist**

- ✓ Installing Red Hat Linux in text mode
- ✓ Installing Red Hat Linux in expert mode
- ✓ Configuring the X Window System
- ✓ Configuring printers
- ✓ Getting help with the Red Hat Linux installation

**T**his session discusses methods for solving the most common installation and configuration problems. In most cases, the Red Hat Linux installation program, Anaconda, works just fine, correctly detecting and configuring key hardware components, such as SCSI controllers and network cards. However, if Anaconda cannot detect or configure a component properly, it skips that step. For example, if Anaconda fails to detect the network card correctly, it skips the network configuration step. The installation program also tries to simplify the installation by skipping some system configuration steps such as setting up a printer. You can recover from most of the installation and configuration problems because there are other ways to configure these tasks. This session also lists some of the resources available if you encounter installation problems you cannot solve.

**30 Min. To Go**

### Installing Red Hat Linux in Text Mode

The Red Hat installation program attempts to use a minimal X Window System to display the graphical user installation screens. If the program fails to detect a video card, X does not start. If, for any reason, X fails to start, you can always fall back on the older text mode installation program to configure the video card manually. You can also use the text mode installation if you are comfortable with the older installation program.

To use text mode installation, type `text` at the `boot:` prompt after booting the Red Hat Linux installation CD. From then on, the basic installation procedure resembles the graphical installation described in Section 1, but small details differ. In particular, you cannot use the mouse and you will need to enter some configuration values manually that Anaconda handles automatically during a graphical installation. If you collected the hardware information described in the section “Checking if Red Hat Linux Supports Your PC Hardware” in Session 1, you should have no trouble responding to the prompts and performing the installation.

In text mode, when the installation program fails to detect the video card, it displays a list of video cards. Select one video card from the list. Because of your help in selecting the video card, X may work when you install in text mode. If it does not, you can configure X using the information in “Configuring the X Window System,” later in this session.

![](img/5fe8f856723cde0b366f73584b9e64b8_37_0.png)

In some cases, using the text mode installation will allow you to install Red Hat Linux on systems containing hardware not specifically mentioned in Red Hat’s hardware compatibility lists. Sometimes, selecting similar hardware options for unsupported hardware may even work. These are not supported or recommended options, however, nor do they always work.

To see how the Red Hat installation program detects certain devices, you can also look at the messages the installer’s kernel displays while it boots. To view these boot messages, press Ctrl+Alt+F4 to switch to a text-mode virtual console where the messages appear. A virtual console is a screen of text or graphical information stored in memory that you can view on the physical screen by pressing the appropriate key sequence (Shift+PageUp to scroll up and Shift+PageDown to scroll down). Look for messages that relate to the device in question. If all else fails, you can specify certain devices manually by running the installation in expert mode, discussed next.

### Installing Red Hat Linux in Expert Mode

The expert mode installation enables you to control almost the entire installation process. Other installation modes hide some of the installation steps and use autodetection, and default values for hardware configuration.

To run the installation in expert mode, follow these steps:

1. Type `expert` at the `boot:` prompt in the initial text screen that appears during the Red Hat Linux installation. The installation program then displays another text screen that asks for a driver disk, if you have one.
2. Your hardware vendor may provide a floppy disk containing Linux drivers. If you have one, press Enter and a dialog box prompts you to insert the disk into the A: drive. After you do so, press Enter, and the installation program loads the driver and guides you through the steps necessary to install the driver.
3. If you do not have a driver disk, select None. The installation program then goes through two more screens in which you select the language and the keyboard layout. Then the installation program prompts for the media containing the packages to be installed.
4. Next, the installation program displays a dialog box that gives you another opportunity to add devices. Press Tab to highlight the Add Device button, and then press Enter. The installation program then displays a dialog box that prompts for the type of device (SCSI or Network).
5. If you have any SCSI device, such as a SCSI hard drive, select SCSI and press Enter. Then, the installation program displays a list of SCSI controllers from which you should select the one on your system and press Enter. The installation program then loads that driver module.

The SCSI driver automatically probes and determines the SCSI controller's settings, such as interrupt request (IRQ) and I/O port address. If the driver has problems detecting the SCSI controller's settings, you can specify these parameters manually. To do so, select the checkbox labeled Specify module parameters and press Enter. The installation program then prompts you for the module parameters.

6. You can then enter a line such as `aha152x=0x340, 11,7` to specify the parameters for the driver module. (See the sidebar “Specifying SCSI Controller Settings,” later in this session, for more information on these settings.)
7. After you add any SCSI controllers, you return to the dialog box that enables you to select a device type. You can add network cards from this dialog box as well. In the dialog box, select Network from the list and press Enter. The installation program then displays a list of network cards from which you can select your network card.

When you press Enter, the installation program loads the driver module for the selected network card. That driver probes and determines the network card settings.

8. Once you return to the screen from which you select a SCSI or network device, select Back and press Enter. This takes you to the dialog box that asks you about adding devices. Select Done and press Enter. The installation program then switches to graphics mode and guides you through the rest of the installation, as explained in Section 1.

### Specifying SCSI Controller Settings

If you have a SCSI controller in your system, the Red Hat installation program loads a SCSI driver module for that controller. You have to identify the type of SCSI controller (such as Adaptec 1542 or Adaptec 2940). The installation program attempts to determine the controller settings, such as IRQ and I/O port address, by probing various I/O port addresses. However, if the installation program fails to determine the SCSI controller settings, you have to specify these parameters — IRQ and I/O address — as options for the driver module. The exact formats of these options vary from one module to another. For example, the driver for an Adaptec AHA 152x card accepts the options in the following format:

```
aha152x=IOPORT,IRQ,SCSI_ID[,Reconnect,Parity]
```

where `IOPORT` is the I/O port address. `IRQ` is the interrupt request number, and `SCSI_ID` is the SCSI ID of the SCSI controller. The last two items are optional. A typical module option for the aha152x module might be:

```
aha152x=0x340, 11,7
```

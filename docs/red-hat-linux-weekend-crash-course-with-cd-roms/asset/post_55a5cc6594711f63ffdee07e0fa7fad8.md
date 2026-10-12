
## REVIEW

In this session, you continued with the Red Hat Linux installation steps that you started in the previous session. The installation program enabled you to configure a number of items including the Linux Loader (LILO), the LAN, the time zone, and the password of the root user. Then you selected the package groups to install and configured the X Window System. After that, the installation program took over — it formatted the disk partitions and copied all necessary files from the CD-ROM to the disk. You also prepared a boot disk for use in emergency when LILO fails to boot Red Hat Linux.

## QUIZ YOURSELF

- 1. What is LILO and what does it do? (See “Install LILO”.)
- 2. What is the root user? (See “Set the root Password and Add User Accounts”.)
- 3. What parameters do you have to specify in the Network Configuration screen? (See “Configure the Network”.)
- 4. What happens if you do not select any package groups to install? (See “Selecting the Package Groups to Install”.)
- 5. What parameters do you have to specify if the installation program cannot correctly detect your monitor? (See “Completing the Installation”.)

## SESSION

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_68_0.png)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_68_1.png)

## Troubleshooting the Red Hat Linux Installation

### Session Checklist

- ✓ Installing Red Hat Linux in text mode
- ✓ Installing Red Hat Linux in expert mode
- ✓ Configuring the X Window System
- ✓ Configuring printers

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_68_2.png)

In the last three sessions, you installed Red Hat Linux from this book’s companion CD-ROMs. The Red Hat Linux installation program attempts to automatically detect key hardware components such as a SCSI controller and network card. Based on the detected hardware, the installation program takes you through a sequence of steps to configure the detected hardware. For example, if the installation program fails to correctly detect the network card, it skips the network configuration step. The installation program also tries to simplify the installation by skipping some system configuration steps such as setting up a printer. You can recover from most of the installation and configuration problems because there are other ways to perform these tasks. This session shows you several troubleshooting approaches for some common installation and configuration problems.

### Installing Red Hat Linux in Text Mode

The Red Hat installation program attempts to use a minimal X Window System (X) to display the graphical user installation screens. If the program fails to detect a video card, X does not start. If — for this reason or any other reason — X fails to start, you can always fall back on the older text mode installation program to specify the video card manually. You can also use the text mode installation if you are comfortable with the older installation program.

To use text mode installation, type text at the boot: prompt after you start the PC from the Red Hat Linux boot floppy. From then on, the basic sequence is similar to that of the graphical installation described in Session 2. However, many small details are different. You should be able to respond to the prompts and perform the installation.

In text mode, when the installation program fails to detect the video card, it displays a list of video cards. Select one video card from the list. Because of your help in selecting the video card, X may work when you install in text mode. If it does not, you can configure X using the information in the “Configuring X” section later in this session.

### Installing Red Hat Linux in Expert Mode

If the Red Hat installation program does not detect your SCSI controller or network card, you can specify these devices manually by running the installation in expert mode. Look for any indication of SCSI or network devices in the messages displayed by the Linux kernel as it boots. To view these boot messages, press Ctrl+Alt+F4. This switches to a text-mode virtual console where the messages appear. A virtual console is a screen of text or graphical information stored in memory that you can view on the physical screen by pressing the appropriate key sequence.

To run the installation in expert mode, type expert at the boot: prompt in the initial text screen that appears during the Red Hat Linux installation. The installation program then displays another text screen that asks for a driver disk, if you have one.

Your hardware vendor provides a floppy disk with Linux drivers. You insert that floppy into the A: drive. If you have that disk, press Enter and a dialog box prompts you to insert the disk into the A: drive. After you do so, press Enter, and the installation program loads the driver and guides you through steps necessary to install the driver.

If you do not have a driver disk, select Cancel. The installation program then goes through two more screens in which you select the language and the keyboard layout. Then the installation program prompts for the media containing the packages to be installed.

Next, the installation program displays a dialog box that gives you another opportunity to add devices. Press Tab to highlight the Add Device button and then press Enter. The installation program then displays a dialog box that prompts for the type of device — SCSI or Network.

If you have any SCSI device, such as a SCSI hard drive, select SCSI and press Enter. Then, the installation program displays a list of SCSI controllers from which you should select the one on your system and press Enter. The installation program then loads that driver module.

The SCSI driver automatically probes and determines the SCSI controller’s settings, such as interrupt request (IRQ) and I/O port address. If the driver has problems detecting the SCSI controller’s settings, you can specify these parameters manually. To do so, select the check box labeled Specify module parameters and press Enter. The installation program then prompts you for the module parameters.

You can then enter a line such as aha152x=0x340,11,7 to specify the parameters for the driver module. See the sidebar “Specifying SCSI Controller Settings” later in this session for more information on these settings.

After you add any SCSI controllers, you return to the dialog box that enables you to select a device type. You can add network cards from this dialog box as well. In the dialog box, select Network from the list and press Enter. The installation program then displays a list of network cards from which you can select your network card.

When you press Enter, the installation program loads the driver module for the selected network card. That driver probes and determines the network card settings.

Once you return to the screen from which you select SCSI or network device, select Back and press Enter. This takes you to the dialog box that asks you about adding devices. Select Done and press Enter. The installation program then switches to graphics mode and guides you through the rest of the installation, as outlined in Sessions 2 and 3.

### Specifying SCSI Controller Settings

If you have a SCSI controller in your system, the Red Hat installation program loads a SCSI driver module for that controller. You have to identify the type of SCSI controller (such as Adaptec 1542 or Adaptec 2940). The installation program can attempt to determine the controller settings, such as IRQ and I/O port address, by probing various I/O port addresses. However, if the installation program fails to determine the SCSI controller settings, you have to specify these parameters — IRQ and I/O address — as options for the driver module. The exact formats of these options vary from one module to another. For example, the driver for an Adaptec AHA 152x card accepts the options in the following format:

```
aha152x=IOPORT,IRQ,SCSI_ID[,Reconnect,Parity]
```

where IOPORT is the I/O port address, IRQ is the interrupt request number, and SCSI_ID is the SCSI ID of the SCSI controller. The last two items are optional. A typical module option for the aha152x module might be:

```
aha152x=0x340,11,7
```

### Configuring the X Window System

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_71_0.png)

If the installation program cannot detect your video card during the X configuration step, you can skip that step and configure X after completing the rest of the installation.

After the installation is complete and you reboot the PC, you get a text login screen. Log in as root and type Xconfigurator to run a utility program with that name. The Xconfigurator utility enables you to create a configuration file that the X server needs.

The Xconfigurator program starts with a Welcome dialog box that displays a message about the X configuration file. After reading the message, press Enter to continue with the configuration process.

Xconfigurator automatically detects the chipset used by your video card and displays a summary message, as shown in Figure 4-1.

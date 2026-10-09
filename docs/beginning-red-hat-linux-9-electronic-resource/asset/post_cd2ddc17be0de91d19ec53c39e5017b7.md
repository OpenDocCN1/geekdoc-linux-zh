
![](img/b852150740856958b10aff9e8c9d2adc_41_0.png)

Of course, you are asked to type the password twice, to confirm that you didn’t mistype the first time. Type the password carefully each time to make sure you type it correctly.

You might encounter a message that tells you that the password is too short or too simple. This is a security feature, designed to remind you of the importance of choosing an unguessable password. If you consider your chosen password to be adequate for your needs, you can ignore these messages. However, for the sake of security you should make an effort to set an uncommon password for the superuser account. We’ll talk more about password security (and the techniques that people use for breaking passwords) in Chapters 8 and 12.

## Selecting Packages for Installation

Now, you have an opportunity to choose the software packages that you want installed along with the system. Red Hat Linux has already chosen a combination of software packages for the installation type that you selected at the beginning of the installation process. If you want to fine-tune the package selection, you can do so here by selecting the Customize… option:

![](img/b852150740856958b10aff9e8c9d2adc_42_0.png)

You don’t have to fiddle with the choice of installed packages here – it’s easy to add and remove packages after the installation is complete, as we’ll see in Chapter 4. So, to keep things simple, we’ll select the Accept the current packages list option here, and proceed to the next screen.

### The Automatic Installation Process

The Red Hat Linux graphical installation tool has now collected all the information that it needs to begin the installation. The next screen prompts you to begin the software installation:

![](img/b852150740856958b10aff9e8c9d2adc_42_1.png)

The software package installation is mostly automatic; the only thing you'll need to do at this stage is change the CD a couple of times (when prompted to do so) and admire the photographs that are displayed while the necessary packages are installed.

Before the software is installed, the installation process formats all the partitions that are supposed to hold these data. Then, the installation process continues by installing the software packages. Progress bars display the total time taken so far, and the estimated time of the software installation:

![](img/b852150740856958b10aff9e8c9d2adc_43_0.png)

### Creating a Boot Disk

With all the software packages installed, we go on to the screen shown opposite. Here, you are asked whether you would like to create a boot disk for your computer. A **boot disk** is a safety measure against problems that might occur in the boot loader. For example, installation of another operating system in the computer might overwrite the Red Hat Linux boot loader, GRUB – if that happened, it would be impossible to boot back into Linux. The boot disk helps us tackle such situations by providing an alternative way to boot into Linux.

You don’t have to create a boot disk, but we recommend that you do (unless you already have a boot disk from a previous installation of this particular operating system):

![](img/b852150740856958b10aff9e8c9d2adc_44_0.png)

The installer asks you to insert a suitable floppy disk for the boot disk creation process. Remember that the installation process overwrites all the contents of the disk, so you should provide a blank floppy disk or one that doesn’t contain any important files:

![](img/b852150740856958b10aff9e8c9d2adc_44_1.png)

When you insert the disk and confirm the creation, the installer starts the boot disk creation process. When the boot disk has been created, you should take it out of the floppy drive, label it, and put it in a safe place.

### Setting up the GUI

The final step of the installation process is to set up the graphical interface (X) for your computer:

Red Hat Linux should normally be able to detect the type of your video card and select it for you, and it is quite safe to accept the default values. If you want to be sure that it’s got the right configuration, check the setting here against the make, model, and RAM you noted in your hardware checklist, and adjust as necessary.

Note that *if you try experimenting with graphics modes during the X server configuration, you run the risk of crashing the computer, leaving the installation process unfinished. If you have any element of doubt regarding the compatibility of your video card with Red Hat Linux, you should probably skip the X-server installation process by checking the **Skip X configuration** checkbox at the bottom of the screen. You can always configure the X server after the installation.*

If *you can’t find your video card in the list, you should skip the X server configuration. It’s possible to configure your graphics card after the installation. Alternatively, you can try using the generic VESA card from the given list, which is likely to work with most of the unsupported video cards.*

Red Hat Linux then proceeds to detect the type of monitor being used. The monitor detected during installation will be highlighted on the screen as shown:

![](img/b852150740856958b10aff9e8c9d2adc_45_0.png)

![](img/b852150740856958b10aff9e8c9d2adc_46_0.png)

If you don’t find your monitor in the list, you can enter the horizontal and vertical sync information in the textbox entries at the bottom of the screen instead.

The video card and the monitor type allow Red Hat to formulate a list of video modes that can be supported on your computer. The video mode is determined by the screen resolution and the color depth (number of colors) in which objects can be shown on screen. The available color depth and resolution choices are displayed by Red Hat Linux in the next screen:

![](img/b852150740856958b10aff9e8c9d2adc_46_1.png)

While you can test the chosen setting using the **Test Setting** button, be aware that for graphic cards with partial support by the X-server, improper modes can crash the system and leave the installation process unfinished. If you're not sure about the compatibility of the chosen video card with the X server, you can skip the X configuration and configure it after the installation is finished.

Red Hat Linux also offers you a choice between booting into a text-based interface and a graphical interface. If you haven't had any issues with your graphics card in the installation process until now, you should accept the pre-selected setting of a graphical login.

## Finishing

This completes the installation of the Red Hat Linux operating system. Now, you need to remove any CDs and floppy disks from their respective drives, and click on the **Exit** button to reboot the machine:

![](img/b852150740856958b10aff9e8c9d2adc_47_0.png)

## Booting Up

When the computer has restarted, the boot loader takes over initially, as shown in the following screenshot:

![](img/b852150740856958b10aff9e8c9d2adc_48_0.png)

The boot loader shows the available operating systems to boot from. For this chapter we used a new installation, and so there is just a single entry in the list shown above. The selected option will be booted automatically within a few seconds, and you can hasten the process by pressing the *Enter* key. This screen should be followed by a long list of rapidly moving text messages, as Linux boots into its new installation.

## First Boot

Before the new installation is fully usable, Red Hat configures the last few parameters:

-   Setting up new user accounts
-   Setting the date and time
-   Configuring the system for the Red Hat Network
-   Selecting additional distribution software or documentation to be installed

The welcome screen (which we won’t show here) shows the list of parameters to be configured. Click **Forward** to move on to the first of these screens.

## Creating New User Accounts

We’ve already talked a little about the root user account – this is an administrative (or “superuser”) account that is created by default, and has privileges for performing just about any task that you need on the computer.

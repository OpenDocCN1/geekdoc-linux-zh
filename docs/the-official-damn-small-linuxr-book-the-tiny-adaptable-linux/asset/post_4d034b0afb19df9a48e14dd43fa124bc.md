
## Setting Up ALSA Sound in DSL

To make sure that your sound system is working in DSL and to set sound levels, you can use several applications that come with DSL or can be easily added using MyDSL. In particular, the Advanced Linux Sound Architecture (ALSA) sound system is required to use Skype in DSL, along with the gnu-utils package (which is required by ALSA).

To begin this procedure, boot up DSL. You can boot directly from a DSL live CD or from any medium you prefer (pen drive, hard disk, etc.).

Because I’m assuming that you want to set up Skype to work persistently in DSL (and not just go away after you reboot), the following procedure describes how to get the extensions you need for sound in Skype and reload them upon reboot. Here’s how to do that:

- 1. Before you begin downloading DSL extensions, determine where you want to save them for future use. For example, mount a hard disk partition or inserted USB flash drive (pen drive) so it is ready to save your extensions. Then, create a mydsl directory at the root of that device. With a pen drive, for example, you might type the following from a Terminal window with root permissions:
  
      `# mkdir /mnt/sda1/mydsl`

> **NOTE**
> 
> If your computer is a Windows system, it’s quite likely that your hard disk partition is formatted for the NTFS file system. If this is the case with your computer, you need to use a USB pen drive, create a hard disk partition of some other type (such as FAT32 or ext3), or remaster a CD (as described in Chapter 4, “Configuring and Saving DSL Settings”) to save the needed packages. DSL does not support writing to NTFS file systems.

- 2. From the DSL desktop, select the MyDSL icon.
- 3. Select UNC and select the ALSA package.
- 4. Read the description of the ALSA package. Note that the ALSA package requires the gnu-utils package to be installed (which we’ll get next) and an ALSA boot option to work.
- 5. Select Download. A pop-up window asks where to install the package.
- 6. When prompted, indicate where you want the ALSA package to be downloaded. The `/tmp` directory is used by default. To save it to a pen drive, however, you might type /mnt/sda1/mydsl instead. Select Download and you can watch the progress as the package is downloaded and installed.
- 7. Select UNC and select the gnu-utils package.
- 8. Read the description of the gnu-utils package.
- 9. Select Download. A pop-up window asks where to install the package.
- 10. When prompted, indicate where you want the gnu-utils package to be downloaded. The /tmp directory is used by default. Instead, you should type /mnt/sda1/mydsl to save the extension to a pen drive. Select Download and you can watch the progress as the package is downloaded and installed.
- 11. Open a Terminal window (right-click the desktop and select XShells, Root Access, Dark) and type the following commands to start the ALSA sound system:

```
# alsa_snddevices
# alsa_init
```

The alsa_snddevices command creates the audio group and sound devices (in /dev) that you need for ALSA to work. The alsa_init command starts the ALSA service. Your ALSA sound system should now be running.

Next, you can try to adjust your audio in DSL:

- 1. Start audio mixer—Start DMix to adjust sound levels by right-clicking the desktop and selecting Apps→ Sound/MPEG/VoIP→ Dmix Sound Mixer.
- 2. Adjust audio output—In the DMix window, select Master Volume. Then, move the sliders to adjust the audio levels for the right and left channels.
- 3. Adjust audio input—In the DMix window, select the name of your input device (it may be Microphone, Phone Input, or Line In). Click the Rec button (so the button turns on) to have the microphone be selected as your recording device. Move the sliders up to adjust the audio input levels.
- 4. Play sound—You can check your Internet connection at the same time you test sound output by starting XMMS to play a streaming radio station. Right-click the desktop and select Apps→ Sound/MPEG/VoIP→ XMMS→ Xmms News Feeds→ Xmms “KCPW NPR NEWS.” Streaming audio should play in your headphones.

At this point, you can close the DMix and XMMS windows. If your sound system is still not working, refer to the Troubleshooting Skype section near the end of this chapter for suggestions on debugging the problem.

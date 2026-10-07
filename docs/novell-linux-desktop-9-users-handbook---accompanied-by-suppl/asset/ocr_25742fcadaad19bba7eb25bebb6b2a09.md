# 40 Configure Sound Settings

# 1 Become Administrator

You remove printers in the Printers window; to become an administrator, select Edit, Become Administrator. The Run as Root dialog box opens.

# 2 Enter Root Password

Enter the root password in the Run as Root dialog and then click OK.

# 3 Remove Printer

Right-click on the printer that you want to remove (in the Printers window) and select Remove from the shortcut menu. The printer is removed from the Printers window (and deleted from your system).

# 40 Configure Sound Settings

Your sound card should be identified and configured during the NLD installation. The audio functionality is provided by Advanced Linux Sound Architecture (ALSA), which is licensed under GNU.

# NOTE

ALSA supports most sound cards. However, some new sound cards or even existing sound cards (from more obscure vendors) may not be supported. You can attempt to fine-tune the settings for an unsupported card and manually choose the driver for the card. In terms of supporting new hardware, sound cards include, it is important that you update your NLD system using Red Carpet whenever the Updates Available notification icon appears in the top panel of the desktop.

When you boot NLD, your NLD system is initiated by the sound server. As a user, you can enable system sound events and select the sounds for specific events. Of course, you also have control over the sound volume and settings for specific devices such as a microphone, the CD drive, and video sound.
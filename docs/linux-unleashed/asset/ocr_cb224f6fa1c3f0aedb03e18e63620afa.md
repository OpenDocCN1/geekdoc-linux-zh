# Configuring a Sound Card

Some versions of Linux come with a routine that can link in support for your sound card. Usually you choose the type of sound card from a menu during the installation procedure, and the install routine takes care of the rest for you. If that's the case, then the sound card should be properly working and you can skip this section. If your version of Linux didn't ask about sound cards when it installed or your sound card is not working properly, you will have to go through the installation and configuration routine described here.

# NOTE

Some CD-ROMs of Linux software include sound card configuration routines that can't be accessed until the operating system installation has been completed. Red Hat 5.0, for example, includes the utility sndconfig which can configure most SoundBlaster and compatible cards for you. Check your CD-ROM documentation to see which (if any) utilities have been provided for you.

The first step to setting up a sound card for Linux is to install the card itself. This is done by following the instructions that come with the sound card. There are no special steps that you must follow to configure a sound card for Linux, other than making sure the IRQ (interrupt), DMA (direct memory address), and I/O address are unique (which is necessary under DOS and Windows). If you installed the sound card already, you can obtain these settings from your Control Panel or other utilities. Some older sound cards use jumpers or DIP switches to establish these parameters. Whichever way they are set, you need to note them for your configuration under Linux.

# TIP

If you are using a sound card that supports Plug and Play, you should install it under Windows or DOS first because Linux doesn't have the ability to set the parameters for these cards in most cases. After installing the card under Windows or DOS, use the Control Panel or similar utility to display the settings chosen for the sound card and note them. You'll need to enter these values when setting up the card under Linux.
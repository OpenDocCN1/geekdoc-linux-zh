![](bbox=[0.19, 0.09, 0.65, 0.34])

**Figure 3.9** *The yast2 client attempts to detect and initialize installed networking interfaces.*

Click the Next button to continue configuring your card. You can assign an IP address and continue on to configure your computer for networking.

For additional information about networking setup, see Chapter 9, "Connecting to the Internet," which contains more details about configuring Internet interfaces from the command line by using such utilities as the `ifconfig` and `route` commands.

# # Sound

One of the most joyful things about using Linux is its support for sound and the wealth of audio and multimedia utilities. However, if you are depending on sound support while using PPC Linux, choose your Power Mac model carefully. Sound may or may not be fully supported.

Unfortunately, there is no comprehensive list of the hardware and functions that are supported on each existing Apple Power Mac computer. However, in general, sound is supported on most machines by simply loading the `dnasound.o` kernel module. An exception is the Apple G4 Cube, which plays sound via USB (*Universal Serial Bus*) speakers. For this model, simply load the `audio.o` kernel module using the `insmod` command, like this:

```
# insmod audio
```

Other models, such as early iBooks, may require specially configured Linux kernels in order to play sound. Linux may not support sound yet on newer (Summer 2000) iBooks.
models, such as the 390X, with a Linux kernel version 2.2.12 or later). You can get this driver at

http://www.linmodems.org

You'll find active discussions regarding this class of communication device (if you can call it that). Some Linux programmers feel that software-driven modems can be used for other tasks, such as voice dialing or call recording.

My opinion is that software-driven modems are a bad idea and bad engineering. This approach to providing communications ability for a notebook might save the manufacturer a few pennies, but it puts the consumer at the mercy of the operating system and the drivers' software vendor. For now, avoid any notebook with an internal modem, or order the notebook without one of these things if you can. Ironically, a very select few notebooks on the market use real modems (one being the Sony 505TX/TR series, now destined to be the "classic" Linux notebook).

In general, you'll have a better chance of success with Linux compatibility with a notebook if the computer is not the "latest and greatest" model. Older models (a year or more) have a much better chance of being supported. You should also peruse the comp.os.linux.portable Usenet newsgroup for answers to questions about compatibility.

Here are the features I look for when choosing a notebook for Linux:

+   *   A readable screen display with a resolution of at least 1024x768. Although 800x600 is acceptable, some X11 clients require 1024x768.

+   *   A graphics chipset supported by XFree86 that provides at least 16bpp.

+   *   A compatible sound system with a chipset supported by the Linux kernel sound modules. Many notebooks have only one speaker, although newer models might have stereo. Nearly all sound tinny, but they should support a line-out or headphone jack.

+   *   A hard drive with a minimum of 2GB of storage, and even more if you are doing development or want to install all the latest software and games.

+   *   A pointing device with at least two mouse buttons (three is even better). Apple iBook users must use two function keys to simulate a middle and right button click.

+   *   A minimum of 32MB of RAM (64MB or 128MB is even better).

+   *   At a minimum, a PCMCIA port supporting at least one Type II card. If the notebook doesn't have an internal CD-ROM, you can at least install Linux over a network. Other alternatives include using the Parallel Line Interface Protocol (PILP).
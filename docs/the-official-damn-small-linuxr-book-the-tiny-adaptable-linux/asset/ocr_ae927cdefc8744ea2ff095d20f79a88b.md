posted the same question and the results were interesting. Most users who do a conventional install do not know about the Frugal method. In addition, some say that there are applications they would like to have that aren’t provided in the repository, and others say that they are using DSL on a low RAM system.

Even with knowledge of the Frugal method, the second and third explanations are still reasonable. If you know what you are doing and you want to run your particular applications from within a very compact system, DSL may be a very good fit. On the other hand, if you have a limited resource system, DSL may work well as a low-fat operating system (e.g., for hardware that was originally built for Windows 95 or Windows 98).

There was a group of Linux enthusiasts who installed Damn Small Linux on a pair of 486 computers with 16MB of RAM. They actually found the performance of this particular installation with DSL somewhat useful. Personally, I think that this is scraping the bottom of the usability scale, unless you are planning on spending most of your time in text mode.

However, there are many examples of people running DSL on machines that have only 32MB of RAM. I feel that a conventional hard drive install makes more sense than a Frugal installation for any conventional computer that has 64MB of RAM or less.

In this example, you are using the computer only as a DSL machine; thus, I am not going to outline the many facets of creating a multiboot system. If you follow this process, you end up with a computer that only boots DSL when you are finished. If you are interested in setting up a multiboot machine, there are lots of how-tos on the Internet to reference. Setting up a single boot computer with DSL is a much simpler process, and you do not need any outside utility to accomplish this.

A good how-to on multibooting can be found at:

http://www.geocities.com/epark/linux/grub-w2k-HOWTO.html

A traditional hard drive install of Damn Small Linux is not that difficult to do. However, before you start, there are some things you should know about software compatibility and hardware requirements.

# Some Debian Compatibility

Damn Small Linux is not Debian! Damn Small Linux is built with KNOPPIX technology that is based on Debian technology. However, we have done a lot of customization to achieve such a small package.
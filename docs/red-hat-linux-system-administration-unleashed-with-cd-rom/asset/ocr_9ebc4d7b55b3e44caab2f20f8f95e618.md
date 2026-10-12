During the 2.1 kernel development cycle, support was added to the Linux kernel for a graphical console device supported by a hardware-specific frame buffer.

In order to take advantage of this support, you need an X server that is aware of frame buffers. This is available in the version of XFree86 that comes with your Red Hat distribution. Documentation of this feature can be found in the framebuffer.txt file under the Documentation directory of the Linux source tree.

# Sound

Although of minor importance on most server systems, the Linux sound drivers are next on the list of items to configure. The sound driver was derived from the OSS/Free driver by Hannu Savolainen, which is the freely available version of the OSS drivers available from http://www.opensound.com/. Work is underway to change the sound driver layer to one where this is not the case, however, and the current driver in the kernel is the result of work funded by Red Hat. Although a large number of sound cards are supported by the kernel sound drivers, you may find that if your sound hardware is obscure or very new, you will need to purchase the commercial OSS drivers if you want to use that hardware under Linux.

The first option in the sound configuration dialog is a simple switch to indicate whether or not you want any sound support in the kernel. If you do not answer this question in the affirmative, you will not get sound support. If you want support for sound, answer yes or indicate that you want sound built as a module.

The remaining options are about specific sound cards and are relatively straightforward. You will need to have information regarding IRQ numbers, DMA channels, and port addresses for your particular sound card, but if you choose to build sound support as modules, you can pass the majority of this information on to the module when it is loaded. If you are looking to build generic sound support, it is usually best to build the various drivers as modules. This has the additional advantage of making it easier to configure sound with the soundcfg tool provided by Red Hat.

If your sound hardware is of the plug-and-play variety, you may be required to obtain the isapnp tools and experiment with them to get your sound card working properly. If this is the case, be sure to build your sound card driver as a module, or you will not be able to properly configure the sound hardware with isapnp before the driver is loaded.

If you do not find a feature of your particular sound card listed in the sound configuration dialog, all is not lost. The next section of the kernel configuration is an extension of the sound configuration dialog with additional drivers for audio hardware subsystems, such as support for Soundblaster AWE and Audio Excel DSP.
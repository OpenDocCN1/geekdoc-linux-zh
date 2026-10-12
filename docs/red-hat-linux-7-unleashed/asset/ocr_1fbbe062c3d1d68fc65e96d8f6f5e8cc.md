+   - DECNet and ARcNet Support
+   - Direct Rendering Manager
+   - Voice Synthesizer Support
+   - Kernel-level HTTPD
+   - *Documentation/DocBook and doxygen*

# Planned Features for Linux 2.5

Kernels take time to polish for production, and books take time to prepare and print; as a result, there are many features that were either not ready in time to be considered for the 2.4 kernel, or that were not well understood enough to be included in this book prior to press. The following sections are a guess as to some of the directions to be taken with 2.5, but do not be surprised if more than one finds its way into an early revision of 2.4.

# CML2

If you have ever tried to *add* a new kernel feature, you have already seen why Eric Raymond is spending his flight and hotel time redesigning the kernel configuration tools.

CML2 is the Configuration Modeling Language to succeed the current `make xconfig` method with a simpler system, is easier to maintain and to program, and will allow module and service developers to specify all dependencies of their code. It may even be possible to specify your hardware to the CML2 interpreter and have it deduce the kernel options without intervention.

# Frame Buffers (fbdev)

James Simmons has plans for cleaning up the `fbdev` layer with a new API, adding support for cards with multiple frame buffers, and adding real multihread support to the console system.

# Sound System

Although partially present in 2.4, the next kernel will expand the support for the ALSA sound drivers.

# V4L2

The 2.4 kernel contains little in the way of new support for the video and FM radio interface primarily because the developers are reworking the entire system for V4L2; unfortunately, V4L2 was not considered stable enough to be included into the 2.3 development tree and has been pushed back to Linux 2.5.
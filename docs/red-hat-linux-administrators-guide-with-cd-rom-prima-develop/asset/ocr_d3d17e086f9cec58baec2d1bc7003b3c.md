Configuring sound under Linux used to be tiresome and unrewarding task. Before Red Hat developed many of the latest utilities and incorporated other programs developed by various users into its basic configuration, only a handful of sound cards ran successfully under Linux. Red Hat Linux now supports a wide variety of sound cards and can detect nearly any card using the kudzu utility after the initial install and can then configure them for sound by using the sndconfig program. As Red Hat continues to progress and more sound card manufacturers make their drivers available, cards will continue to become better supported and detected under Linux. Besides that, the Linux kernel continues to make more resources available for sound development.

This chapter will look at the following issues for configuring sound and setting up audio utilities under Linux:

+   - Checking your system for sound compatibility
+   - Configuring sound automatically using Red Hat utilities
+   - Testing sound files by piping directly to devices
+   - Setting up sound files to play under the various window managers
+   - Encoding audio files for transmission over the Internet
+   - Running various audio tools, such as CD, MP3, and .wav files, under Linux

# # Wiring Linux for Sound

Setting up sound under Linux for your own enjoyment has become remarkably simple. Not so long ago, I remember spending hours trying out different drivers and options under the Linux kernel, reconfiguring settings in various files, and downloading program after program in the feeble attempt to get my plug and play sound card to work under an older Red Hat release. I finally did get it to function, but it is amazing how simple it has become to set up sound and play with audio files and streams under Linux.

Installing the sound card into the machine has now become the more difficult aspect of configuring sound. In many respects, it is now easier to set up sound
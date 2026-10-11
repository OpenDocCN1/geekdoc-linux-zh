+   * The Shareware OSS site Check http://www.4front-tech.com for information on commercial Linux sound drivers.

+   * The ALSA site Check http://www.alsa-project.org for information on the Advanced Linux Sound Architecture (ALSA) drivers.

+   * The XFree86 site Check http://www.xfree86.org for information on video support in XFree86. You might need to dig a bit on this site to find the information you require.

+   * The SuSE site SuSE (http://www.suse.com) contributes a lot to the XFree86 project, and often makes early versions of its XFree86 drivers available from its own site.

+   * The Accelerated-X site Accelerated-X, from Xi Graphics (http://www.xig.com), is a commercial alternative to XFree86.

+   * The Metro-X site Metro-X, from MetroLink (http://www.metrolink.com), is another commercial alternative to XFree86.

If you think it’s likely that you can make a notebook’s hardware work under Linux, but you’re not positive you’ll succeed, you might still consider buying the computer. I recommend doing so only from a store with a good return policy, however. If you think you might need to use software with which you’re not familiar, you might want to try that software on a desktop system, if possible, before buying the notebook. For instance, if your target notebook’s sound chipset is supported by ALSA but not by the standard kernel drivers, you might want to try ALSA on another system, simply to familiarize yourself with it.

# Replacement Hardware

If your video chipset doesn’t work under XFree86, you might still be able to use the computer in text mode. To use X programs, you’ll need to link the computer to a network and use an X server running on another computer. That’s not very convenient for a notebook, but it might be acceptable in a pinch.

If your audio chipset doesn’t work under Linux, your options are somewhat broader, although still not good. Two possibilities are

+   * USB speakers These devices don’t work through a standard sound card; instead, the sound card functions are included in the speakers themselves. You’ll need to lug the speakers around with you wherever you go, or at least wherever you want sound support. You’ll also need to use a 2.3.x or later kernel, or apply a back-port of the 2.3.x USB support to a 2.2.x kernel.

+   * PC Card sound card There are a small number of PC Card sound cards on the market. Most of these aren’t well supported in Linux, however. For the latest information, check http://pcmcia.sourceforge.org/ttp/SUPPORTED_CARDS, which has links to information on supported PC Cards and projects to add new support. As with USB speakers, you’ll need to carry around a set of conventional external speakers.
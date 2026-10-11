# Review

# MINI PC

# Banana Pi

$48.88/£28.50

Does the first of the true Raspberry Pi clones have what it takes to come out from the shadow of its highly successful inspiration?

![](bbox=[0.06, 0.15, 0.94, 0.5])

+   * **Pros**
+       * The dual-core ARMv7 processor, 1GB of RAM and SATA connector make it an upgrade from its source of inspiration

+   * **Cons**
+       * The design isn’t as Raspberry Pi compatible as it first appears, while its clone nature may be off-putting to many

Even if Lemaker, the Chinese-based company behind the Banana Pi, had picked a different name for its product, there would be no hiding its source of inspiration. The single-board computer boasts a 26-pin general-purpose input-output (GPIO) header at the top-left, both composite and HDMI video outputs, a 3.5mm stereo analogue audio jack, uses an SD slung on the underside for storage, and includes two USB 2.0 ports and an Ethernet connector.

In some respects, it’s surprising it has taken this long for someone to create a Pi-alike. A dig into the specifications reveals rather interestingly that the Banana Pi isn’t a direct clone, but a considerable evolution: the single-core ARMv6 700MHz Broadcom BCM2835 is replaced with a more modern dual-core ARMv7 1GHz AllWinner A20, the RAM doubled to 1GB, and additional connectivity added in the form of a SATA 2.0 port with on-board 5V power supply for 2.5” storage devices.

The Banana Pi, then, is being positioned as an upgrade for users who have found the berry-flavoured variant lacking. Sadly, there is a fistful of caveats for those hoping for a drop-in solution to their woes. The Banana Pi’s footprint is somewhat larger than that of the Raspberry Pi, meaning that it’s not directly compatible with any cases or mounts designed for its rival. The 26-pin GPIO header, while designed to be pin-for-pin compatible electrically, is shifted sideways from the Raspberry Pi layout to make room for a corner mounting hole. This causes larger piggyback boards to foul on the composite video output.

A bigger issue presents itself in what Lemaker calls the Camera Serial Interface (CSI) connector. The A20 chip lacks a true CSI implementation, using instead a parallel camera interface. As a result, there are no off-the-shelf camera modules that will connect to the Banana Pi, although Lemaker promises to launch a module of its own in the near future.
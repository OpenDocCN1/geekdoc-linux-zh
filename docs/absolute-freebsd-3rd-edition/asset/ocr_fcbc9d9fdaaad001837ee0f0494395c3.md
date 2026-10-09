hardware to stick at each end that allows us to transmit data much faster. Where old serial connections ran at 300 bits per second (baud), a whole bunch of modern hardware can run at 115,200 baud. Across hardware platforms, though, the common standard is 9600 baud, which is FreeBSD’s default console speed. A baud rate of 9600 is enough to carry whole screens of text at a comfortable speed.

Stick with 9600 baud for physical connections, unless you can’t. Some modern hardware doesn’t support 9600 baud. Some claim to support 9600 baud, but don’t. I’ve worked with devices hardcoded to 115,200 baud. Anything that fails or flat-out refuses to do 9600 baud is busted by design, but we often don’t control the choice of hardware. Changing the serial console speed for reasons other than hardware limitations makes your connection more fragile, and if you’re using the console, you’re in no mood for fragility. When I mention changing the port speed, that’s for use only when you have to.

SOL connections aren’t physical wires, so you don’t have to worry about line noise. You can safely run them at higher speeds.

Serial protocols also include a whole bunch of settings beyond their speed. It’s possible to muck with them, but the standard settings of 8 data bits, no parity, and 1 stop bit are the most widely used. You can’t change these in FreeBSD without recompiling the kernel, so don’t muck with them.

With that in mind, let’s set up a console.

# ## Physical Serial Console Setup

No matter what sort of serial console you have, you’ll need to plug into it correctly to make it work. You’ll need a null modem cable, available at any computer store or from online vendors. While the gold-plated serial cables are not worth the money, don’t buy the cheapest cable you can find either; if you have an emergency and need the serial console, you’re probably not in the mood to endure line noise.⁴

Plug one end of the null modem cable into the serial console port on your FreeBSD server—by default the first serial port (COM1 or uart0,
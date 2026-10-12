# # 286  Setting Up Dial-Up Networking

# Winmodems: They *only* do Windows

A quick word of caution about the *winmodems* that come with many new PCs and laptops. Winmodems are software-based internal modems—totally different from the traditional hardware modems. Also known as *Windows modems* or *software modems* (softmodem for short), they work only with special driver software (which in turn works only with Microsoft Windows). With winmodems and Linux, you’re pretty much on your own—but you can find some useful guidance online at the Linux Winmodem Support home page at `www.linmodems.org`. For example, I found out that the winmodem in my laptop uses a Conexant chipset and that a Linux driver is available from `www.linuxant.com/drivers/hsp/full/` `downloads.php`. Then I downloaded the zipped RPM file for Fedora Core that matches my kernel version (as reported by the `uname -r` command). Then I unzipped the RPM file with the `unzip` command and installed it on the laptop, using the `rpm` command. Now I can use my laptop’s winmodem from Fedora Core applications. By the way, the free version of the driver is limited to 14.4 Kbps. To go up to 56 Kbps, you have to get the full version for a modest price of around $15 U.S. The free version, however, is good for testing to make sure that the driver works with your softmodem.

# ## Connecting the modem

*Modem* is a contraction of *modulator/demodulator*—a device that converts digital signals (string of 1s and 0s) into continuously varying analog signals that transmit over telephone lines and radio waves. Thus, the modem is the intermediary between the digital world of the PC and the analog world of telephones. Figure 1-7 illustrates the concept of a modem.

![](bbox=[0.14, 0.64, 0.76, 0.79])

Inside the PC, 1s and 0s are represented with voltage levels, but signals carried over telephone lines are usually tones of different frequencies. The modem sits between the PC and the telephone lines and makes data communication possible over the phone lines. The modem converts information back and forth between the voltage/no voltage representation of digital circuits and different frequency tones that are appropriate for transmission over phone lines.
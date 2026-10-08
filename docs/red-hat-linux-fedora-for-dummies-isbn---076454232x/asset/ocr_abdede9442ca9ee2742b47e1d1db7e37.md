+   \- **RealPlayer (RealAudio):** Allows you to play the RealNetworks audio and video streams. Many Internet radio stations still use the RealNetworks protocols to stream their content. You can download the RealPlayer plug-in from

`http://proforma.real.com/real/player/unix/unix.html?src=d owner,000814rpchoice_c1`

Install the RPM package and then copy the plug-in to the Mozilla plug-in directory, just like with Macromedia Flash:

`cp /usr/lib/RealPlayer8/rnp.so /usr/lib/mozilla-*/plugins`

You can also use the RealPlayer8 application to listen directly to RealAudio streams.

+   \- **Java (Sun Microsystems):** A programming language that many Web sites use to provide dynamic content. Although dynamic content comes in many forms, it's basically anything that changes over time. Java is good at providing those interesting and often annoying Web things that spin around and do other silly tricks. Download the Java 2 Platform, Standard Edition (J2SE) RPM for Linux from java.sun.com/j2se/1.4.1/download.html.

Speaking of tunes, the next section shows how to play music from your CD-ROM.

# Groovin' to Tunes with CD Player

Imagine that you're sitting alone, working at your computer. Or, you could be reading a book that's boring you. It's Saturday night too, of course. What a drag. Want some diversion? Perhaps some music? We can't provide music, but we can show you how to use your computer to listen to some tunes.

In the following sections, we show you the tools Red Hat Linux provides to make your workstation into a sound system, including all the necessary applications to play CDs, and tools for connecting your PC to a sound card and speakers. Start by making sure that your computer can play music.

# Setting up your sound system

Red Hat Linux should have automatically configured your computer's sound system during the post installation process we describe in Chapter 3. However, you may run into problems — especially on older computers — so Red Hat provides a sound card detection utility.
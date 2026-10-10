# Streaming Audio

Streaming audio is for playing games, listening to Internet radio, and other online audio content. Streaming audio is designed to produce an uninterrupted sound output, but it requires the system to perform a content juggling act. Essentially, the system's audio buffer is continually filled with audio information, which is fed to the buffer through the system's Internet connection. Because of server and connection capabilities, the rate of input might vary. Because audio is used at a constant rate, the trick to managing streaming audio is to always keep the buffer full, although you might not be able to fill it at a constant rate.

Streaming audio is handled in Fedora in the `.m3u` format. The MPEG formats are also used for streaming audio. Although Xmsps supports streaming audio, another popular application is the Real Player, available from http://www.real.com/linux/. An excellent resource for music and sound in Linux is http://linux-sound.org/. The Network Audio section of that website contains an extensive list of streaming audio applications.

> **NOTE**
> The Icecast application, not provided with Fedora, is a popular streaming audio server. You can use Icecast to serve your MP3 music collection over your home LAN. You can learn more about Icecast at http://www.icecast.org/. A nice tutorial on Icecast is available at http://www.linuxnetmag.com/en/issue4/m4icecast1.html.

# Graphics Manipulation

Over a very short space of time, digital cameras and digital imagery have become extremely popular, to the point where some traditional film camera manufacturers are switching solely to digital. This meteoric rise has led to an increase in the number of applications that can handle digital imagery. Linux, thanks to its rapid pace of development, is now highly regarded as a multimedia platform of choice for editing digital images. Did you know that CGI effects for the film *The Lord of the Rings* were produced on Linux workstations and hundreds of Linux servers, all running Fedora?

This section of the chapter discusses The GIMP, a powerful graphics manipulation tool. You also learn about graphic file formats supported by Fedora, as well as some tools you can use to convert them if the application you want to use requires a different format.

# The GNU Image Manipulation Program

One of the best graphics clients available is The GIMP. The GIMP is a free, GPLed image editor with sophisticated capabilities that can import and export more than 30 different graphics formats, including files created with Adobe Photoshop. It is often compared with Photoshop, and The GIMP represents one of the GNU Projects' first significant successes. Many images in Linux were prepaired with The GIMP.

The GIMP can be found under the Applications, Graphics menu as simply The GIMP.

# FOSS

## System Administration

Find out exactly what's going on under the hood of your Linux box.

### Glances

*Glances* is a Python script that smartly displays a lot of information about your current session inside a standard terminal window. You can use the tool to monitor remote machines and use the built-in web interface to monitor machines using a web browser.
https://nicolargo.github.io/glances

### Portainer

Using Docker via the terminal isn't all that cumbersome and the tool is well documented. To make your life easier however, you can use *Portainer*, which is an open source, web-based graphical front-end that supports all the features exposed by the Docker API. You can use it to manage containers, images, networks, and volumes and it can manage a standalone Docker environment, or a Docker Swarm. From its dashboard you can create containers and view and manage all available ones. You can obtain real-time stats such as CPU and memory usage and various other details about the running containers and even access a container's console, all from within the browser window. *Portainer* is available as a Docker container so you can install it with a single command. To create containers you can use one of the dozens of predefined templates. The tool can be used by multiple users and has useful user-management functions. You can for example use it to define the levels of access any other users have to *Portainer*, and the aspects of Docker they can manage from within *Portainer*.
https://portainer.io

![](img/7a0a282248f9658f0c87e55744c797b6_173_0.png)

You can use Portainer to pull images from Docker Hub or a private registry.

### Firejail

*Firejail* enhances security by isolating programs and processes inside limited sandboxed environments. By locking away the web browser or any tool that can be compromised, *firejail* prevents a compromised program from accessing critical areas of the filesystem.
https://firejail.wordpress.com

### Bootchart

One of the major causes of longer boot times is that your system starts unnecessary tools and services during startup. But before you are them, it's best to get a picture of what's happening while your distro boots up. *Bootchart* is a simple utility that enables you to profile your Linux boot process and help measure the loading times of different services. It's now merged with SystemD. Fire up a terminal and enter *systemd-analyze time* to know the breakup of the boot duration. Similarly, *systemd-analyze blame* will list all running units ordered by the time they took to start.

To generate an image of the boot process, type *systemd-analyze plot* and *boot.svg*. From this image you can find all the active processes and can remove any you don't need. For example, if you print occasionally, you can disable CUPS from starting at the boot time. Furthermore, the image also helps you spot processes that take control of all resources and force the other processes to wait, slowing boot up.
www.bootchart.org

### Grub Customizer

There are several reasons you might want to change the default boot loader behaviour and *Grub Customizer* tool will help you to do that. The graphical tool can modify all aspects of the boot process and can even tweak how the Grub screen looks.
https://launchpad.net/grub-customizer

![](img/7a0a282248f9658f0c87e55744c797b6_173_1.png)

*Grub Customizer* also helps restore order when you've accidentally wiped clean the MBR.

### Remmina

A very usable remote desktop client, *Remmina* supports a wide range of protocols. It performs well and offers useful features such as the flexibility to change the quality settings of the connection on the fly.
https://remmina.org

### Inxi

A CLI tool that lists info about the hardware in your computer. With *inxi* you can collate details about the kit, including vendor details, device driver configuration and more.
https://github.com/smx/inxi

### Powertop

Intel developed the *PowerTOP* utility to track down apps that eat up your laptop's battery. The CLI utility offers suggestions to tweak power-guzzling tools to squeeze more juice from your laptop's battery.
https://01.org/powertop

### Stacer

*Stacer* is a system monitor that helps you track different aspects of your installation. It can also show alert messages when values for a parameter exceed a certain threshold.
https://github.io/Stacer-Web

### Logwatch

*Logwatch* parses, analyses and filters logs and then generates daily reports on your system's log activity. The utility also enables you to control the level of the report's verbosity.
https://sourceforge.net/projects/logwatch

## Internet tools

Make your online time more efficient with this collection of utilities.

### UGet

By default, the lightweight **UGet** download manager relies on `curl`, but if you install the `aria2` package, it can take on some more features, such as the ability to download torrents.

**UGet** is an all-round downloader that has all the features you'd expect from a download manager. It features a download queue, can pause and resume downloads and also accelerates downloads by grabbing files from multiple parallel streams. Furthermore, batch downloads are one of its specialities. You can use the tool to prioritise the download queue and even regulate the speed of the downloads individually. **UGet** can also shut down and hibernate your computer once it's finished downloading all the files.

https://ugtdim.com

![](img/7a0a282248f9658f0c87e55744c797b6_174_0.png)

### Rambox

Most desktop distros ship with a default messaging tool that enables you to sign into multiple online messaging services. These tools can sign into only a handful of the popular services.

In contrast, **Rambox** can plug into over 100 online messaging and email services. Every added service resides within its own tab, from where you browse the message history, write messages to your contacts, or use the other means of communication supported by the service. The tool will also display notifications. **Rambox** can also sync configurations if you use it on multiple computers. The program respects your privacy. Instead of storing your personal data, **Rambox** uses the `partition.persist` attribute of the `-webkit-` tag to create a persistent connection with the signed-in service. You can also set a master password and ask the tool to lock itself after a predefined period of inactivity.

http://rambox.pro

### Brave

While popular browsers can be equipped to thwart information leaks, **Brave** ships with privacy-strengthening features. The Brave project promises two improvements over the competition: privacy and speed. One of them is achieved by blocking ads and trackers, which has the pleasant side effect of improving the browsing speed.

https://brave.com

![](img/7a0a282248f9658f0c87e55744c797b6_174_1.png)

Since blocking ads may rob sites of revenue, **Brave** has some unique compensating tricks.

### Wallabag

A read-it-later tool, **wallabag** began when Google Reader was shuttered in 2013. You can install it on your own server or use it via its own service that costs about £8/year. **Wallabag** has favourite features including the ability to save articles, filter them by reading time, and more.

www.wallabag.org

![](img/7a0a282248f9658f0c87e55744c797b6_174_2.png)

### Tor Bundle

**Tor** enables users to browse the web anonymously. Its goal is to prevent people from tracking you online. The **Tor Browser Bundle** includes everything you need to connect to the **Tor** network of relays through a customised version of Firefox known as the **Tor Browser**.

www.torproject.org/projects/torbrowser.html.en

![](img/7a0a282248f9658f0c87e55744c797b6_174_3.png)

The tool is available as a Snap and AppImage binary that you can use without installing.

#### Magic Wormhole

A Python script that creates single-use encrypted channels to ferry files between computers across the Internet identified via pronounceable code.

https://github.com/warner/magic-wormhole

#### uBlock Origin

The **uBlock Origin** browser extension is an ad-blocker that also blocks tracking servers, malware domains, and more. It's available in the app stores of all mainstream web browsers.

https://github.com/gorhill/uBlock/

#### QuiterSS

**Quiterss** has all the features that you'd expect from a news reader. It can pull in RSS and Atom feeds, apply labels to each item and offers plenty of customisation options to boot.

https://quiteross.org

#### Vocal

A feature-rich podcast grabber, **Vocal** can subscribe to and stream podcasts on-the-fly or download them for offline listening. It integrates with popular desktops and has smart library management functions.

https://vocalproject.net

#### uFTPd

**uftp** ships with defaults that work for most users. It's designed for home users and developers who need a simple FTP server, but aren't too particular about being secure.

https://trogothib.com/projects/uftpd

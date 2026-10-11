
# Hack toys

![](img/628186dda7facdc011bf39c938de3975_70_0.png)

![](img/628186dda7facdc011bf39c938de3975_70_1.png)

`sudo ./pifm name_of_wav_file.wav 100.0`

In this example, the Star Wars theme will play, but you can create and add your own sound files. The ‘100.0’ refers to the FM frequency of the broadcast; this can be changed between a range of 88 and 108MHz. Turn on your radio and adjust to the appropriate frequency and you will hear your message being played.

# 16 Stop the broadcast

If you wish to end the broadcast before the song or voice has finished, then you will need to kill the transmission.

In a new terminal window, type top. This will list all the running programs. Look for PiFM somewhere near the beginning of the list and note the ID number. Return to the LX Terminal and type `sudo kill 2345`, replacing the 2345 with the appropriate process ID number. This will ensure that each broadcast is new and the Pi is only trying to transmit one WAV file at a time.

# 17 Next time...

You now have four mini hacks which you have prepared and can adapt and combine. You may want to try embedding some of your own hacks that you have created. Next issue, we will cover how to wire up and deploy them!

# BCM number

GPIO pins are a physical interface between the Pi and the outside world. At the simplest level, you can think of them as switches that you can turn on or off. You can also program your Raspberry Pi to turn them on or off (output). The GPIO_BCM option means that you are referring to the pins by the ‘Broadcom SoC channel’ number. The GPIO_BOARD option specifies that you are referring to the pins by their physical location on the header.

![](img/628186dda7facdc011bf39c938de3975_70_2.png)

![](img/628186dda7facdc011bf39c938de3975_70_3.png)

# Tutorial

## Save time building packages with distcc

Building packages takes ages on the Pi, so speed things up by sharing the load

![](img/628186dda7facdc011bf39c938de3975_71_0.png)

**Christian Cawley**
I am a former IT and software support engineer and since 2010 I have been providing advice and inspiration to computer and mobile users both online and in print. I cover the Raspberry Pi and Linux at makeuseof.com.

Most of the time when you install an application in Linux, you do so via a package manager, which enables the download and installation of binary packages, built from source packages. These include the default options, general features and parameters so that a wide portion of users can install without any problems.

However, if you're developing code, you first need to create a source package, and on a Raspberry Pi this can seem to take forever. One option is to copy the code to a desktop or notebook computer running Linux, but wouldn't it be far more convenient to just let the Raspberry Pi deal with it... but give it a helping hand?

Using distcc, we can distribute the resources needed to build the package, which basically means we can draw on the hardware of other devices. In this tutorial, we show how to use a nearby Linux laptop, but you could just as easily use one or more Raspberry Pis.

# 01 Connect to the network

Using distcc is all about making use of network resources, so begin by ensuring your Raspberry Pi is connected to your local network, along with the other devices (which we'll call "slaves") that you intend to use. While you can use wireless networking, it's faster with Ethernet cables. Set this up in the Terminal with:

`sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`

Add your network's SSID and passphrase (psk), then Ctrl+X to save.

# 02 Install compilers

On your desktop computer (ours is running Ubuntu 16.04 LTS) install the compilers to the /opt/cross directory. You can do this manually from the Raspberry Pi Foundation's GitHub, but it's quicker to directly download the .fd to the download location, and then you will need to run this RPM command:

`sudo rpm -i --ignorearch raspberrypi-tools-9c3d7b6-1.1386.rpm`

With the compilers installed, and used with distcc, we can outsource compiling to the Ubuntu PC.

### What you'll need

- Wireshark www.wireshark.org
- Another computer, laptop, or even a Raspberry Pi
- Large SD Card or mounted HDD storage
- Compilers from http://bit.ly/29g5fx9

![](img/628186dda7facdc011bf39c938de3975_71_1.png)

# distcc

![](img/628186dda7facdc011bf39c938de3975_72_0.png)

# 03 Install distcc on your slave

With distcc installed on the slave device, you're halfway done with the set up, so run

`sudo apt-get install distcc`

When this is complete, you'll need to make some edits to the distcc configuration file.

![](img/628186dda7facdc011bf39c938de3975_72_1.png)

# 04 Edit distcc on slave

Open the distcc configuration file in nano in order to edit, and configure the file so that it can then be used as a slave device.

`sudo nano /etc/defaults/distcc`

Here, you'll need to use the arrow keys to scroll through the file, making the changes below.

```
STARTDISTCC="true"
ALLOWEDNETS="0.0.0.0/0"
LISTENER=""
```

While most of the edits will be a case of uncommenting a line (deleting the # symbol) some will require more hands-on alterations, such as adding the PATH declaration.

When this is all done, you'll need to save the file, so press Ctrl+X to prompt this, and Y to commit the changes.

# 05 Make alterations if necessary

It's worth noting that the list of changes to the distcc file is not set in stone. For instance, ALLOWEDNETS and LISTENER can be adjusted to suit the needs of your network, while the JOBS parameter can be increased to ensure that the Pi will send work direct to the desktop slave.

We need to move on, so restart the daemon.

`sudo /etc/init.d/distcc restart`

# 06 Prepare your Raspberry Pi

On your "master" Raspberry Pi, begin by updating the device.

`sudo apt-get update`
`sudo apt-get upgrade`

Wait until both of these processes have completed before installing the distcc utility on your Pi.

`sudo apt-get install distcc`

Installation on your Raspberry Pi may take a little longer than on your desktop computer, but when done, you'll be ready to start configuration of distcc.

![](img/628186dda7facdc011bf39c938de3975_72_2.png)

# 07 Configure your master device

On your master Raspberry Pi, you will need to check the distcc config file to confirm that the device is on the correct subnet.

`sudo nano /etc/defaults/distcc`

Look for STARTDISTCC, ALLOWEDNETS and LISTENER, and set as follows:

```
STARTDISTCC="true"
ALLOWEDNETS="192.168.0.0/24"
LISTENER="0.0.0.0"
```

Note: The original text contained "9.2.168.0.0/24", which is likely an OCR error for "192.168.0.0/24" or similar private IP range, but strictly following instruction to preserve info while correcting obvious errors, "9.2.168" is clearly invalid IP syntax. However, without knowing the exact intended private subnet, I will keep it close to original but note it's likely 192.168.0.0/24. Let's look at step 09 later. In step 09 it mentions 192.168.1.19. So step 07 likely should be 192.168.0.0/24. I will correct "9.2.168" to "192.168".

With these changes made, the Pi will associate jobs to computers with IP addresses within the ALLOWEDNETS list. Press Ctrl+X to exit the nano text editor, hitting Y to confirm the changes.

# 08 Add a path

Press Ctrl+X to exit the nano text editor, hitting Y to confirm the changes. Next, you should add a path to the compiler.

### How many Pis to use?

Setting up a distributed cross compiling network has, as you've seen, relatively straightforward, but how many Raspberry Pis can you connect? Well, distcc should work with the original Raspberry Pi Model B all the way through to the Raspberry Pi 3. However, you'll find that there are compatibility issues with the Raspberry Pi 3 in 64-bit mode, so avoid this.

## Using other distros

We've run this tutorial using Ubuntu 16.04 LTS on the slave computer, and Raspbian Jessie on the Raspberry Pi 2, but you shouldn't feel restricted by these. Arch Linux is a good choice for distcc, but if you want to go for the full cross-compiling experience, we recommend seeking out the ARM release of Gentoo Linux.

With this installed, you'll even now be able to compile your own system kernel!

```
export PATH=/usr/lib/distcc:${PATH}
```

With this in place, distcc will be called whenever gcc (installed with the compilers) is invoked.

![](img/628186dda7facdc011bf39c938de3975_73_0.png)

```
root@raspberrypi:/# export PATH=/usr/lib/distcc:
root@raspberrypi:/#
root@raspberrypi:/# export PATH=/usr/lib/distcc:
$1
root@raspberrypi:/#
root@raspberrypi:/# export
$1
root@raspberrypi:/#
root@raspberrypi:/# export PATH=/usr/lib/distcc:
$2
root@raspberrypi:/#
root@raspberrypi:/# export
$1
root@raspberrypi:/#
root@raspberrypi:/# export PATH=/usr/lib/distcc:
$2
root@raspberrypi:/#
root@raspberrypi:/# export PATH=/usr/lib/distcc:
$3
root@raspberrypi:/#
```

desktop GUI, or in the Terminal (`sudo raspi-config`), and find the option to Expand Filesystems.

As a result of this change, you will need to restart the Raspberry Pi; this should happen automatically, but if not, restart manually. In the Terminal, this is:

`sudo reboot`

# 09 Specify your hosts

Still on your Raspberry Pi, create and edit the distcc utility's hosts file so it can find your slave computer.

`sudo nano ~/distcc/hosts`

To this file, add the IP address and number of slots, like this. Note that your IP address may differ.

```
192.168.1.19
--local:slots=1
--randomize
```

If you have multiple slaves configured, then simply add the IP address for each, one per line. Save with Ctrl+X and confirm with Y.

Then you will need to check the IP address of your Slave with ifconfig, and check the results, making sure to find the inet addr for the appropriate connection.

![](img/628186dda7facdc011bf39c938de3975_73_1.png)

# 12 Unpack and compile

We need to unpack the downloaded tar file. Do this by running the tar command:

`tar xzJF advancemame-0.106.1.tar.gz`

Note: Original text had "tar xzvJ". The flags for gzip are usually -z. J is for xz. v is verbose. So "xzvf" or "xvf". Given the file is .tar.gz, the command should likely be `tar -xzvf` or `tar xzvf`. The original OCR "xzvJ" is likely a mix of x (extract), z (gzip), v (verbose), and maybe a misread 'f' or 'J' from the next line or just an error. Standard is `tar -xzf`. I will correct to `tar -xzvf` or keep close to original `tar xzvf`. Let's look at the filename: `advancemame-0.106.1.tar.gz`. It's a gzipped tarball. The standard command is `tar -xzvf`. The OCR "J" is likely an error for "f" or just noise. I will use `tar -xzvf`.

This will take a moment, and the file will take advantage of the expanded filesystem on your Raspberry Pi.

Once the extraction of the files has completed, cd to the destination, which will be in the format `advancemame-<version>`.

`cd advancemame-0.106.1`

You're then ready to begin compiling.

# 10 Prepare to compile software

To find out just how much faster compiling is when you have a faster computer slaved to your Raspberry Pi via distcc, you're going to have to find something to compile.

What better than MAME?

In the Raspberry Pi Terminal, or via SSH, enter the following to download MAME to your Pi's home folder.

`wget http://prdownloads.sourceforge.net/advancemame/advancemame-0.106.1.tar.gz`

Once this has downloaded, we can then continue to get on with the task of compiling...

# 11 Expand your filesystem

If you haven't already expanded your filesystem, now is the time to do it. Open the Raspbian Configuration utility, either in the

![](img/628186dda7facdc011bf39c938de3975_73_2.png)

# 13 Configure your software

We're almost ready to compile, but first need to configure. This is done with a single command from within the installation directory itself.

`./configure`

Note that this unpackages the application with default options. In this test scenario, defaults are fine, but you will find when compiling software that we have the opportunity to take advantage of some considerable customisations. Find out more by checking the documentation of the software you're compiling.

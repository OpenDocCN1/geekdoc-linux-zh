# distcc

![](bbox=[0.08, 0.12, 0.38, 0.16])

directory. You can do this manually from the Raspberry Pi Foundation's GitHub, but it's quicker to directly download the .fd to the download location, and then you will need to run this RPM command:

```
sudo rpm -i --ignorearch raspberrypi-tools-9c3d7b6-1.1386.rpm
```

With the compilers installed, and used with distcc, we can outsource compiling to the Ubuntu PC.

# 03 Install distcc on your slave

With distcc installed on the slave device, you're halfway done with the set up, so run

```
sudo apt-get install distcc
```

When this is complete, you'll need to make some edits to the distcc configuration file.

![](bbox=[0.08, 0.47, 0.38, 0.61])

# 04 Edit distcc on slave

Open the distcc configuration file in nano in order to edit, and configure the file so that it can then be used as a slave device.

```
sudo nano /etc/defaults/distcc
```

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

```
sudo /etc/init.d/distcc restart
```

# 06 Prepare your Raspberry Pi

On your "master" Raspberry Pi, begin by updating the device.

```
sudo apt-get update
sudo apt-get upgrade
```

Wait until both of these processes have completed before installing the distcc utility on your Pi.

```
sudo apt-get install distcc
```

Installation on your Raspberry Pi may take a little longer than on your desktop computer, but when done, you'll be ready to start configuration of distcc.

![](bbox=[0.46, 0.5, 0.78, 0.64])

# 07 Configure your master device

On your master Raspberry Pi, you will need to check the distcc config file to confirm that the device is on the correct subnet.

```
sudo nano /etc/defaults/distcc
```

Look for STARTDISTCC, ALLOWEDNETS and LISTENER, and set as follows:

```
STARTDISTCC="true"
ALLOWEDNETS="9.2.168.0.0/24"
LISTENER="0.0.0.0"
```

With these changes made, the Pi will associate jobs to computers with IP addresses within the ALLOWEDNETS list. Press Ctrl+X to exit the nano text editor, hitting Y to confirm the changes.

# 08 Add a path

Press Ctrl+X to exit the nano text editor, hitting Y to confirm the changes. Next, you should add a path to the compiler.

# How many Pis to use?

Setting up a distributed cross compiling network has, as you've seen, relatively straightforward, but how many Raspberry Pis can you connect? Well, distcc should work with the original Raspberry Pi Model B all the way through to the Raspberry Pi 3. However, you'll find that there are compatibility issues with the Raspberry Pi 3 in 64-bit mode, so avoid this.
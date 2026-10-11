
## Private cloud storage

Turn the Pi into your own personal Dropbox using ownCloud and an internet connection

![](img/daaca9116bc2b1db669c224de81abc7c_59_0.png)

The themes of a lot of our Raspberry Pi guides revolve around the size and portability of the Pi itself, lending it to tasks you may have used a full-sized or small computer for in the past that the Pi can now take over. Having your own private cloud is another excellent use of the Raspberry Pi's capabilities, because you can store it hidden away somewhere and it will require very little day-to-day maintenance. Make sure you invest in some decent, portable USB storage such as an external HDD, and also get a case for your Pi in the process.

![](img/daaca9116bc2b1db669c224de81abc7c_59_1.png)

### What you'll need
- External storage
- Constant internet connection

> *Left* Rather than store all your media and files on a cloud server in an unknown location, you can keep a cloud in your own home

### 01 Set a static IP

After setting up your wired or wireless internet connection, you need to make it static. Use `sudo nano /etc/network/interfaces` to open up the network settings file. Find the `iface eth0` line so you can change and add to it:

```
iface eth0 inet static
address 192.168.0.50
gateway 192.168.0.1
netmask 255.255.255.0
network 192.168.0.0
broadcast 192.168.0.255
```

### 02 Install a lot of software

You'll want Apache software and PHP for this. Install everything you need with:

```
$ sudo apt-get install apache2 php5 php5-json php5-gd php5-sqlite curl libcurl3 libcurl4-openssl-dev php5-curl php5-gd php5-cgi php-pear php5-dev build-essential libpcre3-dev libapache2-mod-php php-apc
```

### 03 Set up PHP Accelerator

Install your accelerator with `sudo pecl install apc` and create an ini file for it. To do this, use `sudo nano /etc/php5/cgi/conf.d/apc.ini` and then add this to the file:

```
extension=apc.so
apc.enabled=1
apc.shm_size=30
```

![](img/daaca9116bc2b1db669c224de81abc7c_60_1.png)

### 04 Configure file limits

Go into the Apache config file with `sudo nano /etc/php5/apache2/php.ini`. It's a big file, but there are two filesize options you need to find, and a third extension option you need to add as below:

```
upload_max_filesize = 2048M
post_max_size = 2200M
extension = apc.so
```

### 05 Set up SSL

First of all, you need to enable SSL in Apache; do this by using `sudo nano /etc/apache2/sites-enabled/000-default` and change "None" to "All" in the `AllowOverride` option. Follow this up with the following two commands:

```
$ sudo a2enmod rewrite
$ sudo a2enmod headers
```

### 06 Finish up with Apache

You now need to do two sets of commands: a big one which requires some info and then a restart:

```
$ sudo openssl genrsa -des3 -out server.key 1024
$ sudo openssl rsa -in server.key -out server.key.insecure
$ sudo openssl req -new -key server.key -out server.csr
$ sudo openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
$ sudo cp server.crt /etc/ssl/certs; sudo cp server.key /etc/ssl/private; sudo a2enmod ssl
$ sudo a2ensite default-ssl
$ sudo service apache2 restart
```

### 07 Download and install ownCloud

Here you have a series of commands to run that will download, unzip and install ownCloud to the right place:

```
$ wget https://download.owncloud.org/community/ownCloud-7.0.0.tar.bz2
$ sudo tar -xjf owncloud-7.0.0.tar.bz2
$ sudo cp -r owncloud /var/www
```

### 08 ownCloud permissions

Make sure your hard drive is connected and mounted as you want it. First, give webserver permission to use ownCloud:

```
$ sudo chown -R www-data:www-data /var/www/owncloud/
```

Next, use `sudo nano /var/www/owncloud/.htaccess` and make the same changes you did in the `php.ini` file above. Finally, give permissions to the location you mounted the hard drive to with:

```
$ sudo chown -R www-data:www-data [mount]
```

![](img/daaca9116bc2b1db669c224de81abc7c_60_2.png)

### 09 Set up ownCloud

Open Midori and navigate to `https://[ipaddress]/owncloud` to begin the ownCloud setup process. The first thing you'll need to do is change the data location to the mount point of your external drive, which can be found in the advanced options. And you're done!

### Be inspired

Need an idea of what your next step could be? Check out our media caster tutorial and maybe you can fuse the two concepts together. Upload videos to your cloud and get them to play over your network.

![](img/daaca9116bc2b1db669c224de81abc7c_61_0.png)

## AirPi

Predict the weather using your own sensor station

The AirPi has a pedigree that aligns perfectly with the mission of the Raspberry Pi Foundation. Created by two teens in sixth form to measure various forms of pollution, the project's popularity exploded with thanks to some highlighting by the Raspberry Pi Foundation and it's now the premier way to create a weather station on the Raspberry Pi.

The AirPi kit comes with a small selection of sensors by default that can be upgraded and improved upon with extra breakout boards and modules. Included with the kit is a barometric pressure sensor, a humidity and temperature sensor, an ultraviolet radiation sensor and a microphone for noise pollution.

The first thing you'll need to do is assemble the kit, for which you'll require a soldering iron and a steady hand. There are some basic instructions that come with the kit you can follow but it doesn't hurt to have a look at some of the online images to figure out exactly where everything goes. Be careful when soldering all the resistors to make sure you don't melt the 26-pin connector on the underside otherwise it won't go on your Pi.

Once that's done you need to start setting up your Raspberry Pi. Open up a terminal and get some of the Python tools you'll need to use:

```
$ sudo apt-get install git-core python-dev python-pip python-snibus
```

Download and install the python-eeml package:

```
$ sudo apt-get install libxml2-dev libxslt-dev python-lxml
$ git clone https://github.com/peterivi/python-eeml.git
$ cd python-eeml
$ sudo python setup.py install
```

You need to install i2c support for the pressure sensor, so first use `sudo nano /etc/modprobe.d/raspi-blacklist.conf` and remove the comment from the blacklist `i2c-bcm2708` line.

Next, open up the modules file with `sudo nano /etc/modules` and add `i2c-dev` to the bottom of the file. Save that and install:

```
$ sudo apt-get install i2c-tools
```

Add your Pi to the i2c user group with:

```
$ sudo adduser pi i2c
```

Now reboot your Raspberry Pi before continuing. Finally, install the final Python module with:

```
$ sudo apt-get install python-smbus
```

Now we can install the AirPi code. Still in the terminal, use:

```
$ git clone -b non-modular https://github.com/tonmharcley/AirPi.git
```

If you're using a revision 2 Model B or a B+, use `sudo nano AirPi/AirPi.cfg` to edit the config file. Change `I2CBus = 0` to `I2CBus = 1` and alter the next line to read `LCD = False`. Create a Xively account, add the API and ID keys to the config file and save it. You can now start taking measurements by running `Upload.py`.

### What you'll need
- AirPi
- Soldering iron
- Solder

**Top right** Measure your surroundings with AirPi and share your data with the scientific community

**Bottom right** The AirPi perfectly fits the Raspberry Pi, so you can easily enclose your device in a small weatherproof box

![](img/daaca9116bc2b1db669c224de81abc7c_62_0.png)

## Dusklights

Use your Raspberry Pi to control outdoor lights that automatically come on when it’s dark

### What you’ll need
- 1.2 k resistor
- 2.2 k resistor
- Light dependent resistor
- 1 μF capacitor
- Breadboard and wires

You’ve probably all seen those cheap, solar-powered lamps that you can stick into your garden to try and give it a classy bit of illumination during the night. If you’ve actually got one then you may have found out that they don’t shine very brightly and the plastic stakes can be very flimsy. So why not make your own version? What we’ll show you on this page is the beginning of an array of light-sensitive LEDs using a single LED, so that you can understand how the system works. We’ll use a special resistor called a light dependent resistor (LDR) or photosistor that changes its resistance based on the levels of light it’s receiving.

There’s no extra software you’ll need for this, so just make sure your Pi is up to date with `apt-get update` and `apt-get upgrade`. Turn it off, unplug it from the power source and get to work wiring up the circuit as shown in the Fritzing diagram. Take special note of the placement of the components, especially the LDR and the capacitor. What you’ll need to do is measure the time it takes for the capacitor to fully charge between pin three of the GPIO ports and ground. Also, make sure the negative end of the capacitor is hooked to the ground side of the circuit.

Once that’s done, turn your Raspberry Pi back on and download the code we’ve created for this project using:

```
$ wget http://www.linuxuser.co.uk/wp-content/uploads/2014/08/dusklight.zip
```

![](img/daaca9116bc2b1db669c224de81abc7c_62_1.png)

Unzip it and run it. We’ve made it so the Python shell will print out the values that the circuit returns, with a higher number meaning it’s darker and the capacitor takes longer to charge.

See how the circuit reacts to you covering the LDR with a finger or shinning a torch on it in order to get an idea of how your version will work.

To get this working for outdoor use it will require a bit of trial and error. The easiest way is to set it up when it’s getting to about the level of darkness you’d want the light to turn on and record the output from the sensor. Change the `if` statement so that it activates the LED over a certain number and you’ll be set. With some external power and more LEDs you can have a Raspberry Pi power an entire array of shining lights around your garden.

### Put ’em together

Linking up the AirPi with your dusklights allows you to have the ultimate outdoor Raspberry Pi device, allowing you to predict the weather and control your outdoor lighting.

With humidity and pressure sensors will be able to tell if it’s foggy or not, giving you more control over when your lights turn on.

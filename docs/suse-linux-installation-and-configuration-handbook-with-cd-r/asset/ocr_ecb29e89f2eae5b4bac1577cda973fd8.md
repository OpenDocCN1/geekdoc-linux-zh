```
#tar xzvf alsa-driverxxx.tar.gz -C /tmp
#cd /tmp/alsa-driverxxx
```

```
#./configure --with-isapnp=yes (Sound card is PnP. isapnptools must be installed)
#./configure (if you don't have a PnP sound card)
#make;make install
#./snddevices (To create the sound devices in the /dev directory)
#depmod -a (To handle the module dependency)
#cp /tmp/alsa-driverxxx/utils/alsasound /sbin/init.d/
```

Now you are finished installing the sound drivers. Next, you have to install the ALSA libraries with the following command:

```
#tar xzvf alsa-libxxx.tar.gz -C /tmp
#cd /tmp/alsa-libxxx
#./configure
#make;make install
#ldconfig
```

Now that the ALSA libraries are installed, you need to build the utilities. Enter the following:

```
#tar xzvf alsa-utilxxx.tar.gz -C /tmp
#cd /tmp/alsa-utilxxx
#./configure
#make;make install
```

After you're done installing the three packages, you should delete the three directories you made in the /tmp directory to save space.

# Configuring ALSA Using alsaconf

alsaconf is a shell script that automates the sound card configuration. This shell script uses a module (snd-detect) that was built or installed during the installation process. This script should automatically detect the existence of sound cards on your system. Again, if you have the binary RPMs, you only have to run alsaconf by issuing the following command:

```
#alsaconf
```

If you have the source distribution, you'll have to untar it and then execute it:

```
#tar xzvf alsaconf-xyz.tar.gz -C /tmp
#cd /tmp/alsaconf-xyz
#./alsaconf
```

+   Card Identifier—The card ID that refers to which sound card you are configuring. Normally, the first sound card is called CARD_0, the second card is called CARD_1, and so on.
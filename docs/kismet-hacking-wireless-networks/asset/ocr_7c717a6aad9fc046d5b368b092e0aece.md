```
cd /usr/src/madwifi-0.9.4
./configure
make
make install
```

When the `configure`, `make`, and `make install` commands have completed, the MadWifi driver has been installed. The installation process should be similar for any other wireless card driver.

# Configuring Kismet (Editing kismet.conf)

At this point, we have successfully installed both Kismet and a wireless card driver. We've almost completed the process, but there is still one more task we have to complete before we can successfully run Kismet on the laptop. Kismet has to be told two pieces of information. The first piece of information is the name of the user who will be running Kismet, and the second is what wireless card will be receiving the wireless data, and passing that on to Kismet itself.

To accomplish this, we have to tell the `kismet.conf` file, which controls the Kismet configuration, which wireless card is running and send the wireless data to Kismet. This will be a brief introduction to editing the `kismet.conf`, enough to get this basic installation running. Editing `kismet.conf` will be fully covered in Chapter 6.

To set up the `kismet.conf` file, open it in a text editor. If using the CLI, then editor such as vi or nano will be perfect. The `kismet.conf` file is usually located in the `/usr/local/etc/` directory.

```
vi /usr/local/etc/kismet.conf
```

Alternatively, you may use the GUI, and then pick a test editor which can be selected from a menu. The screenshots here were done in KWrite, which is a text editor under the KDE GUI.

First find the line that begins with `suidduser`. In the initial state, this line should read `suidduser=your_user_here`. (See Figure 2.9.)
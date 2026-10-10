
The *logtypes* variable tells Kismet which types of log files you want it to generate. The default options are acceptable (*dump*, *network*, *csv*, *xmll*, *weak*, *cisco*, and *gps*); however, you may not need all of these. The bare minimum that you should ensure are generated are the *dump*, *network* and *gps* logs:

```
logtypes=dump,network,gps
```

The *logdefault* variable specifies what text should be prepended to the log file name. Kismet writes the files in the format [logdefault]-[date]-[sequence-number].[filetype]. For instance, if the *logdefault* is set to Roamer, then the *gps* log of the third wardriving session of the day would be named Roamer-Oct-14-2006-3.gps. This option can be helpful for sorting results if you are wardriving multiple areas in the same day:

```
# Default log title
logdefault=MyCustomer
```

The final option that you may want to change in the *kismet.conf* file is the *logtemplate*. This option controls both the location that the logs are created and stored in and the format of the log files. If no changes are made to this variable, the logs will be created in the default format, with the default title, in the directory that Kismet is launched from. However, it can be beneficial to store all of your logs in one location, or to store the different types of logs in different directories. There are seven variables that can be set in relation to the logtemplate:

- %t is the title set in logdefault
- %d is the current date in the format Month-Day-Year (Mon-DD-YYYY)
- %D is the current date in the format YYYYMMDD
- %f is the time that the log started
- %i is the increment number of the log (i.e., 1 for first log of the day, 2 for second, and so forth)
- %l is the log type
- %h is the home directory

For example, if you wanted to have your logs generated in different directories by filetype, and created in the wardrives directory, you would have the following logtemplate:

```
logtemplate=WarDrives/$1/%n-%id
```

Assuming you set the logtypes variable to dump, network, and gps, you would need to create the wardrives directory with three sub-directories: dump, network, and gps.

After you have made any changes, save the file and you are ready to wardrive with Kismet.

# Wardriving with Linux and Kismet

There are a lot of reasons to use Kismet to wardrive. The exceptional range of log files you can generate make it very attractive. Unlike some other wardriving software, Kismet doesn’t just detect the access points, but also saves a complete log of all of the packets it sees. These dumps can be opened with other packet analyzers and can be fed into penetration test programs. Monitor mode allows you to identify access points that are cloaked (not broadcast via the SSID). Additionally, since the SSID is sent in cleartext when a client authenticates to the network, Kismet can often determine the SSID of these cloaked networks.

Now that we have tweaked the Kismet configuration files to our liking, we are ready to start wardriving with Kismet. In this section, you will learn how to start Kismet and how to use the Kismet interface once you have it running. We look at the different options that Kismet provides and, how to use a graphical front end for Kismet.

# Starting Kismet

Starting Kismet is relatively simple. Assuming Kismet is in your path, type kismet at the command line as shown in Figure 1.5.

# Figure 1.5 Starting Kismet…Something is Wrong Here

![](img/d6ac176c353d2b7687c1186a140180a1_39_0.png)

The process ID file (*pidfile*) could not be set. This is because you don’t have permission to write to /var/run. There are two ways to fix this. You can change the location where the *pidfile* is written in the *kismet.conf*:

```
# Where do we store the pid file of the server?
piddir=/home/roamer
```

Changing the location of the *pidfile* is one option, but because you have already set a *suiduser* in your *kismet.conf*, it is probably easier to *su* to root and then run kismet. Root has permission to write the *pidfile*, but after it has performed that action, Kismet drops the privilege down to the *suiduser*, avoiding the potential security risks of running as root.

# Figure 1.6 Kismet Starts Successfully

![](img/d6ac176c353d2b7687c1186a140180a1_40_0.png)

# Using the Kismet Interface

In this section, we'll provide you with an introduction to the Kismet interface. See Chapter 4 for a complete discussion of the Kismet menus and functionality. In addition to its ability to identify access points, Kismet has a very powerful user interface. You can find a large amount of information about each access point you have identified by examining the Kismet options in the user interface. Obvious information (e.g., the SSID) is available to you immediately, whether or not an access point is encrypted. For a casual wardrive, this may be all of the information that you need. However, if you want to understand more about the networks you have discovered, you need to be familiar with the different options available to you.

## Understanding the Kismet Options

When using the different options with Kismet, you will need to change your *sort* option first. By default, Kismet is in *autofit sort mode*. Unfortunately, in this mode you can't obtain a lot of information about the different access points beyond the information displayed in the default view. To change the sort mode, press the **s** key to bring up a menu of the sort options (see Figure 1.7).

Figure 1.7 Kismet Sort Options

![](img/d6ac176c353d2b7687c1186a140180a1_41_0.png)

At this point, you have 14 different *sort* options to choose from. Choose the option that best suits your needs. For instance, if you are only interested in access points with a specific SSID, you would choose **s** to have the access points sorted by SSID and then scroll down to the desired SSID.

Once you have chosen your sort method, you can start to find out additional information about each network. Using the arrow keys, highlight the access point you are interested in and press **Enter** to get the Network Details (see Figure 1.8).

# Figure 1.8 Network Details

![](img/d6ac176c353d2b7687c1186a140180a1_42_0.png)

You now know the MAC address (Basic Service Set Identifier [BSSID]) of the access point. Because the access point has a max rate of 54.0, you know that it is an 802.11 g access point operating in infrastructure mode. Although the main screen said that the network was using encryption, you can now identify WPA as the encryption mechanism in place. Once you are satisfied with the information, press the **q** key to close the details and return to the main view.

You may want to know what clients are connected to a network. By highlighting the access point and pressing the **e** key, you are presented with a list of any clients associated with the network (see Figure 1.9).

# Figure 1.9 The Client List

![](img/d6ac176c353d2b7687c1186a140180a1_43_0.png)

In client view, you can determine the MAC address of any clients associated with the access point. Additionally, in some cases, you can determine what type of card it is. The number of data packets that Kismet has seen and the number of those packets that are encrypted are identified. Once Kismet determines the Internet Protocol (IP) address of a specific client it is noted as well as the strength of the signal. Again, when you are finished looking at the client list, press **q** to return to the Network List.

There will be times where you are only interested in collecting information about access points on a specific channel. To disable channel hopping and collect data only on one channel, highlight an access point on that channel and press the **Shift+L** key to lock on that channel.

To resume channel hopping, press **Shift+H**.

Kismet also has a robust help panel. If you are unsure of an option, press **h** to display the Help menu (see Figure 1.10).

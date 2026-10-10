For example, if you wanted to have your logs generated in different directories by filetype, and created in the wardrives directory, you would have the following logtemplate:

```
logtemplate=WarDrives/$1/%n-%id
```

Assuming you set the logtypes variable to dump, network, and gps, you would need to create the wardrives directory with three sub–directories: dump, network, and gps.

After you have made any changes, save the file and you are ready to wardrive with Kismet.

# Wardriving with Linux and Kismet

There are a lot of reasons to use Kismet to wardrive. The exceptional range of log files you can generate make it very attractive. Unlike some other wardriving software, Kismet doesn’t just detect the access points, but also saves a complete log of all of the packets it sees. These dumps can be opened with other packet analyzers and can be fed into penetration test programs. Monitor mode allows you to identify access points that are cloaked (not broadcast via the SSID). Additionally, since the SSID is sent in cleartext when a client authenticates to the network, Kismet can often determine the SSID of these cloaked networks.

Now that we have tweaked the Kismet configuration files to our liking, we are ready to start wardriving with Kismet. In this section, you will learn how to start Kismet and how to use the Kismet interface once you have it running. We look at the different options that Kismet provides and, how to use a graphical front end for Kismet.

# Starting Kismet

Starting Kismet is relatively simple. Assuming Kismet is in your path, type kismet at the command line as shown in Figure 1.5.
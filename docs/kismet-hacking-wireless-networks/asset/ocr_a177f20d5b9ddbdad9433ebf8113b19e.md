Kismet and Mapping • Chapter 9 225

# ### Patching GPSMap

You can patch GPSMap to work with Google Maps, but this also presumes that you have a place to display those maps (i.e., your own Web server).

First, download the patch (http://parknation.com/gmap/files/gpsmap-gmap-0.1.tgz). Then, uncompress and apply the patch to the source and compile the binary:

```
```
tar xzf gpsmap-gmap-0.1.tgz
cd /pentest/svn/kismet-devel
patch -p0 < /root/gpsmap-gmap-0.1/gpsmap-gmap-0.1.diff
./configure
make gpsmap
```
```

Next, copy gpsmap to your desired location. Then, copy index.html and the mapfiles folder from /root/gpsmap-gmap-0.1 (or wherever you uncomprsessed it) to your web server. Run gpsmap against one of your Kismet .GPS files:

```
```
gpsmap -j -o gpsdata.js -u -r Kismet.gps
```
```

Your output file, gpsdata.js, should be copied to your Web server. Finally, you'll require a Google Maps API (http://code.google.com/apis/maps/signup.html). When you get your key, paste it into the index.html file (conveniently, where it says “KEYHERE”). This process is a bit complicated, and it does require that you have a Web server, but the results speak for themselves.

# ## KisMap

Due partially to the lack of map sources and the limitations of the patches, GPSMap is currently being re-written from the ground up as a new python-based tool (currently known as KisMap). KisMap works with Google Maps (something that was not originally supported in GPSMap), with other formats likely to come in the future.

# ## WiGLE

As has been mentioned in the BackTrack chapter, WiGLE (Wireless Geographic Logging Engine) is an online database that includes in excess of 15 million recorded wireless networks, most with geographic coordinates. WiGLE gives you access to Service Set Identifier (SSID) and manufacturer statistics, octet and channel usage statistics, and a browsable Web map of the world (see Figure 9.1).
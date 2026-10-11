Universal Time is now: Wed Feb 9 18:50:10 UTC 2011.

+   1) Yes
+   2) No
+   #?

If the change is correct enter 1 to confirm. Notice in the preceding example that tzselect switches time zones by setting the value of the TZ environment variable. You can actually change time zones from the shell prompt without tzselect by setting the value of the TZ environment variable and then exporting it. This is useful in situations where you don't have the root password for the system or if you want to use a different time zone for your account without changing the time zone used by other users. The syntax is `export TZ=time_zone`. A list of available time zones can be found in the /usr/share/zoneinfo/ directory, as shown here:

```
ws1:~ # ls /usr/share/zoneinfo/
Africa        Canada        Factory       Iceland     MST7MDT     Portugal    Zulu
America       Chile         GB            Indian      Mexico      ROK         iso3166.tab
Antarctica    Cuba          GB-Eire       Iran        Mideast     Singapore   posix
Arctic        EET           GMT           Israel      NZ          Turkey      posixrules
Asia          EST           GMT+0         Jamaica     NZ-CHAT     UCT         right
Atlantic      EST5EDT       GMT-0         Japan       Navajo      US          zone.tab
Australia     Egypt         GMT0          Kwajalein   PRC         UTC
Brazil        Eire          Greenwich     Libya       PST8PDT     Universal
CET           Etc           HST           MET         Pacific     W-SU
CST6CDT       Europe        Hongkong      MST         Poland      WET
ws1:~ #
```

Be aware that this change is not persistent. If you reboot your system, the time zone change will be lost. You can make the time zone change persistent for your user account by adding the following to the .profile file in your user's home directory:

```
export TZ='America/Denver'
```

You can also change time zones using the /etc/localtime file and the various zone files in /usr/share/zoneinfo that we looked at earlier. To do this, create a symbolic link to the appropriate time zone file in /usr/share/zoneinfo from /etc/localtime. For example, if you wanted to switch to the Mountain Standard Time zone in the United States, you would enter `ln -sf /usr/share/zoneinfo/MST /etc/localtime` at the shell prompt.

> **NOTE** Commonly used text encodings include iso8859 (also called Latin-9 encoding) which is designed for Western European languages, ASCII which uses an English-based character-encoding scheme, and Unicode which is designed to handle character sets from languages around the world.

![](bbox=[0.04, 0.73, 0.2, 0.82])

# ## Chapter Review

In this chapter, I emphasized the importance of creating a deployment plan when implementing new Linux systems. The first component in this plan is to conduct a needs assessment. When conducting a needs assessment, you should first determine the goals of the project and identify who the stakeholders are. You should get approval from all concerned parties before actually starting the project. You should use the information gathered in the needs assessment to develop the project scope, which states exactly what
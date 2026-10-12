# E.5. HOW TO LOAD MILO

NT ARC as boot options.

To get Milo into flash via the Evaluation Board Debug Monitor, you will need a flashable image. The build procedures make milo.rom, but you can also make a rom image using the makerom tool in the Debug Monitor software that comes with the board:

```
} makerom -v -l7 -1200000 Milo -o mini.flash
```

(type makerom to find out what the arguments mean, but 7 is a flash image id used by the srom and -l200000 gives the load address for the image as 0x200000).

Load that image into memory (via the Debug Monitor commands fload, netload, and so on) at 0x200000 and then blow the image into flash:

```
AlphaPC64} flash 200000 8
```

(200000 is where the image to be blown is in memory and 8 is the segment number where you put the image. There are 16 1024*64 byte segments in the flash and the Debug Monitor is at seg 0 and the Windows NT ARC firmware is at seg 4).

Set up the image that the srom will boot by writing the number of the image into the TOY clock.

```
AlphaPC64} bootopt 131
```

(131 means boot the 3rd image, 129 = 1st, 130 = 2nd and so on).

Power off, put jumper 7 on and power on and you should see the Milo burst into life. If you don't then take jumper 7 back off and reboot the Debug Monitor.

# EB66+

The EB66+, like all of the Alpha Evaluation Boards built by Digital contains the Evaluation Board Debug Monitor and so this is available to load Milo (Section ref id="dbm-section" name="Loading from the Debug Monitor"). Quite often (although not always) boards whose design is derived
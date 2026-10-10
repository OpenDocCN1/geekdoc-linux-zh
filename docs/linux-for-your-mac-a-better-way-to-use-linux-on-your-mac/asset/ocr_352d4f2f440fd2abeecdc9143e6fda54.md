Not all the output is shown here, but as you can see, this example output corresponds with the previous `/etc/lilo.conf` information. The Extended Mac OS partition resides on `/dev/hda9` and is about 6GB in size. The standard HFS volume (with the name `/boot`) is `/dev/hda10`. The root Linux partition is contained on `/dev/hda1`. The remaining partitions are a swap partition of more than 315MB, a secondary Linux volume labeled `/d2`, and a tiny bit of leftover and unused free hard space.

Other problems can be solved with proper configuration of the kernel (perhaps using kernel arguments) to work with a particular Power Mac's video hardware. In general, you can nearly always safely boot to an install or Linux session by using a framebuffer console, and not taking advantage of any special video hardware. For example, an ultrasafe YaBOOT or LILO kernel argument to use framebuffer console video might look like:

```
""
...
append="video=atyfb video=only"
...
""
```

A companion program named `fbset` is used to print diagnostic information or to set the console to a different resolution (if supported). For example, you can see the current framebuffer settings by using `fbset` at the console, like this:

```
```
$ fbset -i

mode "1024x768-75"
# D: 78.740 Mhz, H: 60.015 kHz, V: 75.019 Hz
gometry 1024 768 1024 768 16
timing 12700 159 33 28 1 96 3
hsync high
vsync high
rgba 5/10,5/5,5/0,0/0
endmode
```

```text
Frame buffer device information:

Name		: ATY Rage128
Address	: 0x94000000
Size		: 16777216
Type		: PACKED PIXELS
Visual		: DIRECTCOLOR
XpanStep	: 8
YPanStep	: 1
YWrapStep	: 0
```
```
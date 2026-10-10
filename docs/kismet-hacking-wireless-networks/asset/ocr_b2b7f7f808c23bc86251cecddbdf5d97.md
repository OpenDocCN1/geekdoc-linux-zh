# WARNING

Kismet does not calculate signal power or noise; rather it simply displays information provided by the wireless card driver and/or firmware. Some drivers or firmware may not report this information (especially while in rfmon mode), and in this case Kismet will not provide you with anything useful. Furthermore, even when cards do properly report this data, there is no consistency in terms of a scale, so comparing signal and noise levels among different cards is more or less useless.

# Figure 4.16 Wireless Card Power Display

![](bbox=[0.15, 0.325, 0.875, 0.725])

# Network Location

Kismet has a nice (and not very well known) feature that will attempt to geo-locate a network. The accuracy of this information is wholly dependent upon GPS location data. Since estimating range based upon non-existent signal and noise standards is virtually impossible, this data is (unfortunately) not very useful in geo-location. Rather Kismet will guess location based upon a sample of GPS-logged locations.
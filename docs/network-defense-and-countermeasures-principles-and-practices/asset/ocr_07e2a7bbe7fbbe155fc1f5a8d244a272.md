# Wi-Fi

When an individual connects to a wireless network, the service set identifier (SSID) is logged as a preferred network connection. This information can be found in the Registry in the HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WZSCVC\Parameters\Interfaces key.

The registry key HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\NetworkList\Profiles gives you a list of all the Wi-Fi networks to which this interface has connected. The SSID of the network is recorded within the Description key. When the computer first connected to the network is recorded in the DateCreated field.

# Uninstalled Software

This is a very important registry key for forensic examination. An intruder who breaks into a computer might install software for various purposes such as recovering deleted files or creating a back door. He will then, most, delete the software he used. It is also possible that an employee who is stealing data might install steganography software so he can hide the data Will subsequently uninstall that software. This key lets you see all the software that has been uninstalled from this machine: HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall.

# Gathering Evidence from a Cell Phone

In our modern times, cell phones are ubiquitous. As common as they are, it should be no surprise that cell phones play a role in some computer cases. As discussed in previous chapters, there are some crimes that are primarily executed via cell phones. Sending pornographic images via cell phone is one crime. Securing data from a suspect's cell phone in criminal investigation is often a good idea. Some of the kinds of data that might be retrieved and examined during a cell phone forensic investigation include

+   * Photos
* Videos
* Text messages or SMS messages
* Call times, dialed and received calls, and all calls
* Contact names and phone numbers

Obviously photos, videos, and text messages could contain evidence of a crime. However, contact information can be valuable as well. You learned in the first few chapters of this book that criminals frequently work in concert. A contact list can help you track down perpetrators.
# CHAPTER 5 First Steps with Linux

```
| -- /etc/sysconfig/networking
| -- /etc/sysconfig/networking/devices
| -- /etc/sysconfig/networking/ifcfcg-lo
|
| -- /etc/sysconfig/networking/profiles
| -- /etc/sysconfig/networking/profiles/default
|-- /etc/sysconfig/ntpd
|-- /etc/sysconfig/pcmcia
||
| -- /etc/sysconfig/redhat-config-users
|-- /etc/sysconfig/redhat-logviewer
|-- /etc/sysconfig/rhn
| -- /etc/sysconfig/rhn/rhnsd
| -- /etc/sysconfig/rhn/up2date
| -- /etc/sysconfig/rhn/up2date-keyring.gpg
|-- /etc/sysconfig/samba
|-- /etc/sysconfig/sendmail
|-- /etc/sysconfig/spamassassin
|-- /etc/sysconfig/squid
|-- /etc/sysconfig/syslog
||
| -- /etc/sysconfig/ups
|-- /etc/sysconfig/vncservers
|-- /etc/sysconfig/xinetd
|-- /etc/sysconfig/yppasswdd
```

For brevity, not all directories and files are discussed here or listed in the example.
etc/sysconfig contains many different hardware and software settings critical to the operation of your Red Hat Linux system. Knowing the location and contents of these files can be helpful if you need to troubleshoot new hardware configurations.

The settings in various files /etc/sysconfig (such as keyboard, mouse, sound, and so) are usually created automatically by a related Red Hat graphical or console-based utility.

These contents may dynamically change if you use the kudzu hardware configuration service. The kudzu service alerts you at boot time to remove, configure, or ignore a related setting if kudzu detects new or different hardware (such as a USB keyboard, network card, or monitor). kudzu creates a file called that contains a profile of your PC's current state. Note that if kudzu is not enabled or running, you can use device-specific configuration utilities such as redhat-config-keyboard, or you can manually edit configuration files.

Information about the type of pointing device attached to the PC, for example, is contained in the file /etc/sysconfig/mouse:
The **rootpw** command sets the password to whatever word follows (in the following example, `passWord`). It is a security risk to leave this password hanging around, so you should change this password (with the `passwd` command) after Linux is installed. You also have the option of adding an encrypted password instead (`--iscrypted g.UJ.RQeOV3Bg --enablemd5`).

```
```
rootpw passWord
```
or
```
rootpw --iscrypted g.UJ.RQeOV3Bg --enablemd5
```
```

The **firewall** command lets you set the default firewall used by your Fedora system. The default value is `enabled` (if the firewall is turned on). You can also set `firewall to disabled` (no firewall). (These values are described in the installation procedure earlier in this chapter.) As you can see in the example, you can optionally indicate that there be no restrictions from host computers on a particular interface (`--trust eth0`). You can also allow an individual service (`--ssh`) or a particular `port:protocol` pair (`--port 1234:udp`).

```
```
firewall --enabled --trust=eth0 --ssh --port=1234:udp
```
```

The **selinux** command indicates whether or not Security Enhanced Linux is enabled. The following line shows it as disabled:

```
```
selinux --disabled
```
```

The required **authconfig** command sets the type of authentication used to protect your user passwords. The `--enablshadow` option enables the `/etc/shadow` file to store your passwords. The `--enablemd5` option enables up to 256 character passwords. (You would typically use both.)

```
```
authconfig --enablshadow --enablemd5
```
```

The **timezone** command sets the time zone for your Linux system. The default, shown here, is United States, New York (America/New_York). The `-utc` option indicates that the computer's hardware clock is set to UTC time. If you don't set a time zone, US/Eastern is used. Run the **timeconfig** command to see other valid time zones.

```
```
timezone --utc America/New_York
```
```

The **bootloader** command sets the location of the boot loader (GRUB, by default). For example, `--location=mbr` adds GRUB to the master boot record. (Use `--location=none` to not add GRUB.) You can also add kernel options to be read at boot time using the `append` option (`--append hdd=ide-scsi`) or an optional password for GRUB (`--password=GRUBpassword`).

```
```
bootloader --location=mbr
password=GRUBpassword
```
```

Partitioning is required for a new install, optional for an upgrade. The code that follows is from the sample `ks.cfg` file. The `clearpart --linux` value removes existing Linux

## Clearing Partitions

This will wipe all information from your current partition table. Another way to accomplish this is with:

```
clearpart --all
```

If you already have the drives partitioned, then do not use either of the previous two lines of code. Use the following if you do not want all partitions wiped:

```
zerombr no
```

After this, if you only want to remove all Linux native and swap partitions, include the following:

```
clearpart --linux
```

At this time, you cannot remove any other partition types using this method. After the old partitions you no longer want to keep are removed, it is time to create new ones. KickStart uses the part command to accomplish this, in this format:

```
part mountpoint --size MB
```

Two optional flags are available as well:

- `--grow`: Add if you want the partition to be "growable"—that is, have its size extended if room is left after all the partitions are assigned.
- `--maxsize MB`: If you list this partition as "growable," you can add this flag after, to limit how large the partition can get.

So, to create a 16MB boot partition, you might use:

```
part /boot --size 16
```

For a /home partition that must be at least 200MB, you might use:

```
part /home --size 200 --grow
```

> **NOTE:** Partitions are created in the order they appear in the KickStart file.

## Action Type

The next piece of a KickStart file tells the installation program whether you want to install or upgrade. Assuming that you are using this tool to do a raw install, you need to use:

```
install
```

On a large network, which may include centralized home directories and user programs, it may be most useful to do a clean install on many of the machines rather than an upgrade. See the Immediate Solutions section “Upgrading With KickStart” to learn ways to make the most out of using this tool for upgrading existing Red Hat installations.

## System Configuration

Now, it is time to move on to the various configuration statements. Each of these statements involves a step of the setup process done during a normal install. The first of these configuration statements is for the mouse:

```
mouse type
```

Available types are listed in Table 10.1.

| **Type** | **Used For** |
| :--- | :--- |
| none | No mouse on the system |
| alpsps/2 | ALPS GlidePoint PS/2 mouse |
| ascii | Serial ASCII MietMouse |
| asciips/2 | PS/2 ASCII MietMouse |
| atibm | ATI bus (PS/2) mouse |
| generic | Generic two-button serial mouse |
| generic3 | Generic three-button serial mouse |
| genericsps/2 | Generic two-button PS/2 mouse |
| generic3ps/2 | Generic three-button PS/2 mouse |
| geniusnm | Serial Genius Netmouse |
| geniusnmps/2 | PS/2 Genius Netmouse |
| geniusnpsps/2 | PS/2 Genius Netmouse Pro |
| thinking | Serial Kensington Thinking Mouse |
| thinkingps/2 | PS/2 Kensington Thinking Mouse |
| logitech | Serial C7 Logitech mouse |
| logitechcc | Serial CC Logitech mouse |
| logibm | Logitech bus (PS/2) mouse |
| logimman | Serial Logitech MouseMan/FirstMouse |
| logimmanps/2 | PS/2 Logitech MouseMan/FirstMouse |
| logimman+ | Serial Logitech MouseMan+/FirstMouse+ |

| **Type** | **Used For** |
| :--- | :--- |
| logimman+ps/2 | PS/2 Logitech MouseMan+/FirstMouse+ |
| microsoft | Microsoft-compatible serial mouse |
| msnew | Microsoft serial mouse Revision 2.1A or higher |
| msintelli | Serial Microsoft IntelliMouse |
| msintellips/2 | PS/2 Microsoft IntelliMouse |
| msbm | Microsoft bus (PS/2) mouse |
| mousesytems | Serial Mouse Systems mouse |
| mmseries | Serial MM Series mouse |
| mmhittab | Serial MM HitTablet mouse |

After the mouse identification comes the time zone, which is set with the **timezone** item. Many options are available, depending on what country you are in and whether the country is large enough to span multiple time zones. Some commonly used zones are shown in Figure 10.1— for the rest, run the **timeconfig** command to find your time zone. Along with the time zones, you can tell your system to use Greenwich Mean Time (GMT) by adding the **--utc** flag. In my KickStart file, this line might look like this:

```
timezone --utc Canada/Pacific
```

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_329_0.png)

Setting up video information is more complicated; how much so depends on how well your hardware is autoprobed. Regardless, this setup simply depends on knowing your hardware and doing your research. The X configuration line begins with **xconf**. Although you could just leave it as is, you will end up with an autoprobed video card (hopefully) and a generic 640x480 video mode. Options available to go with the **xconf** item are the following:

- **--card**: Information identifying your video card. You only need this or the **--server** option, not both.
- **--hsync**: Your monitor's horizontal sync rate. This and **--vsync** are needed only if the monitor type is not available in the list. Numbers should be in either a comma-separated list or a range with a dash.
- **--monitor**: Information identifying your video display. If you have this information, you do not need **--vsync** or **--hsync**.
- **--server**: Instructions on which X server to install. You only need this or the **--card** option, not both.
- **--vsync**: Your monitor's vertical sync rate. This and **--hsync** are needed only if the monitor type is not available in the list. Numbers should be in either a comma-separated list or a range with a dash.

Too many monitors and video cards exist to try to list them all here. Type the following to get a list of all of your options saved into the file /root/xhardware:

```
Xconfigurator --help 2> /root/xhardware
```

> **NOTE:** You need to include **2>** because just `Xconfigurator --help` sends information to STDERR, not STDOUT, and therefore a standard redirection of **>** will not work.

All the values associated with these options need to be listed in quotes. In the simplest case, in which the monitor type is known and the video card probes properly, you might use the following:

```
xconfig --monitor "mag DX700T"
```

Now, you need to set the root password. Although both encrypted and unencrypted options are available, you are best off sending encrypted versions if you are installing over a network. If you are just installing locally using a floppy and a CD-ROM, then encryption is not necessary. The statement for setting this password is **rootpw**, which can be used in either of two ways. For unencrypted passwords, type the following:

```
rootpw password
```

If you want to have the password encrypted, first you need to set this password for an account on another machine. Then, open /etc/shadow or /etc/passwd and copy the encrypted version of the password, as follows:

```
rootpw --iscrypted encryptedpassword
```

Following the same theme, the next item involves how the machine handles authentication. The basic statement that handles authentication is **auth**. Three major options are available with this statement: NIS (see Chapter 16), shadow passwords, and MD5 passwords (refer to Chapter 9). If you want to use shadow passwords—which is highly recommended, unless you are using a specific tool that does not understand them—include the flag **--usesshadow**. To include MD5—also recommended—use the flag **--enablemd5**.

If you want to use NIS to centralize your users for network management purposes, first add the flag **--enablisis**. Then, you need to include the flag **--nismdomain** *domain*, where *domain* is the name assigned to your NIS domain. You also need **--nisservice** *server*, where *server* is the hostname for your NIS server.

If you are not using NIS but are using shadow and MD5, then your line might look like this:

```
auth --usesshadow --enablemd5
```

However, if you are using NIS, you might have:

```
auth --enablemd5 --enablisis --nismdomain hidden.dom --nisservice 192.168.0.14
```

> NOTE: As usual, the code above needs to all be on the same line. It has to be broken up in this case for printing reasons.

Last, but certainly not least, is the LILO configuration section. This line begins with **lilo** and, in fact, can just be left with that one word if you don’t need any of the options. The LILO installation flag is **--location**, which refers to where LILO is installed. Available options are the following:

- **mbr**: The default location
- **partition**: Specifically, the root partition
- **none**: Do not install LILO

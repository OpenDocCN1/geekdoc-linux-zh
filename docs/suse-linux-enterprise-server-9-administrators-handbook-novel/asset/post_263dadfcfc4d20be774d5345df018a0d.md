
## FIGURE 8.3
NTP client configuration screen.

![](img/ae8469257d2662b469f2360b3bbbe322_261_0.png)

The default dialog box allows you to specify a single host as the time source. To use multiple sources, click Complex Configuration and then use the Add button to create an entry for each desired time server. If you already have at least one time source defined (other than the local clock), the Complex Configuration screen is displayed automatically.

### NOTE

One of the options in the Complex NTP Client Configuration dialog box is called Run NTP Daemon in Chroot Jail. chroot jail (or Change root jail) is a way to limit the portion of the file system that the daemon can see; this is similar to using MAP ROOT in NetWare. By default, ntpd runs in chroot jail mode. If, for some reason, you don’t want ntpd in chroot jail, edit either `/etc/init.d/xntpd` or `/etc/sysconfig/xntp` and change the `XNTPD_RUN_CHROOTED` setting from yes to no.

Refer to Chapter 13, “System Security,” for further discussions about chroot jails.

### CAUTION

Even if you are running `ntpd` in chroot jail, the copy of `ntp.conf` to edit is still the copy in `/etc`, and not the copy in the jail’s `/etc` directory (which, by default, is `/var/lib/ntp/etc`). The copy is updated automatically by `ntpd`’s startup script.

When you use YaST to set up your NTP client configuration, it also updates `XNTPD_INITIAL_NTPDATE` variable (used by `ntpd` upon system startup to obtain the current date and time information) setting in `/etc/sysconfig/ntp`. However, if you manually edited `/etc/ntp.conf` outside YaST, the `XNTPD_INITIAL_NTPDATE` setting may contain obsolete host data until the next time YaST is used to update the NTP settings. The following example illustrates the telltale sign of this happening when you manually start or restart `ntpd` from a terminal session:

```
Athena:/home/admin # rcxntpd start
Try to get initial date and time via NTP from ticker failed
Starting network time protocol daemon (NTPD)        done
```

Ticker is a time source that has been removed from the network, and its server command entry was manually removed from `/etc/ntp.conf` without using YaST. As a result, `/etc/sysconfig/ntp` contains the outdated information (`XNTPD_INITIAL_NTPDATE = ticker`) leading to the failure message.

## Configuring an NTP Server

`ntpd` can function as an NTP client or as an NTP server or as both concurrently. This allows a single server in the network to run `ntpd` to obtain time from an authoritative time source (either an NTP server on the Internet or a locally attached reference clock); then it redistributes that information to other servers (running ntpd client-only mode) internally. This reduces traffic to the external time source and ensures all NTP clients use a common time source.

There are two ways in which an NTP client can locate an NTP server. The first method is simply to statically configure either the IP address or the DNS name of the NTP source in the client’s `/etc/ntp.conf` file. The other method is to set up the NTP time server to broadcast or multicast its time onto the network and configure the clients to listen for the broadcasted/multicasted time information.

To run `ntpd` with broadcasts or multicasts, add the `broadcast address` command to the configuration file. In broadcast mode, the address should be the broadcast address of one (or more) of the local network(s), such as 192.168.1.255. To enable multicast mode, the address should be 224.0.1.1 (for IPv4) or ff05::101 (site local, for IPv6)—the addresses assigned to NTP. Multiple broadcast commands may be specified to support multiple local network interfaces or multiple multicast groups.

Before you allow **ntpd** to act as a time source, you must ensure the server has the correct time. In most cases, you accomplish this by obtaining its time from one or more of the standard Internet NTP servers. This also can be done with reference clocks. The NTP distribution includes hardware drivers for more than 40 radio and satellite clocks and modem services that can be used as reference clocks. A list of supported drivers can be found in `/usr/share/doc/packages/ntp-doc/html/refclock.html`. It is also possible to use an otherwise “undisciplined” local clock as a primary or backup time source. The following discussion presents information on how to set up a reference clock, using the local clock as an example.

### NOTE

Many radio reference clocks can be set to display local time as adjusted for time zone and daylight saving mode. When used with NTP, the clock must be set for Coordinated Universal Time (UTC) only. The OS kernel performs the conversion to local time, so the fact that the clock runs on UTC will be transparent to the users.

The clocks are specified in `/etc/ntp.conf` as though they are real-time servers on the network using the server keyword. For this purpose, they are assigned special IP addresses in the form 127.127.t.u. In the address, t specifies the clock type and u is a unit number in the range 0–3 that distinguishes multiple instances of clocks of the same type. For example, the server's hardware clock will have a pseudo IP address of 127.127.1.0.

### NOTE

You can find a list of supported clock type values (t) in `/usr/share/doc/packages/ntp-doc/html/refclock.html`.

Normally, the individual drivers have special parameters that describe their configuration details. The refclock.html file mentioned in the preceding note provides links to the driver pages describing these parameters. For instance, a TimeBrick DCF77 receiver module uses the Type 8 Generic Reference Driver (PARSE). But because this Type 8 driver supports a number of different receiver modules, you need to include additional parameters to tell the driver which specific receiver module you are using. The complete server command for a TimeBrick DCF77 receiver module would be

```
server 127.127.8.0 mode 6
```

With the exception of the local clock, most of the radio reference clocks require support in the form of a serial port or special bus peripheral. You need to associate the clock driver to the particular hardware device by manually creating a symbolic link between them. For example, if you have a TimeBrick DCF77 receiver connected to your server's serial terminal port 1 (/dev/ttyS1), link the TimeBrick's clock device (/dev/refclock-u, where u is 0 for the first TimeBrick device) to the serial port as follows:

```
ln -s /dev/ttyS1 /dev/refclock-0
```

### NOTE

The clock device names are listed on their respective driver pages, under the Synopsis heading at the top of each page.

The local clock driver is also a special case. A server configured with this driver can operate as a primary server to synchronize other clients when no other external synchronization sources are available. If the server is connected directly or indirectly to the Internet, there is some danger that it can adversely affect the operation of unrelated clients. For this, you would configure this driver at a stratum greater than any other likely sources of time (say 3 or 4) to prevent the server from taking over when legitimate sources are still available.

By default, the stratum for this driver is set at 5, but can be changed by the fudge configuration command and/or the ntpdc utility. As a matter of fact, the default /etc/ntp.conf sets its stratum to 10.

### WARNING

You should never configure an NTP time server that might “devolve” to use its local clock to use multicast mode or broadcast mode.

The following summarizes the procedure necessary for setting up an NTP time source:

- 1. If using a hardware reference clock, configure and connect the device to your server per manufacturer instructions.
- 2. Update /etc/ntp.conf with the appropriate server 127.127.t.u command to support the installed clock.
- 3. Create a symbolic link between the clock device name and the hardware device driver.
- 4. Configure the startup scripts to run ntpd upon server boot using either insserv or the Runlevel Editor in YaST.
- 5. Start up or restart ntpd for the updated ntp.conf to take effect.

## Troubleshooting Tips

Most of the time, ntpd is a “configure-and-forget” utility, especially if you are running it in the time consumer (a.k.a. client) mode. The most common oversight when it comes to using public NTP time sources is due to your firewall setting: NTP requires UDP port 123 to be opened in both directions. Unlike other client/server-type protocols such as Telnet, where the client uses a high-numbered port (1024 or higher), both the NTP client and server use port 123.

Sometimes the problem may be a misconfigured ntpd.conf entry causing ntpd to obtain its time from a wrong server, or something has gone astray with the time source itself. The NTP distribution includes a couple of utilities that are helpful in verifying the correct operations of ntpd running in time server mode: ntpq (NTP query) and ntpdc (a special NTP query program utility). The ntpq program implements the Mode 6 control message formats defined in the NTP specification (http://www.ietf.org/rfc/rfc1305.txt). The ntpdc program, on the other hand, implements additional functionality not provided for in the NTP standard. Both programs can be used to inspect the state variables defined in the specification and, in the case of ntpdc, additional ones intended for serious debugging. In addition, ntpdc can be used to dynamically reconfigure and enable or disable some functions while the ntpd is running.

Both ntpq and ntpdc can be run either in interactive mode or controlled using command-line arguments. For quick troubleshooting, it is easiest to run them using the -p switch; the following shows sample output from ntpq:

```
Athena:/home/admin # ntpq -p

     remote           refid st t when poll reach delay offset jitter
==============================================================================
 LOCAL(0)        .LOCL.  10 l   7   64   1  0.000  0.000  0.002
 dense.utcc.utor .INIT.  16 u   -   64   0  0.000  0.000 4000.00
```

### NOTE

You can run either ntpq or ntpdc on the server itself or from another machine elsewhere in the network (by specifying the host address on the command line; the default is localhost).


### Setting pppd Options

The `/etc/ppp/options` file is used to set options that govern pppd. The package ships with a template file, named `options.tpl`, but Red Hat and others don't include it. The `/etc/ppp/options` file shown in Listing 4.2 will do for most purposes.

#### Listing 4.2 The pppd Options File

```
# /etc/ppp/options
#
# Prevent pppd from forking into the background
detach
#
# use the modem control lines
modem
# use uucp style locks to ensure exclusive access to the serial device
lock
# use hardware flow control
crtscts
# create a default route for this connection in the routing table
defaultroute
# do NOT set up any "escaped" control sequences
asyncmap 0
# use a maximum transmission packet size of 1500 bytes
mtu 1500
# use a maximum receive packet size of 1500 bytes
mru 1500
#
# force pppd to use your ISP user name as your 'host name' during the
# authentication process
name username
#
# If you are using ENCRYPTED secrets in the /etc/ppp/pap-secrets
# file, then uncomment the following line.
#-papcrypt
```

The exam doesn't make much of the contents of this file, focusing more on the steps needed to make a connection.

### Authentication Options

PPP doesn't restrict who can connect from a client to a server because it's not designed to. Without authentication mechanisms such as PAP and CHAP, getting access to a machine over PPP is easy.

Linux supports the following protocols for authentication:

- **Password Authentication Protocol (PAP)** — This protocol provides clear text authentication.
- **Challenge Handshake Authentication Protocol (CHAP)** — With this protocol, passwords are never sent unencrypted.
- **Microsoft Challenge Handshake Authentication Protocol (MSCHAP)** — This is the Microsoft-specific CHAP version.

Both PAP and CHAP use secrets files to secure their logins, with differing degrees of effectiveness. PAP uses a procedure similar to the username and password pair for logging on to a machine, sending the information across the communications link.

CHAP uses a random string and the hostname to send an authentication request to the server, where it's compared and a similar set of data is sent back to the client. CHAP doesn't just authenticate at the initialization of the link, but at random times for the duration of the session, making it much more secure.

The `/etc/ppp/pap-secrets` and `/etc/ppp/chap-secrets` files contain four fields that are delimited by spaces, an example of which is shown here. This `/etc/chap-secrets` file is on the host blue:

```
# Secrets for authentication using CHAP
# client server secret
blue red fuchsia
red blue magenta
```

On the red host the `/etc/ppp/chap-secrets` file would contain the following:

```
# Secrets for authentication using CHAP
# client server secret
red blue fuchsia
blue red magenta
```

When blue is initiating a session to red, it looks for the line that lists blue as the client and red as a server and uses that secret string to build the authentication message. This means that when blue encrypts a message asking red to authenticate itself, red sends the message back encrypted with fuchsia.

When the red host is initiating the connection, it looks for its own hostname in the client field and the blue hostname in the server field and sends a message built with the magenta string.

> Both the `/etc/ppp/pap-secrets` and `/etc/ppp/chap-secrets` must be owned by the root user and root group with the permissions set to 740. In addition, you can use the minicom terminal adapter application as a quick test of the modem's connectivity.

## Plug and Play

When Plug and Play (PnP) is used, a device usually configures itself when plugged into the system bus. Plug and Play helps match drivers and devices with the correct communication mechanisms.

Linux isn't truly a Plug and Play OS, but the kernel does read the registers for the devices on the system, many of which can be easily recognized and made available to the device drivers via a table managed by the kernel.

The kernel does provide programmatic help to drivers in the form of programs and code that do PnP, and typically that's enough to get the device working. The kernel also assists in keeping resource conflicts from occurring by restricting bus resources to a single device. The 2.2 kernel provided this only for the IRQ and DMA resources, but the 2.4 kernel now provides this support for I/O addresses as well.

> **NOTE** Most BIOSs are PnP-compatible, and if the BIOS reads the device and then the kernel can see it from there, it's not really PnP, but it works.

### PnP Tools

The main utility for configuring devices under Linux is the `isapnp` program. Part of the isapnp tools suite, it's run at startup on many Linux distributions to discover the resources located on the ISA bus using software. (Remember that the PCI bus typically discovers devices using hardware and then makes those devices available to Linux.)

isapnp is configured with the `/etc/isapnp.conf` file, consisting of a custom mapping of which devices are going to use which resources on the system.

pnpdump reads the devices on the ISA bus and dumps that information out to the console by default. You can use pnpdump to view the configuration of a device and then edit `isapnp.conf` to add a similar device to the system, particularly if that device was not recognized properly.

> **ALERT** Thankfully, LPI doesn't think that we should be delving into the `isapnp.conf` file or the gory details of PnP outside of the concept, needed files, and commands we have covered here.

## Configuring Sound and Time

If you’re lucky enough to have a sound card that works with Linux already, you’ll hear the welcome sounds in KDE or be able to play CDs and sound files in X or the command line.

If the sound card on the system doesn’t currently work with Linux, the first thing to run is the sndconfig program. This exists on Red Hat Systems and plays a sound clip of Linus Torvalds pronouncing "Linux".

> **ALERT** The primary cause of a recently added sound card not functioning is a conflict with a secondary parallel port because both are using IRQ 5. The exam will test your knowledge of the IRQs and conflicts. Anytime you see a new card being inserted and something not working, an IRQ or I/O address conflict is somewhere in the answer.

### Local System Time

Being able to set system time properly is important for the accurate date and time on emails, synchronization of databases, and anything else that requires a reasonably accurate system clock.

Two clocks affect a system’s time: the hardware clock, which runs even when the system is off, and the system clock, which is a function of the kernel and an interrupt on the system. System time is a value derived by the time elapsed since January 1, 1970, or the number of seconds since 1969 ended.

The hardware clock exists to supply time to the booting Linux kernel and is ignored thereafter until the system is booted again.

### The date Command

The date command affects the system clock or time. To set your system time manually, use the date. The program offers a couple of ways to accomplish this, one for exquisite setting of the time, such as in a script, and the other for quick fixes in a shell session.

To set the system time to July 1 (0701), 4 a.m. (0400), 1995 (95), you’d use the following:

```
date 0701040095
Sat Jul  1 04:00:00 PDT 1995
```

To set the system time with a quickie update, you’d use the date command’s normal time formatting, like so:

```
date
Sat Jul  1 04:01:39 PDT 1995
date -s 'Sat Jul  1 04:01:39 PDT 1999'
```

Just cut and paste the output from the `date` command to the `new` command line by selecting the output while holding down the left mouse button, positioning the cursor, and pressing the middle mouse button to paste it. Alter the time to suit and press Enter.

> **NOTE** If you don't have a middle mouse button, you can try to *chord* the left and right mouse buttons by pressing them both at the same time to paste the information. You're actually better off typing it in, based on my experience.

To display the date in an alternative format, use the `+FORMAT` style. Instead of outputting the date and time with the normal formatting, you can cause it to meet certain character restrictions such as for naming files. For example, to display the date in yyyy-dd-mm format, you'd use the following:

```
date +%Y-%d-%m
```

This shows the following output:

```
2004-09-09
```

Naming a new file at the same time as it was created is simple if you know the previous code. To create a new directory named `backup` and prefix it with the current date (so it will sort nicely), you would use

```
mkdir `date +%Y-%d-%m`_backup
```

> **CAUTION** Be sure to use the back tick character (`), not the apostrophe ('). The back tick is normally found on the same key as the tilde character (~).

### The hwclock Command

`hwclock` affects the hardware clock, not the system clock or time. If you've spent a few cycles getting the system clock to the precise time, you'll need to ensure that those time values are stored to the hardware clock properly.

Most shutdown routines include a synchronization of the system time to the hardware clock, but just in case, follow the examples here to set it properly.

```
hwclock -r
hwclock --sysync
hwclock --hctosys
```

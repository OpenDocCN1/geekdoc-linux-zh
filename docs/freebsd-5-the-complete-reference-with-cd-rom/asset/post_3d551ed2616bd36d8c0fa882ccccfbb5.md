
## Testing Your Modem Hardware

Before proceeding further, you should test your modem’s functionality under FreeBSD. Today’s modems fall into three broad classes, each with different requirements under FreeBSD:

- **RS-232 serial modems** These modems attach to a computer’s external RS-232 serial port, or come as plug-in ISA or PCI cards that include serial port hardware on-board. RS-232 serial modems almost always work with FreeBSD, although you may need to reconfigure an internal modem’s interrupt request (IRQ) line or disable a motherboard’s RS-232 port to get the modem to work. These devices can be accessed as `/dev/cua0` through `/dev/cua3`.
- **Internal controllerless modems** Most internal modems sold today are *controllerless*, meaning that they lack much of the hardware traditionally associated with a modem, relying instead upon special drivers. These modems are also sometimes called *soft modems* or *WinModems*. Controllerless modems usually don’t work at all with FreeBSD. Drivers for some controllerless modems (particularly the popular Lucent-based modems) exist, but are hard to find—at the time of this writing, the `comms/ltmodem` port exists, but the files to which it points don’t exist. This problem may be remedied by the time you read this.
- **USB modems** Increasingly, external modems use the Universal Serial Bus (USB) interface rather than the RS-232 interface. Work is underway to support some of these (particularly those built around the Communications Data Class Abstract Control Model, or CDC-ACM, protocol), but it’s still primitive, as of FreeBSD 5.0.

As you might gather from the preceding list, your best bet for a modem is an RS-232 serial modem. This usually means an external RS-232 serial model, although older (mid-to-late 1990s and earlier) internal modems also work well.

To test your modem, connect it, power it on, and use a terminal program such as the text-based `minicom` or the X-based Seyon to test basic modem functionality. (Both of these programs can be installed as packages or ports, as described in Chapter 11.) You can launch Seyon by typing `seyon -modem /dev/cua0` (substitute your modem device filename, if it’s not `/dev/cua0`). You can then type `AT` or variants of that followed by numbers to obtain status information from the modem, or `ATDT####-####` to dial a number (replace `####-####` with the telephone number you want to dial). Your modem’s manual should list other commands you can type, and their effects. Figure 15-1 shows Seyon running, with a successful connection to a modem displayed.

![](img/f34d37e3abe9f4517128e54f80ab2616_416_0.png)

![](img/f34d37e3abe9f4517128e54f80ab2616_417_0.png)

![](img/f34d37e3abe9f4517128e54f80ab2616_417_1.png)

**Figure 15-1.** A terminal program enables you to test a modem without using PPP tools.

## Using a GUI Dialer

If you’re new to FreeBSD, the easiest way to initiate a PPP connection is to use a GUI dialing utility. These tools operate much like similar tools in other OSs, such as Windows or Mac OS. You enter critical information, such as your ISP’s telephone number, in dialog boxes, and then click a button to initiate a connection. You can usually configure these tools so that ordinary users can initiate connections, so they’re good for use on workstations. They can’t be controlled through an external script, though, so they aren’t so good if you want your system to automatically go online at particular times (say, to exchange e-mail once an hour). For that, a dialing script is superior, as described in the upcoming section, “Using Text-Mode Dialing Tools.”

## Locating a GUI Dialer

The first hurdle you must overcome in configuring a GUI dialer is in locating one. A wide variety of such dialers are available for FreeBSD. If you’ve installed KDE, you may have already installed one dialer, called KPPP. The GNOME project provides a similar dialer, GNOME-PPP, but it’s not installed in a standard FreeBSD GNOME system, and as of this writing, it’s not available in the ports system. For this reason, I describe the X-ISP dialer (`http://xisp.hellug.gr`). This is a GUI dialer that works from any X11 environment, and is available from the FreeBSD packages system and as a port (consult Chapter 11 for information on installing software).

If you locate and use some other GUI dialer, the details described here won’t apply, but the overall needs of the software will be very similar. Consult your GUI dialer’s documentation, or just browse its menus and dialog boxes, to learn about its differences from X-ISP.

## Creating an ISP Configuration

Configuring X-ISP to connect to an ISP entails two different types of configuration. First, you must create a *secrets* file, which stores your ISP username and password on disk; and second, you must tell X-ISP about your ISP’s telephone number, your connect speed, and so on.

> Some GUI dialers enable you to configure your secrets from within the GUI dialer itself, by entering a password in an obvious password field. X-ISP relies upon manual configuration of this critical file, though.

### Creating a Secrets File

FreeBSD (or more precisely, the *pppd* program that’s responsible for establishing a PPP link) stores critical authentication information in a file that’s called `/etc/ppp/pap-secrets`. This file stores usernames and passwords for the Password Authentication Protocol (PAP), which most ISPs use in 2002. Another protocol, called the Challenge Handshake Authentication Protocol (CHAP), is still in use by some ISPs, and if your ISP uses CHAP, you should create an `/etc/ppp/chap-secrets` file, which has precisely the same format and contents as *pap-secrets*.

> In the past, ISPs frequently used login procedures that required you to create a script that would echo your username and password in response to text-mode prompts. Such configurations are rare today, but you can still configure X-ISP to use this method. If your ISP uses such an antiquated login method, you don’t need to create a secrets file.

The secrets file consists of lines that have the following format:

```
client-name server-name password [ip-address[...]]
```

In this context, the *client-name* is usually your username, as issued by the ISP. (This might not be the same as your FreeBSD username.) The *server-name* is the ISP's dial-in server name. Because this name is often unknown, it's common to use an asterisk (*) in this field, to signify that any value is acceptable. The *password* is the password you use to log into the ISP; it's not the same as your FreeBSD login password. Finally, you may conclude a secrets file line with a list of IP addresses you're willing to accept from the ISP. Normally, this final field is missing because most ISPs assign IP addresses dynamically.

> **Caution**
>
> The *password* you enter in the secrets file is unencrypted. You should ensure that the *secrets* file is readable only by *root* (it should be owned by *root* and have 0600 permissions), to prevent ordinary users or intruders from reading your ISP password. You should use your ISP password only for logging into the ISP, not for logging into any other computer, including your FreeBSD system. These steps can minimize the risk posed by storing a password in unencrypted form on your hard disk.

You can create multiple *secrets* file entries for multiple users or ISPs. When you do this, you'll use GUI dialer or dialing script options to pick which username to use. For instance, the following entries enable a user to log into systems using the *agb* and *alex* usernames, each with its own password:

```
agb * w8tS4nr6
alex * b311gm7
```

### Configuring X-ISP

X-ISP, as installed from a FreeBSD package or port, may only be run by *root* or by a member of the *dialer* group. You can use this feature to control who can configure and use X-ISP—add any authorized PPP users to the *dialer* group, as described in Chapter 10, and leave others out of this group.

Once you have created a secrets file, you can launch X-ISP by typing **xISP** in an xterm window. The result is the main X-ISP window, as shown in Figure 15-2. To begin configuring X-ISP to handle your PPP connection, follow these steps:

1. Select Options | Account Information. This action produces the Account Information dialog box shown next:

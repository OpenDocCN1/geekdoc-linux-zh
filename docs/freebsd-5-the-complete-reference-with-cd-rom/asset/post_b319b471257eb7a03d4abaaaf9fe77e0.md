
2. Click **Add** in the **Account Information** dialog box. X-ISP responds by displaying a small dialog box with the prompt **Enter ISP Description**.

![](img/f34d37e3abe9f4517128e54f80ab2616_420_0.png)

![](img/f34d37e3abe9f4517128e54f80ab2616_420_1.png)

Figure 15-2. The main X-ISP window lets you control a connection, and you can use dialog boxes from the **Options** menu item to configure the program.

3. Type your ISP's name or some other identifying information. This text will later appear as an option in the ISP selection box in the main X-ISP window, such as A Small ISP in Figure 15-2. Click OK when you've entered this information. You should see the new ISP appear in the ISP name(s) field in the Account Information dialog box.

4. Type the ISP's telephone number into the Phone No(s) field in the Account Information dialog box. Do not include an area code unless you need to dial it to reach your ISP, but do include any codes you need to dial to get an outside line, if applicable. You can use a comma between digits to impose a delay, if you need such a delay at any point in the dialing process.

5. Click PAP or CHAP, if applicable, to use one of these authentication protocols. If you leave None selected in the Authentication Protocol area, you'll need to define a dialing script. Because this need is so rare today, I don't describe it.

6. Type your username in the User Name and Remote Name fields. Depending upon your ISP's configuration, you may need to enter this information in only one of these fields or in both of them.

7. Click OK in the Account Information dialog box.

8. Select Options | Communications Options from the main X-ISP window (Figure 15-2). This action produces the Communications Options dialog box shown here:

![](img/f34d37e3abe9f4517128e54f80ab2616_421_0.png)

9. You can adjust various serial port options in the **Communications Options** dialog box. Pay particular attention to the **Device** field, which should point to your modem device file. This is normally `/dev/cuaa0` or `/dev/cuaa1` for an RS-232 serial modem, but higher numbers are possible if you have more than two serial ports, and if you use an unusual device, it may be something else entirely. The Serial Port Baud Rate section sets the modem speed. Normally, 115200 works best, but the default is 38400, which produces slower-than-optimal speeds.

10. Select **Options | TCP/IP Options** from the main X-ISP window (Figure 15-2). This action produces the TCP/IP Options dialog box shown here:

![](img/f34d37e3abe9f4517128e54f80ab2616_422_0.png)

11. The **TCP/IP Options** dialog box lets you set various options related to TCP/IP configuration. Chapter 14 describes most of those options. You should leave most of them alone, but one possible exception is the DNS Support area. You may need to obtain the IP addresses of one or two DNS servers from your ISP, select Yes to the DNS Support option, and enter the IP addresses in the Primary DNS Server and Secondary DNS Server fields. Your system might obtain its DNS server addresses automatically as part of the PPP configuration process, but this exchange doesn't always go smoothly, so overriding it in this way is sometimes necessary.

X-ISP is now configured to make a PPP connection—at least in theory. Your connection may require tweaking, so you may need to dig into the configuration dialog boxes, including dialog boxes not described here, to tweak settings. Doing this can be a tedious and frustrating process because error messages tend to be cryptic.

> Tip
> *X-ISP relies upon pppd to make the PPP connection, and pppd logs information to /var/log/messages as it operates. Thus, if a connection fails, you should check /var/log/messages for clues by typing `tail -n 20 /var/log/messages`.*

## Initiating a Connection

Once you've configured X-ISP and created a secrets file for it, you can select your ISP and click Connect in the main window (Figure 15-2). You should then hear your modem dial (if it's set to echo those sounds through its speaker), and you should see some basic progress information appear in the display just below the ISP selection field in the main window. The Modem Speed field will then display your connection speed, and very shortly thereafter, you should be able to use the connection.

To check that your connection is active, you can use any TCP/IP programs, such as `ping`, as described in Chapter 14. You should be able to use web browsers, e-mail clients, and so on. Some of these may require reconfiguring to use your ISP's servers. Consult Chapter 24 and your ISP's documentation for more information. You can also use `ifconfig` to check for the presence of a `ppp0` interface, thus:

```
# ifconfig ppp0
 ppp0: flags=8051<UP,POINTOPOINT,RUNNING,MULTICAST> mtu 1500
     inet 192.168.1.205 --> 192.168.1.2 netmask 0xffffff00
```

If this command doesn't return the final line (which displays the local IP address and that of the computer to which it connects), then something is wrong, or perhaps you've tried it before the computers have negotiated a stable connection. When you're done using the connection, click Disconnect in the main X-ISP window. You should see PPP Link is Down displayed; and you may hear your modem *click* as it goes off-line and see its lights change, if it's an external model.

> Caution
> *Remember to disconnect when you're done using your PPP connection. If you don't, and if your ISP doesn't have an auto-disconnect feature and you pay per-minute connection charges, you may see a huge bill because of a careless failure to disconnect!*

## Using Text-Mode Dialing Tools

GUI PPP dialers are convenient for individual users, but they aren't always the best method of making a connection. You may want to use text-based Internet tools without running X at all, or you may want to run cron jobs that bring up a connection and perform some automated task, such as retrieving e-mail. You can use the `pppd` program upon which X-ISP relies more directly to accomplish these goals. To use pppd, your kernel must include PPP support (as it does by default).

> **Note**
>
> There's a user-mode PPP tool, in addition to the kernel-mode tool described here. The user-mode tool is called *chat*, and it's configured using the `/etc/ppp/pap.conf` file. The user-mode PPP tool is described in the upcoming section, “Configuring PPPoE,” with reference to PPPoE configuration, although its use isn’t restricted to PPPoE.

## Editing Support Files

Before you begin configuring either kernel- or user-mode PPP, you should see to the status of certain support files. One of these is the *secrets file* (*pap-secrets* or *chap-secrets*, depending upon whether your ISP uses PAP or CHAP). This file is described in the earlier section, “Creating a Secrets File.” It’s configured the same way for a dialing script as for a GUI dialing tool.

Another important support file is the `/etc/resolv.conf` file, which lists your ISP's DNS servers. This file is described in the “Setting Up Hostname Resolution” section of Chapter 14, so read it for more information. Some ISPs configure their dial-in systems to give you this information automatically, but this process often doesn't work correctly, so you may need to configure it manually. Ask your ISP for the IP addresses of its DNS servers, if they don’t provide you with this information initially.

## Configuring Kernel PPP

Kernel PPP configuration requires editing or creating at least two files: a PPP options file and a *chat script*. The latter is a series of strings sent to the modem and the expected responses from the modem. The chat script enables *pppd* to dial the modem and, if necessary, issue commands to log into your ISP. Normally, you must also configure a *pap-secrets* or *chap-secrets* file, as described earlier, in “Creating a Secrets File.” Once you’ve created the necessary configuration files, you can call *pppd* with the options required to call your ISP.

### Editing /etc/ppp/options

The `/etc/ppp/options` file controls most *pppd* options, aside from the secrets used for PAP and CHAP authentication. (It’s also possible to pass options as parameters in the call to *pppd*.) Listing 15-1 shows a typical options file.

![](img/f34d37e3abe9f4517128e54f80ab2616_424_0.png)

```
`15.1 Sample /etc/ppp/options File`

    /dev/cua0 115200
    crtscts
    modem
    noipdefault
    silent
    defaultroute
```


You should also see the modem's response to the line: OK. If you're familiar with modem commands, you might want to change the initialization string, but you shouldn't do that here unless you plan to use minicom extensively; for a PPP connection, you should customize the PPP dial scripts. You can type other AT ("attention") commands at this prompt, including ATDT to dial the modem—for instance, ATDT555-1234 dials the phone number 555-1234. You might want to try dialing your ISP or some other number you know will connect to a computer to test basic functionality.

## NOTE

If you try to connect to your ISP with a terminal program, chances are you won't get anything intelligible on the screen. You might get a CONNECT message indicating that the modem has connected, and possibly some sort of banner in English, but then you'll probably see gibberish, followed by a NO CARRIER message. This is normal; it indicates that the remote system attempted to use an authentication protocol such as Password Authentication Protocol (PAP) or Challenge Handshake Authentication Protocol (CHAP), but failed, which is understandable because you weren't running your PPP startup scripts.

minicom uses command keys prefixed by Ctrl+A, so to control the program, you start by pressing Ctrl+A. If you follow Ctrl+A with Z, minicom displays the menu shown in Figure 8.1. After you've finished your check of basic functionality, you probably want to exit from minicom, which you can do by pressing Ctrl+A, and then either X or Q.

![](img/5d4d3092919d1d16884788127447cc6d_213_0.png)

## FIGURE 8.1

Whatever you type in minicom normally goes directly to your modem, but if you first press Ctrl+A, minicom interprets the next character as a command.

If you have problems at this stage, you should resolve them now, or you probably won’t have much luck with PPP. Table 8.1 lists some common modem problem symptoms and possible solutions.

**Table 8.1  Modem Troubleshooting Tips**

| Symptom | Possible Causes/Solutions |
|---|---|
| `minicom` won’t run; get a `NO GLOBAL CONFIGURATION FILE` message | As root, run `minicom -s`, enter configuration data, and then save it as `df1`. |
| `minicom` won’t run; get a `PERMISSION DENIED` message | Run `minicom` as root. Alter permissions on serial port device. |
| No response from modem | The modem is not turned on. The modem is a Windows-only model. Attempting to use the wrong device file. Linux serial device driver is not loaded; use `cat /proc/interrupts` and check for a serial device interrupt. Bad modem cable, or cable plugged into wrong port. |
| Can dial, but get gibberish from ISP | This is normal when dialing an ISP that expects to make a PPP connection. |

## PPP Authentication

When you dial an ISP to make a PPP connection, the ISP wants to know who you are for both security and accounting purposes. The process by which you (or your dialing scripts) confirm your identity to your ISP is known as authentication, and there are several different methods of authentication in use today:

- **Manual login—**If you dial your ISP and get a prompt asking for your username and password, it’s likely that your ISP supports a manual login procedure. This doesn’t mean that a manual login is your *only* option, though. Manual login is distinctly antiquated by today’s standards, and few ISPs require manual logins. If yours does, you can create a login script to supply appropriate information at appropriate times, but given the scarcity of systems requiring this procedure, this book doesn’t cover creating such a script.
- PAP—PAP is one of the most popular authentication methods in use today. On recent versions of Linux, it requires that you create a special file containing your username and ISP password. The PPP dialing utilities then read this file and send the appropriate password when asked for it.
- CHAP—CHAP works very much like PAP in practice, although it varies in its internal details. As with PAP, you create a special file with your username and password, and the PPP dialer uses that file when the ISP asks who’s calling.

In the case of PAP and CHAP, the password files are /etc/ppp/pap-secrets and /etc/ppp/chap-secrets, respectively. Red Hat Linux includes samples of these files in the ppp package, which you should install if it’s not already installed on your system. The Red Hat sample secrets files are very minimal—they contain no entries, just comments. In order to provide the best security, these files should have permissions set to -rw------- (600 in octal notation), meaning that only the owner (root) can read or write the file. Each of these files can contain separate authentication for different ISPs or users, one authentication per line. The information on each line is the same for both files:

```
client  server  secret  IP address
```

The meaning of each field is:

- client—Your username on the ISP’s system.
- server—The name of your ISP’s server. If you don’t know the server’s name, as you probably don’t for most ISPs, you can use an asterisk (*) here.
- secret—Your password, which is stored in plain text in this file, which is why it’s important that this file not be readable by anybody but root.
- IP address—The IP address you’ll be assigned by the remote system. In most cases, you don’t know what this will be ahead of time, so you should leave this field blank.

## Tip

> If you don’t know whether your ISP uses PAP or CHAP, you can create one file—say, pap-secrets—and create a link for the other file to the one you’ve created. Your system will then use the same secrets file for both PAP and CHAP.

As an example, here’s a pap-secrets/chap-secrets file that can be used by three individuals on a single client to connect to three different PPP accounts, which might be on the same or different ISPs:

```
elmo  sesame  elmopw  192.168.1.101
bert  *       bertpw
ernie *       erniepw
```

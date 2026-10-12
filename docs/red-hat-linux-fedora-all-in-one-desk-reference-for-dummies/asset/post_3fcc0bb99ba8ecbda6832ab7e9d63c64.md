
If you see a message such as the following, then Linux has detected a serial port in your PC:

```
ttyS0 at 0x03f8 (irq = 4) is a 16550A
```

In this case, the message indicates that the Linux kernel has detected the first serial port (COM1). It shows the I/O address (in hexadecimal), 0x3f8, and IRQ 4. The last part of the message — 16550A — refers to the identifying number of the universal asynchronous receiver/transmitter (UART) chip, which is at the heart of all serial communications hardware (the UART converts each byte to a stream of 1s and 0s, and vice versa when it receives such a stream).

You can also check for the serial ports with the setserial command. Type the following command to see detailed information about the serial ports:

```
setserial -g /dev/ttyS?
```

Any device that is listed in the output of this command with an unknown UART is either not installed or not detected by the Linux kernel.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_329_0.png)

## Testing the modem

After you complete the physical installation of the modem and verify that the Linux kernel detected the serial port, you can try to dial out through the modem. The best approach is to use the Minicom serial communications program that comes with Red Hat Linux.

Minicom is similar to other communications software, such as Procomm or Crosstalk, that you may have used under MS-DOS or Windows.

To run Minicom, log in as root and type minicom at the shell prompt in the terminal window (or in a virtual console). Minicom runs and resets the modem. Figure 1-8 shows the result of running Minicom in a terminal window.

If you don't see the OK, it probably means that this particular serial-device name is not set correctly. To set the serial device, follow these steps:

- 1. Press Ctrl+A and then Z.
- Minicom displays its help screen.
- 2. Press O.
- Minicom displays its configuration menu.
- 3. Use the arrow key to select Serial port setup and press Enter.
- Minicom displays the serial port settings.
- 4. Press A.

Minicom puts the cursor in the line that shows the serial-device name. Edit the device name to match where your modem is connected. For example, if the modem is on the first serial port, make sure that the device name is /dev/ttyS0.

- 5. Press Enter twice.
- Minicom returns to the configuration menu.
- 6. Select Save setup as dfl and press Enter.
- Minicom saves the settings.
- 7. Select Exit and press Enter.
- Minicom returns to online mode.
- 8. Press Ctrl+A and X.
- Minicom prompts you to ask whether you really want to exit.
- 9. Press Enter to exit.
- After setting the correct device name for the serial port where the modem is connected, make sure that your modem is powered on and connected to the phone line.
- 10. Start Minicom again (type minicom in the terminal window).
- 11. Press Ctrl+A to get the attention of the Minicom program.
- After you press Ctrl+A, if you press Z, a help screen appears in the form of a text window. In the help screen, you can get information about other Minicom commands.

Figure 1-8: You can test your modem manually with Minicom.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_330_0.png)

12. From the help screen, press Enter to go back to online mode.

In online mode, you can use the modem's AT commands to dial out. In particular, you can use the ATDT command to dial the phone number of another modem (for example, dial your ISP's number). When you get the login prompt, you know that the modem is working. Figure 1-9 shows the results of a typical dial-up using Minicom: only 38.4 Kbps with a 56 Kbps modem. (No wonder I needed DSL or cable modem!)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_331_0.png)

Figure 1-9:
Use the ATDT command to manually dial out using Minicom.

13. To exit Minicom, press Ctrl+A and then type X.

14. Press Enter again to close Minicom.

## Setting up and activating a PPP connection

Most ISPs provide PPP dial-up access to the Internet through one or more systems that the ISP maintains. If you sign up for such a service, the ISP should provide you the information that you need to make a PPP connection to the ISP's system. Typically, this information includes the following:

- The phone number to dial to connect to the remote system
- The user name and password that you must use to log in to the remote system
- The names of the ISP's mail and news servers
- The IP address for your PPP connection. ISP does not provide this address if the IP address is assigned dynamically (this means the IP address may change every time your system establishes a connection).
- IP addresses of the ISP's Domain Name Servers (DNS). The ISP does not provide these addresses if it assigns the IP address dynamically.

Of this information, the first two items are what you need to set up a PPP connection.

Follow these steps to set up a PPP connection using Red Hat's Internet Configuration Wizard:

- 1. **Log in as root and choose Main Menu→System Tools→Internet Configuration Wizard from the GNOME desktop.**

If you are not logged in as root, type the `root` password when you're prompted for it.

The Select Device Type dialog box appears (as shown in Figure 1-10).

![](img/a7eec43a54473e95dc5ea333fecf1bd7_332_0.png)

Figure 1-10:
Configure the Modem connection from this dialog box.

- 2. **Select Modem connection from the Device Type list, and then click Forward.**

The Select Modem dialog box shows information about your modem.

- 3. **Click Forward to continue.**

The Select Provider dialog box appears.

- 4. **Fill in the connection information — the ISP's phone number, your login name, and password — in the text boxes (shown in Figure 1-11); click Forward to continue.**

Figure 1-11:
Fill in the connection information in this dialog box.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_333_0.png)

5. Enter the IP settings — whether you want to automatically get an IP address or provide a static IP address — and then click Forward to continue.

Typically, you would select the option to automatically obtain an IP address and name server settings from the ISP.

6. Click Apply to save the dial-up configuration information, and then close the Internet Configuration Wizard.

The Network Configuration dialog box appears with the name of the new dial-up connection in a list (Figure 1-12).

Figure 1-12:
Click Activate in the Network Configuration dialog box to establish the PPP connection.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_333_1.png)

7. Select the connection name, and then click Activate.
8. When you're done, click Deactivate to turn the PPP connection off.

## Configuring CHAP and PAP authentication

The PPP server on your system has to authenticate itself to the ISP's PPP server before the PPP connection can get fully up and running. Authentication requires proving that you have a valid account with the ISP; essentially this involves providing a user name and a secret (that is, a password). PPP specifies two ways of exchanging the authentication information between the two ends of the connection:

- **Challenge Handshake Authentication Protocol (CHAP)** requires the remote end to send a randomly generated challenge string along with the remote server's name. The local system looks up the secret, using the server's name; then it sends back a response that includes its name and a value that combines the secret and the challenge, using a one-way hash function. The remote system then checks that value against its own calculation of the expected hash value. If the values match, the authentication succeeds; otherwise, the remote system terminates the connection. In this case, the name and secret are stored in the `/etc/ppp/chap-secrets` file. Note that the remote system can repeat the CHAP authentication any time while the PPP link is up.
- **Password Authentication Protocol (PAP)** is like the normal login process. When using PAP, the local system repeatedly sends a username (name) and password (secret) until the remote system acknowledges the authentication or ends the connection. The name and secret are stored in the `/etc/ppp/pap-secrets` file. Note that the user name and password are sent in the clear (that is, unencrypted).

The Linux PPP server supports both types of authentication. For both PAP and CHAP, the information that the PPP server needs is a name and a secret — a username-password pair. This authentication information is stored in the following configuration files:

- `/etc/ppp/chap-secrets` stores the information for CHAP. Here's what a typical chap-secrets file looks like:

```
# Secrets for authentication using CHAP
# client    server    secret    IP addresses
"naba"      *        "mypassword"
```

- `/etc/ppp/pap-secrets` stores the information for PAP. Here's a typical pap-secrets file:

```
# Secrets for authentication using PAP
# client    server    secret    IP addresses
"naba"      *        "mypassword"
```

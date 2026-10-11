+   * **Fax features** The capability to both send and receive faxes is standard on modern modems. As a general rule, you should look for a modem that supports Class 2.0 fax protocols, which impose the least overhead on the sending applications. In Linux, programs such as `mgetty+sendfax` (`http://alpha.greenie.net/mgetty/`) or HylaFax (`http://www.hylafax.org/`) handle sending and receiving faxes. Unfortunately, most of these programs are far less user-friendly than are their Windows equivalents. Matters are improved somewhat by fax front-end programs like GFax (`http://www.gmsys.com/gnome-gfax.html`), which provide an easy-to-use GUI atop the underlying fax software.

+   * **Voice features** Some modems support voice functionality. You can use these modems as speakerphones, answering machines, or voicemail systems. Linux support for these devices exists, but is extremely crude compared to the user-friendly Windows voicemail programs for the same hardware. The main Linux package for voice modems is `vgetty` (`http://alpha.greenie.net/vgetty/index.html`). This is a variant of the `mgetty+sendfax` package.

# ## Using Modems for PPP Internet Connections

You can use a modem to connect your Linux computer to the Internet using the *Point-to-Point Protocol* (PPP). Most Linux distributions today include tools to help you manage a PPP dial-up account. For instance, the *K Desktop Environment* (KDE), which is the default desktop on many Linux installations, includes a program called *kppp*, shown in Figure 18.3. When you click the Setup button in the main window, you get the *kppp Configuration* window shown in the foreground. You can enter information on your PPP account in this window much as you would enter information in a Windows PPP dialer: When you're done, you can connect to your ISP by clicking the Connect button in the main *kppp* window. Other GUI PPP dialers function in a similar fashion, although the details differ.

Depending upon the authentication method you use, you might need to take one additional step: You might need to add your username and password to the `/etc/ppp/pap-secrets` or `/etc/ppp/chap-secrets` file, depending upon whether your ISP uses PAP or CHAP authentication. These files are readable only by *root*, and they contain your sensitive passwords. An example is

```
# client  server secret    IP addresses
rootsmith *   password
```

This sample file allows the user *rootsmith* to log in to a PPP server using the password *password*. In most cases you want to leave the *server* field set to an asterisk (*), which allows a login to any server. If you're assigned a static IP address by your ISP, you can enter it in the final IP addresses field; otherwise, leave that field blank.
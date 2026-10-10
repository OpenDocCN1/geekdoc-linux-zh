+   * enable DNS—This option causes PPP to check with your ISP to see whether the DNS servers you have listed in /etc/resolv.conf are correct. If they aren’t, PPP will update the file automatically with the servers suggested by the ISP, creating persistent entries that will last until you (or PPP) modify the file again.
+   * set phone—This option replaces PHONE_NUM with the phone number you use to connect to your ISP.
+   * set autname—This option replaces USERNAME with the login name that you use to connect to your ISP.
+   * set authkey—This option replaces PASSWORD with the password you use for your ISP.

If you can’t use PAP or CHAP and need to use a standard Unix shell login instead, you must make some more changes to the default configuration file. First, remove the papchap section, including the set phone, set autname, and set authkey statements. Next, add the following lines after the set dial statement:

```
Provider:
set phone "5551212"
set login "TIMEOUT 10 \ \" gin::-g1n: foo sword: bar"
```

Once again, replace foo and bar with your ISP login name and password, respectively. As with kernel PPP, include after the password any other commands you need to send to start PPP on the remote host. Like the chat script in kernel PPP, this script uses an “expect/send” syntax, in which you type what it should expect to receive from the server and then what it should respond with.

> **TIP**
> If you are unsure about which prompts your ISP sends, use a terminal emulator such as minicom (available in the ports tree) to dial your ISP’s phone number and then perform a manual login. That way, you can observe what prompts the ISP’s server sends when requesting various items of information.

# Starting User PPP

If you are using PAP or CHAP authentication, you can start user PPP from the command line by typing ppp -background papchap. If you are using a shell login instead of CHAP or PAP, use the ppp -background provider instead. The ppp -background provider starts user PPP in the background. If all goes well, you should hear your modem dial, and after a connection has been established, the system will respond with PPP Enabled and then return you to a command prompt.

![](bbox=[0.95, 0.27, 1.0, 0.37])
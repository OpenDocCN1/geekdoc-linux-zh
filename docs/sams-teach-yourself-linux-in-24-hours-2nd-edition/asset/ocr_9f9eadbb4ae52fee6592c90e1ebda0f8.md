Here is the step-by-step method. You can do this because one of minicom's features is that it has the capability to quit without resetting your modem. This means you can use minicom to dial out, connect, and then quit, enabling you to start your PPP session with the pppd daemon. Make sure you enter your ISP's DNS server information in /etc/resolv.conf first! Here's how:

+   1. Run minicom.
+   2. Type ATDT, followed by your ISP's modem number.
+   3. Wait for the connection and your ISP's prompt, and then log in with your username and password. Note whether the login and password prompts are different. If so, write them down so you have the information you need to edit the chat program options in your ppp-on-dialer script. After you type your password and press Enter, you might see a string of garbage characters sent back from your ISP's computer; this is normal and indicates your ISP's computer has started PPP.
+   4. Press Ctrl+A, and then press Q to exit minicom without a modem reset.
+   5. From the command line, log in as the root operator, and then type the following:

```
# pppd -d detach /dev/modem &
```

After a second or so, you're connected! (Well, check first—try some of the programs discussed later.)

# Using Your ppp-on Script to Connect

Using the ppp-on script to establish your PPP connection is easy. Make sure you're logged in as root, and type the following to start the connection:

```
# /etc/ppp/ppp-on
```

![](bbox=[0.15, 0.83, 0.2, 0.92])

> You don't have to log in as the root operator to start a PPP connection with the ppp-on script. Use the su command instead, like so:
> 
> su -c /etc/ppp/ppp-on
> 
> Press Enter. After you enter the root password, the script runs.

Notice that you have to type the entire pathname to the script. If your connection works, you can either move the script to the /usr/local/bin directory or make a symbolic link to the script with the following (you can call it whatever you want; just don't use pppd):

```
# ln -s /etc/ppp/ppp-on /usr/local/bin/start-ppp
```
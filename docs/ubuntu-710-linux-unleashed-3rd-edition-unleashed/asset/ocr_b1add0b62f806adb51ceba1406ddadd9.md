To enable sharing, you must follow a few steps, because by default CUPS is not set up to share printers across a network.

First, edit your `/etc/cups/cupsd.conf` file using the following command:

```
```bash
$ sudo gedit /etc/cups/cupsd.conf
```
```

In this example I have used gedit, but feel free to substitute in your favorite text editor.

Then, look for the section that begins with `<Location />` and modify it so that it reads as follows:

```
```text
<Location />
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
Allow From 192.168.0.*
</Location>
```
```

This tells CUPS to share your printers across the network 192.168.0.*, for example. Make sure and change this to match your own network settings.

Next you need to look in the same file for the section that starts

```
```text
Listen localhost:631
```
```

and modify it to show this:

```
```text
Listen 631
```
```

This tells CUPS to listen on port 631 for any print requests. All you need to do now is open up `system-config-printer` on your clients and select Detect LAN Printers under the Global Settings menu. After a few short moments, the printer should pop up in your window, as shown in Figure 16.7

![](bbox=[0.082, 0.681, 0.489, 0.87])

**FIGURE 16.7**  The highlighted printer has been shared across the network. Ubuntu makes this process as painless as possible.
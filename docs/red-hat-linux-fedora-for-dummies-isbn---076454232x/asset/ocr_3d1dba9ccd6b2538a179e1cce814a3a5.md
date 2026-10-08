4. **Enter** `/etc/sysctl.conf` **in the** Selection **text box and click the** OK **button.**

The gedit program displays the contents of sysctl.conf, as shown in Figure 15-3.

5. **Locate this line (which should be close to the top of the file):**

```
```
net.ipv4.ip_forward = 0
```
```

6. **Change the** 0 **to a** 1:

```
```
net.ipv4.ip_forward = 1
```
```

7. **Click the** Save **button and then choose** File **\> Quit to close** gedit.

You can view the change by clicking the Nautilus Refresh button. You have to restart Linux networking for the change to take effect.

8. **Open the** Service Configuration **utility by clicking the** GNOME Menu **button and choosing** System Settings **\> Server Settings\>** *Services*.

9. **Enter the** root **password, if you're prompted.**

10. **Locate and click the** Network **service.**

11. **Click the** Restart **button to turn on IP forwarding.**

![](bbox=[0.14, 0.51, 0.74, 0.85])
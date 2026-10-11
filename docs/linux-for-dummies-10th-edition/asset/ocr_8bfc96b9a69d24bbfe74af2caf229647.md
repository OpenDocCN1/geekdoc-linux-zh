![](bbox=[0.15, 0.07, 0.2, 0.14])

If you created only the root account, you can log in there as root.

After you enter the username and password, you find yourself at the screen shown in Figure 22-2, which just happens to be the second spot where people get worried. If you see this screen, you have not only booted properly into Linux, but you’re also logged in and using the machine! Give yourself a good pat on the back.

```
ubuntu 20.04 LTS ubuntu20 tryd
Ubuntu20 login: rish
Password:
Welcome to Ubuntu 20.04 LTS (GNU/Linux 5.4.0-57-generic x86_64)
* Documentation: https://help.ubuntu.com
* Management: https://landscape.canonical.com
* Support: https://ubuntu.com/advantage


N updates can be installed immediately.
1 of these updates are security updates.
To see these additional updates run: apt list --upgradable

4 updates could not be installed automatically. For more details, run:
/usr/lib/apt/apt.systemd-updates.d/unattended-upgrades.log
New release 'Ubuntu 22.04' is available.
Run 'apt list --upgrgradable' to see updates available.
Last login: Fri Jun 14 10:20:14 EDT 2020 from 192.168.1.28 on pts/1
[rish@ubuntu2020r ~]$
```

![](bbox=[0.15, 0.5, 0.25, 0.59])

What do you do from here? Anything you want. Surf through this book for commands you want to run. Type startx to start up the GUI. If you didn’t install any GUI (which means you selected a minimal install option with no graphical interface, or you actually unselected graphics), you may want to reinstall, or you have to add all the tools by hand (which is not a quick job! ).

# Tip #6: “I Don’t Want to Boot into This!”

Are you booting into the command-line environment when you want to use only the GUI? Or are you finding that you’re already booting into the GUI and you would rather boot to that nice, clean, black-and-white command line screen? You’re not stuck with either of these options. You can change them at any time.
sample configurations in the NetBox documentation are just that and might need to have something added, re-moved, or otherwise changed in order to work properly.

NetBox now will tell you to restart the NetBox services (Figure 6). If you restart at this time, you will get the failure to restart message shown in Listing 4. You get the failure message because you have not yet created those services.

If you decide for whatever reason that you no longer want a plugin, then you can simply remove it from both files. If you are unsure, or if you would like to temporarily disable a plugin for some reason, then you can do so by removing it from conf\_guara- tion.py but leaving it in local\_require- ments.txt. In order to enable or disable a plugin, you will need to restart the NetBox service, which I will explain shortly.

You now need to create the NetBox su-peruser by entering:

```
`$ source /opt/netbox/venv/bin/activate`

The (venv) added to the command prompt is normal. Now, add the superuser:
```

```
`(venv) $ cd /opt/netbox/netbox
(venv) $ python3 manage.py`

`creatersuperuser`

You can use a deactivate command to leave the virtual environment and get
```

![](bbox=[0.05, 0.6, 0.95, 0.92])

back to a normal terminal window, but I usually found myself closing and opening a new terminal (or rather refreshing the page because I was connected using Cockpit).

With the superuser added, you will want to add the housekeeping script as a cron job to occasionally do some cleanup. To do this, add a link to the script in the cron.daily folder as follows:

```
`$ sudo ln -s /opt/netbox/contrib/`
`netbox-housekeeping.sh /etc/cron.daily/netbox-housekeeping`

At this point, you should have a running NetBox instance that you can connect to by entering the IP address or hostname that you defined earlier in conf\_guara- tion.py. You will need to have the Un- complicated Firewall (UFW), which might require running:
```

```
`$ sudo ufw allow 9090
$ sudo ufw allow OpenSSH
$ sudo ufw allow https
$ sudo ufw allow http`
```

# Listing 5: Creating Services

```
```python
01 $ sudo cp /opt/netbox/contrib/gunicorn.py /opt/netbox/gunicorn.py
02 $ sudo cp -v /opt/netbox/contrib/*.service /etc/systemd/system/
03 $ sudo systemctl daemon-reload
04 $ sudo systemctl start netbox netbox-rq
05 $ sudo systemctl enable netbox netbox-rq
06 $ systemctl status netbox.service
```
```

```
`$ sudo ufw enable
$ sudo ufw status`
```

I added ports 9090 and 22 because I was using Cockpit and also wanted the ability to connect to this server using SSH, but that is beyond the scope of this article. If you don't know how to SSH into a server or haven't installed and used Cockpit or a similar server admin web GUI such as Webmin, I suggest you do those things first, because it will help to familiarize you with running servers without a GUI from the terminal. You can connect to your machine with SSH or Cockpit even if you are running the desktop version of Ubuntu.

# Creating Services

You will now want to copy the default Gunicorn [16] configuration and create the services to turn NetBox on and off using the code in Listing 5.

The code in Listing 5 copies the de- fault Gunicorn config file and then cre-ates the NetBox system service, starts it, enables it to run each time the system
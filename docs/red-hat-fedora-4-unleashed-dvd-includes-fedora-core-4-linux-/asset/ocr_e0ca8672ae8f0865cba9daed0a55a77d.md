You need to perform a few steps before you can start using SWAT. First, make sure you have the Samba and the samba-swat RPM packages installed. You then enable SWAT access to your system by editing the /etc/xinetd.d/swat file by changing the following line:

```
disable = yes
```

Change the word yes to the word no, like so:

```
disable = no
```

Save the file, and then restart the xinetd daemon, using either the system-config-services client or the xinetd shell script under /etc/rc.d/init.d like so:

```
# /etc/rc.d/init.d/xinetd restart
```

Next, start an X session, launch the Mozilla web browser, and browse to the http://localhost:901 uniform resource locator (URL). You are presented a login prompt. Enter the root username and password, and then click the OK button. The screen clears, and you see the main SWAT page, as shown in Figure 21.2.

> **TIP**
> 
> You can also configure Samba using Red Hat's system-config-samba client. Launch the client from the command line of an X terminal window or select the System Settings, Samba Server menu item (as shown later in Figure 21.9).

# sample_database

# phonebook

| last_name | first_name | phone |
|---|---|---|
| Doe | John | 555-555-1212 |
| Doe | Jane | 555-555-1212 |
| Palmer | John | 555-123-4567 |
| Johnson | Richard | 555-111-4321 |

# cd_collection

| id | title | artist | year | rating |
|---|---|---|---|---|
| 1 | Mind Bomb | The The | 1989 | 4 |
| 2 | For All You've Done | Hillsong | 2004 | |
| 3 | Trouser Jazz | Mr Scuff | 2002 | 5 |
| 4 | Natural Elements | Acoustic Alchemy | 1988 | 3 |
| 5 | Combat Rock | The Clash | 1982 | 4 |
| 6 | Life for Rent | Dida | 2003 | |
| 7 | Aidermus 4 | Karl Jenkins | 2000 | 5 |
| 8 | The Two Towers | Howard Shore | 2002 | 5 |

![](bbox=[0.078, 0.84, 0.934, 0.86])

First, click the GLOBALS icon in SWAT's main page. You see a page similar to the one shown in Figure 21.3. Many options are in the window, but you can quickly set up access for hosts from your LAN by simply entering one or more IP addresses or a subnet address (such as 192.168.2.—note the trailing period, which allows access for all hosts; in this
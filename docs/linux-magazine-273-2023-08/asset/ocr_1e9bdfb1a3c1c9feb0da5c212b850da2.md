Some users may not need to see a par-\nticular section, so you can simply not\ngive them that access. This is also useful\nif you have users from different sites or\nlocations all connecting to your NetBox\ninstance. In this instance, users may\nhave the ability to only change items\nwithin their location or site as needed.

Permissions are a big deal and need to\nbe well thought out. Remember, these are\nthe keys to the kingdom. Even if that isn’t\nreally the case for your organization, it is\nprobably a safe approach to NetBox.

# Conclusion

When I first started reading about Net-\nBox, I found their aim of being “the pre-\nmiere network source of truth” kind of\ncheesy. It’s just a web GUI for a network\nmap with some stuff from a database\nafter all. Since installing and using it,\nhowever, I’m a true believer. I think\n\n56 | AUGUST 2023 | ISSUE 273 | LINUX-MAGAZINE.COM\n\nevery single networker should be mapp-ed\nout using NetBox. I have installed the\ncommunity edition at work as well as on\nmy home network. It really is your net-\nwork’s “truth” – or at least it becomes\nthat once you put in the work.

I am still in the process of document-\ning the network in my organization. It is\nan enormous task and one that never\nends, because updates will need to be\nmade as the network expands, contracts,\nand changes. My intent is to build Net-\nBox out thoroughly enough that I can\ngive a new employee a login to NetBox\nso they can find their way around the\nentire organization, even if they aren’t\nable to access everything that they see in\nthere. I also need to add maps for each\nbuilding in the NetBox’s location

section, which I could do by simply up-\nloading PNG images of our physical\nmaps. I might not give a new employee\nthe credentials for our building’s\nswitches, but they will know where the\nswitches are located, what devices con-\nnect to them and through which ports,\nand the IP addresses those devices have,\nas well as be able to very quickly and\neasily find product information. NetBox\nwill give new employees all that they\nneed to know about the devices that\nthey will work on to be able to effec-\ntively and efficiently do their jobs. With\ndozens of printers and hundreds of PCs\non our network, the ability to pinpoint\none device and its connection to a spe-\ncific switch by searching for a room or a\nbuilding, and to have a link to the user’s\nguide and installation manual, drivers\ndownload page, specifications, asset tag\nnumber and corresponding serial num-\nber, and so on, will greatly improve team\nefficiency in the long run, though it will\nabsolutely take time to implement. None\nof that time is wasted, however, because\nanyone who is mapping out the network\nin NetBox is also learning all of the ins\nand outs of it simultaneously.

Something incredibly important that I\ndidn’t focus on in this article: Knowing\nwhat is on your network and where that\ngear is located is critical to network secu-\nrity and is connected directly to CIS\nSafeguards numbers 1.1, 1.2, 1.3, 2.4, 6,\nand many others in the CIS Risk Assess-\nment Methodology (RAM)\[18\].

Initially, I found a ton of overlap be-\ntween tools that we were already using\nand NetBox. However, to add more devices\nto the database and put in more details\nabout each device, I realized that I had\nbeen looking at it all wrong. While alter-\nnates exist to basically all of NetBox’s func-\ntions, the disconnect between the individu-\nal programs and services creates ineffi-\nciency. NetBox offers a fantastic opportu-\nnity for long-term improvement in network\nmanagement. NetBox, if well-imple-\nmented, will act as a central knowledge\nhub for the network, with each of those\nother programs and services functioning as\nspokes off of that hub. NetBox doesn’t lay\nover the top of your existing management\nstack, but instead coalesces with it in a\nway that empowers your IT team. While\nNetBox may initially look like a lot of work,\n\nLINUX-MAGAZINE.COM | ISSUE 273 | AUGUST 2023 | 56

# Info

+   \[1\] NetBox: https://github.com/\nnetbox-community/netbox/wiki\n\[2\] NetBox demo:\nhttps://demo.netbox.dev/login/next/\n\[3\] Ubuntu: https://ubuntu.com/\n\[4\] Level1 Techs Guide to NetBox:\nhttps://forum.level1techs.com/t/\nnetbox-ipam-dcim-guide/132435\n\[5\] PostgreSQL: https://postgresql.org/\n\[6\] Redis: https://redis.io/\n\[7\] Python: https://www.python.org/\n\[8\] Cockpit: https://cockpit-project.org/\n\[9\] 45Drives cockpit-navigator: https://\ngithub.com/45Drives/cockpit-navigator\n\[10\] nano: https://www.nano-editor.org/\n\[11\] Vim: https://www.vim.com/\n\[12\] Django: https://www.djangoproject.com/\n\[13\] NetBox Community Plugins: https://\nnetbox-community/\n\[14\] gedit: https://github.com/GNOME/gedit\n\[15\] Gnome Text Editor: https://gitlab.\ngnome.org/GNOME/gnome-text-editor\n\[16\] Gunicorn: https://gunicorn.org/\n\[17\] NGINX: https://www.nginx.com/\n\[18\] CIS RAM: https://ciscocite.org/\ninsights/white-papers/cis-ram-risk-\nassessment-method

# Author

Adam Dix, a former\nteacher and product\nline manager, is a\nmechanical engineer\nand Linux enthusiast\nworking as a LAN\ntechnician. You can\ncheck out some of his related work at\nEduBUbDie Linux (https://edubudgie.com).

![](bbox=[0.79, 0.8, 0.94, 0.94])

![](bbox=[0.06, 0.65, 0.62, 0.91])

Figure 9: When you first connect to your NetBox installation you may\nget a privacy warning if you use a self-signed SSL certificate.
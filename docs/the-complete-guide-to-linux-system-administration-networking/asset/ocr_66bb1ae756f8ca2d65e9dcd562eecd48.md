3. If this still didn’t work, consider the address itself. It apparently refers to NVCC within some larger unit, vccs—probably the Virginia Community College System, or something like that. With this theory in mind, try a query to the Educause-whois server using just vccs.edu. What results do you see?

```
whois -h whois.educause.net vccs.edu
```

4. You are concerned that the VCCS people may not have direct authority over the NVCC servers, so you decide to try the other NVCC address to see if you can locate someone at that school. Run a whois query for nv.cc.va.us (You might want to view both www.nv.cc.va.us and www.nvcc.vccs.edu in your Web browser first to check that they are valid domains.) Where did you query for nv.cc.va.us? What result did you see, and why did you get that result?

```
whois -h whois.educause.net nv.cc.va.us
```

5. Concerned that you haven’t been able to find the contact person yet at NVCC, you decide to try the University of Virginia site, uva.edu. Make this whois query. Sometimes a query directly to whois.internic.net can connect directly to another whois server such as educause.net. Other times you may need to specify Educause.net as your whois server.

```
whois -h whois.educause.net uva.edu
```

6. From the information listed, obtain the IP addresses of the DNS servers and the name, phone, and e-mail address of the contact person. You should check with the contact person as a courtesy before referencing their DNS servers. Log off.

# Project 15-4

In this project, you experiment with the NFS protocol. The steps describe the procedure on Red Hat Linux and Fedora, but they should be substantially equivalent for any Linux distribution. To complete this project, you should have the NFS daemons installed. Be aware that if you used a High Security setting when you installed Linux, or otherwise set up firewalling, the procedure may not work. If you are in a safe lab environment, you can delete all firewall rules on the system and set all default firewall policies to ACCEPT by issuing the following commands while logged in as root:

```
iptables -F
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
```

For this project you should work in teams; one Linux system should be designated as the NFS server and the other as the NFS client. You should have root access to both systems.

+   1. Log in to the server, open a command-line window and change to root access. Then edit the /etc/exports file and add the following line, substituting the host name of your client system where indicated:
+   
+   /usr/share/doc client_host(all_squash,rw)
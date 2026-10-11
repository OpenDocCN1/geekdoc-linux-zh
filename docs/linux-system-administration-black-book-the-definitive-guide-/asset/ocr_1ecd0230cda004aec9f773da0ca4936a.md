making access to your user information even more difficult for outsiders.
For example, I might choose animals.nis as my NIS domain, though this might be too easy for intruders to guess in a real-world situation.

+   20.  Put the NIS domain into place by typing `/bin/domainname ntsdomain`.
+       For example, `/bin/domainname animals.nis`.

+   21.  Type `/usr/lib/yp/ypinit -m` to start the program that builds your map files.
+       This is an interactive program. This is the first text you see:

```
At this point, we have to construct a list of the hosts
which will run NIS servers. localhost.localdomain is in the
list of NIS server hosts. Please continue to add the names
for the other hosts, one per line. When you are done with
the list, type a <control D>.

next host to add: localhost.localdomain
next host to add:
```

+   22.  Add the full *host.domain.extension* for each machine that needs access to the NIS server. Press Enter between each name, because the program adds one host at a time.

+   23.  After you enter the last host, press the key combination Ctrl+D. This ends the host addition process and displays a list of the hosts that you entered, asking you whether the information was entered correctly. If yes, type “y” and proceed. If not, type “n” and reenter the hosts.

+   24.  The **ypinit** program now creates all the map files and other items that the NIS server needs.

| Related solution: | Found on page: |
|:------------------|:---------------|
| Restricting Network Access With **tcp_wrappers** | 267 |

# Setting Up An NIS Client

To set up an NIS client under Red Hat Linux, do the following:

+   1.  Log in as root to the client machine you want to set up.
+   2.  Ensure that you followed the instructions in the section “Installing The NIS Client,” so that you have the client software already installed.
+   3.  Type “/etc/yp.conf” to open the **ypbind**—the program that connects to the NIS server and manages communication with that server—configuration file.
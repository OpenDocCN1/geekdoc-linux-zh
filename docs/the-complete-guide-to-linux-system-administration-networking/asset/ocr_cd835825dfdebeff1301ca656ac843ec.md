10. Close the program by pressing Ctrl+c on your friend's system or choosing Quit from the File menu on your screen (within gedit).

11. Though you trust your friend, the next time you log out of X and log in again, a new xauth cookie is generated automatically, so your friend is not able to use your system as an X server unless you hand over your cookie again. Log off.

# Project 15-2

In this project, you experiment with the nmap port-scanning utility. You should work in a lab for this project. In the steps, the host name target.edu has been used; replace this with the IP address or host name of any single system in your computer lab. To complete this project you should have Linux installed and have root access. The second part of the project requires the Nmap Front End package, which can only be used on Red Hat Linux or Fedora (or other systems using the GNOME desktop).

> Do not complete this project on a production network; work only in an isolated lab environment.

+   1. Log in to Linux, open a command-line window, and change to root access. Use this scan to determine which hosts are "listening" on your local network:

```
nmap -sP target.edu/24
```

This scan may take several minutes to complete, depending on the size of your LAN. You see a report listing each system that appears to be running on the network. This gives you the information you need to start reviewing the services offered by each host.

+   2. Use the following command to determine the OS used by one of the hosts in your network and see a list of ports discovered to be open using a basic port scan. This scan takes a couple of minutes to complete:

```
nmap -O target.edu
```

+   3. You would want to try a stealthier scan if you were concerned that the default scan might alert the server to your actions and block your subsequent access. In that case you might try a scan such as this one. The resulting list should look the same: you see which ports appear to be open, so that you could attack them based on the service they are providing to the network:

```
nmap -sN target.edu
```
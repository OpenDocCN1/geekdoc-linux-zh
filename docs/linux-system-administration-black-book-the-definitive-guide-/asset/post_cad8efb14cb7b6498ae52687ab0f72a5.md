
## Shutting Off Unnecessary Non-Daemon Network Services

To stop network services that do not require daemons, do the following:

1. Log in as root.
2. Type `vi /etc/inetd.conf` to open the superdaemon’s configuration file.
3. Use the arrow and Page Up and Page Down keys to move through the file. Any line that starts with a hash mark is commented out, and thus not in use. Carefully consider each uncommented line and decide whether you are using that service.

> **TIP:** *Utilize the man system if you cannot tell whether you want a particular item. Type `man process` to learn what it does.*

4. If you decide you do not need the service (common examples are **finger** and **talk**), place the cursor on the beginning of its line.
5. Type `i` to enter Insert mode.
6. Type a hash mark (#) to comment out the line.
7. Press the Esc key to return to Command mode.
8. After you finish editing this file, type `ZZ` to save and close it.
9. Type `/etc/rc.d/init.d/inet restart` to stop the superdaemon and start it with its new configuration.

> **NOTE:** *This process works the same regardless of which distribution you are using. The primary difference here might be what is on or off by default, or what is included in the listing. Also, the way you restart inetd may be different in another distribution. A basic method that works on any distribution is to type `ps aux | grep inetd` to get the Process ID (PID) that inetd is running under, and then type `kill -HUP PID` to restart the service.*

## Restricting Network Access With tcp_wrappers

To restrict network access on a specific machine without using a full-blown firewall, do the following:

1. Log in as root.
2. Type `vi /etc/hosts.deny` to open the file that allows you to block who has access to the network.
3. This file already has some descriptive content. Type `G` to move the cursor to the last line.
4. Type `o` to create a new line beneath the current position, and then enter Insert mode.
5. Add the following line to tell the machine to make sure that incoming traffic’s claimed address matches its real address:

   ```
   ALL: PARANOID
   ```

6. What you add from here depends on what you want to block. At the bare minimum, you need to add the following if you want to allow the sendmail server to move mail through this system:

   ```
   ALL EXCEPT sendmail: ALL
   ```

7. Remember that **tcp_wrappers** looks in /etc/hosts.allow to see what is explicitly allowed as well. Anything that does not match in /etc/hosts.allow but is not email will be blocked by this setup. If you need to open anything else explicitly, add additional **EXCEPT** portions to this statement. Remember that you need to use the actual daemon’s name in the daemon portion. Many of these names are listed if you type `ls /usr/sbin/in*`. For example, you might use the following if you have a Web server on a specific machine:

   ```
   ALL EXCEPT sendmail EXCEPT httpd: ALL
   ```

> **NOTE:** *Don't knock too many holes in this file! This is security, remember; deny, and then explicitly allow.*

8. When you are finished, press the Esc key, and then type `ZZ` to save and close the file.
9. Type `vi /etc/hosts.allow` to open the file that lets you state what kinds of connections should definitely be let through.
10. It is more important for this file to understand how to refer to individual machines or groups of machines than it is for the deny file to understand. Whenever you punch holes, try to make them as small as possible so that you do not accidentally allow intruders' packets as well. Instead of the standard asterisk used in so many files as wildcards, you can use the following characters together as a wildcard: back quote, period, backslash, and front quote. The following are the formats available:

    - `*.domain.extension`, as in `*.animals.org`
    - `*ip1.ip2.*`, as in `192.168.170.*`
    - `*ip1.ip2.ip3.ip4/nm1.nm2.nm3.nm4*`, as in `192.168.170.9/255.255.255.90`

Add rules that let the traffic into the machine that it needs. For example, if you need to be able to **telnet** from your machine in another part of the office to this one, add a line such as this:

```
in.telnetd:192.168.170.12
```

11. When you are finished, press the Esc key, and then type `ZZ` to save and close the file.

> **NOTE:** Do not open too many holes right away. Sometimes, instead of poking your security full of holes, it is better to see what you explicitly need to add.

## Obtaining And Installing ssh

To get and then install the secure shell software—which must be done on both client and server machines—do the following:

1. Go to the URL **www.ssh.org/download.html**.
2. Read this Web page. Two different versions of ssh are available, ssh and ssh2. These instructions are for ssh, because it has the less-restrictive version license.
3. Click the appropriate mirror site's URL to enter that site's FTP folder.
4. Click the newest version of ssh available. At the time of this writing, the version to download was ssh-1.2.27.tar.gz. Do not be fooled by newer-looking versions that start with ssh-2. These files are ssh2.

> **TIP:** You can also use FTP to go directly to one of the mirror sites after you get the URL address from the main ssh Web page.

5. Close the Web browser or FTP connection.
6. Move the file to your preferred source location (for example, `mv ssh-1.2.27.tar.gz /usr/src`).
7. **gunzip** the file (for example, `gunzip ssh-1.2.27.tar.gz`).
8. Unpack the file with **tar** (for example, `tar -xvf ssh-1.2.27.tar`).
9. Change into the source directory with the **cd** command (for example, `cd ssh-1.2.27`).

> **TIP:** If the newest series 1 version is higher than 1.2.27, see the INSTALL file to make sure that the installation instructions have not changed.

10. Type `./configure` to run the ssh configuration script. You must type the command with ./ in front of it unless you type the entire path, such as `usr/src/ssh-1.2.27/configure`. You would have to have this directory in your path statement to be able to directly type `configure`.
11. Type `make` to start the ssh compilation process. Depending on your machine’s speed and RAM, this compile may take a minute or several minutes.
12. Type `make install` to run the installation portion of the ssh Makefile. This process places the ssh binaries where they need to be on your system. For more on **make** and Makefiles, see Chapter 22. The installation may take several minutes or longer, because code keys need to be generated.
13. Type `make clean` to tidy up your file system by removing the intermediate files created during the compile process.

| Related solutions: | Found on page: |
|---|---|
| Opening **gzipped** Files | 108 |
| Opening **tar** Files | 110 |
| Compiling C Code With **gcc** | 647 |

## Setting Up ssh On A Server

To set up the secure shell on the machine you want to provide ssh secured access to, do the following:

1. Log in as root.
2. Type `vi /etc/sshd_config` to open the ssh server configuration file.
3. Many options are available for /etc/sshd_config. Table 9.10 breaks them down into categories to make them more manageable. Be sure to consider each option carefully, starting with the definitions that state who you allow to access this machine through ssh. Choose the options that apply to your needs.

> **TIP:** When typing all of these keywords, you do not need to be careful about the case. This is a rare instance in Linux where case does not matter.

4. Now, choose the options that apply to the level of authentication you want to require. Table 9.11 lists what these options are and how to use them.

| Option | Purpose | Values |
| :--- | :--- | :--- |
| **AllowGroups** | Specifies exactly which groups are allowed to log in. This item refers to primary groups only. It does not look at secondary groups. | **group1 group2 group3...** |
| **AllowHosts** | Specifies exactly which hosts users can log in from. | **host1 host2...** |
| **AllowSSHHosts** | Double-checks any remote login attempts against the following host pattern. | **host1 host2...** |
| **AllowUsers** | Double-checks any remote login attempts against the following two types of user patterns, which can be mixed or used singly. | **user user@host...** |
| **DenyGroups** | Refuses to allow the specified groups to log in. This item refers to primary groups only. It does not look at secondary groups. | **group1 group2 group3...** |
| **DenyHosts** | Refuses to allow anyone from the specified hosts to log in. | **host1 host2...** |
| **DenySSHHosts** | Refuses to allow anyone from the specified hosts to log in, even if they are listed in the appropriate login files created when setting up the client (`~/.rhosts` or `~/.shosts`). | **host1 host2...** |
| **DenyUsers** | Refuses to allow anyone to log in if they match the following two types of user patterns, which can be mixed or used singly. | **user user@host...** |
| **PermitRootLogin** | Allows root to log in to this machine. It is always a security hole to allow remote access by root. | **yes** (root can log in regardless of method), **no** (root cannot log in regardless of method), or **noPWD** (root can log in but not with just a password authentication), with a default of **yes**. |

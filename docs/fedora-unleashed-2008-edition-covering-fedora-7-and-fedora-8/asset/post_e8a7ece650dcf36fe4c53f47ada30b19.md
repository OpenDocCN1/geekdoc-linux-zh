
## Using sftp to Copy Many Files Between Machines

sftp is a mix between ftp and scp. Connecting to the server uses the same syntax as scp—you can just specify an IP address to connect to using your current username, or you can specify a username using username@ipaddress. You can optionally add a colon and a directory, as with scp. After you are connected, the commands are the same as ftp: cd, put, mput, get, quit, and so on.

In one of the scp examples, we copied a remote file locally. You can do the same thing with sftp through the following conversation:

```bash
[paul@susannah ~]$ sftp 10.0.0.1
Connecting to 10.0.0.1...
paul@10.0.0.1's password:
sftp> get remote.txt
Fetching /home/paul/remote.txt to remote.txt
/home/paul/remote.txt   100%   23   0.0kB/s   00:00
sftp> quit
paul@susannah ~]$
```

Although FTP remains prominent because of the number of systems that do not have support for SSH (Windows, specifically), SFTP is gaining in popularity. Apart from the fact that it secures all communications between client and server, SFTP is popular because the initial connection between the client and server is made over port 22 through the sshd daemon. Someone using SFTP connects to the standard sshd daemon, verifies himself, and then is handed over to the SFTP server. The advantage to this is that it reduces the attack vectors because the SFTP server cannot be contacted directly and so cannot be attacked as long as the sshd daemon is secure.

![](img/34e72348d53ca54c2a1d9c871316691b_368_0.png)

## Using ssh-keygen to Enable Key-Based Logins

There is a weak link in the SSH system, and, inevitably, it lies with users. No matter what lengths system administrators go to in training users to be careful with their passwords, Post-it notes with “Password” written on them are attached to monitors around the world. Sure, it has a mix of letters and numbers, but it can be cracked in less than a second by any brute-force method. *Brute-forcing* is the method of trying every password possibility, starting with likely words (such as *password* and variants, or *god*) and then just trying random letters (for example, *a, aa, ab, ac*, and so on).

Even very strong passwords are no more than about 16 characters; such passwords take a long time to brute-force but can still be cracked. The solution is to use key-based logins, which generate a unique, 1024-bit private and public key pair for your machine. These keys take even the fastest computers a lifetime to crack, and you can back them up with a password to stop others from using them.

Creating an SSH key is done through the ssh-keygen command, like this:

```bash
ssh-keygen -t dsa
```

Press Enter when it prompts you where to save your key, and enter a passphrase when it asks you to. This passphrase is just a password used to protect the key—you can leave it blank if you want to, but doing so would allow other people to use your account to connect to remote machines if they manage to log in as you.

After the key is generated (it might take up to 30 seconds depending on the speed of your machine), change the directory to `~/.ssh` (`cd ~/.ssh`), which is a hidden directory where your key is stored and also where a list of safe SSH hosts is kept. There you will see the files `id_dsa` and `id_dsa.pub`. The first is your private key and should never be given out. The second is your public key, which is safe for distribution. You need to copy the public key to each server you want to connect to via key-based SSH.

Using `scp`, you can copy the public key over to your server, like this:

```bash
scp id_dsa.pub 10.0.0.1:
```

This places `id_dsa.pub` in your home directory on 10.0.0.1. The next step is to SSH into 10.0.0.1 normally and set up that key as an authorized key. So you can SSH in as yourself and then type the following:

```bash
touch .ssh/authorized_keys
cat id_dsa.pub >> .ssh/authorized_keys
chmod 400 .ssh/authorized_keys
```

The `touch` command creates the `authorized_keys` file (if it does not exist already); then you use `cat` to append the contents of `id_dsa.pub` to the list of already authorized keys. Finally, `chmod` is used to make `authorized_keys` read only.

With that done, you can type `exit` to disconnect from the remote machine and return to your local machine. Then you can try running `ssh` again. If you are prompted for your passphrase, you have successfully configured key-based authentication.

Now the current machine is secured, but what about every other machine? It is still possible to log in from another machine using only a password, which means your remote machine is still vulnerable.

The solution to this is to switch to root and edit the `/etc/ssh/sshd_config` file. Look for the `PasswordAuthentication` line and make sure it reads `no` (and that it is not commented out with a `#`). Save the file, and run `kill -HUP $(cat /var/run/sshd.pid)` to have `sshd` reread its configuration files. With that done, `sshd` accepts connections only from clients with authorized keys, which stops crackers from brute-forcing their way in.

### TIP

For extra security, consider setting `PermitRootLogin` to `no` in `/etc/ssh/ssh_config`. When this is set, it becomes impossible to SSH into your machine using the root account—you must connect with a normal user account and then use `su` or `sudo` to switch to root. This is advantageous because most brute-force attempts take place on the root account because it is the only account that is guaranteed to exist on a server. Also, even if a cracker knows your user account, she has to guess both your user password and your root password to take control of your system.

## Remote X

Everything we have looked at so far has been about command-line remoting, with no mention of how to bring up a graphical user interface. There are two ways of doing this in Linux: the X Display Manager Control Protocol (XDMCP) and Virtual Network Computing (VNC). The former is specific to the X Window System and is very tightly integrated with the rest of the graphical system but is also very insecure. VNC is more modern and very widespread but insecure in some implementations. Both are being used with Fedora, so we cover both here.

### XDMCP

Unless you have Fedora configured to log in a specific user automatically, you will be familiar with the user login screen that appears at bootup. What you are seeing is the GNOME Display Manager (GDM), which runs your X sessions, checks passwords, and so forth. What you are doing is logging in to the local machine because that is the default configuration.

However, GDM is also equipped to allow other network users to connect to your machine through the XDMCP protocol. There are various reasons for using XDMCP; the most popular is that many modern machines are large and noisy. They have big hard drives, CPUs with huge fans, powerful graphics cards, and so do not fit into a peaceful living room. On the flip side, a thin client (a machine with very little CPU power and no hard disk of its own) is silent but not powerful enough to run GNOME or OpenOffice.org.

The solution is to have your powerful machine locked away in a cupboard somewhere with a Wi-Fi connection attached and your quiet thin client sitting in the lounge also on the Wi-Fi link. The thin client connects to the powerful machine and runs all its programs from there, with all the graphics being relayed over the network.

With Fedora, this is easy to do. On the server side (the powerful machine), you need to check one box, and on the client side (the less-powerful machine), you need to check another box. We will start with the server side. Select System Settings, Login Screen; then select the XDMCP tab and enable XDMCP. On the client side, select System Settings, Login Screen; then select the Security tab and click the Allow Running XDMCP Chooser from the Login Screen. You should also make sure the Show Actions Menu box is checked.

Now, from the client side, log out from your desktop so that you return to the Fedora login screen. When it prompts you for your username, press F10. A menu appears with an option labeled XDMCP Chooser. Select that and a new dialog box appears with a list of local XDMCP servers that are willing to accept your connection—you should see your server in there. Select it and click Connect; you will see a login screen from that server, inviting you to log in. You need, of course, a valid account on the server to be able to log in; however, that is the only thing you need.

As you can see, because XDMCP is so core to the X Window System, it is easy to set up. However, as you will find as you use it, XDMCP is very slow—even on a Gigabit Ethernet network, it chews up a substantial percentage of bandwidth. It is also insecure. Anyone can monitor what you are doing with very little work. Because of these two flaws, XDMCP should never be used outside a trusted network.

### VNC

The next step up from XDMCP is VNC, which was developed at AT&T’s Cambridge Research Laboratory in England. VNC is widespread in the Linux world and, to a lesser extent, in the Windows world. Its main advantage is its wide-scale nature: Nearly all Linux distributions bundle VNC, and clients are available for a wide selection of platforms.

By default, Fedora installs the VNC server component but not the client component. Go to the Add or Remove Packages dialog box and select System Tools. Then select *vnc* to install the client, go to Network Servers, and select *vnc-server* to install the server.

With that done, all that remains is to tell Fedora who should be allowed to connect to your session. This is done from the Remote Desktop option on the Preferences menu. By default, your desktop is not shared, so check Allow Other Users to View Your Desktop to share it. You should also check Allow Other Users to Control Your Desktop; otherwise, people can see what you are doing but not interact with the desktop—which is not very helpful.

The second set of options on that screen is important. If you are using this as a remote way to connect to your own desktop, deselect Ask for Confirmation. If this is not done, when you try to connect from your remote location, Fedora pops a message box up on the local machine asking *Should this person be allowed to connect?*. Because you are not there to click Yes, the connection fails. If you want to let someone else remotely

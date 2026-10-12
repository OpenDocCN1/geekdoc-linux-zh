
To determine which system profile is currently being used by Linuxconf, select **Control Panel - Switch system profile** from the left side of the Linuxconf screen. You will see the list of available configurations in the "Pick a version" tab, as shown in Figure 4-11.

![](img/f9ec99365f159bfe663f8ac29732663c_104_0.png)

Figure 4-11 Determining the current system profile

You can also create your own system profiles, as follows:

1. Select **Control Files and Systems - Configure system profiles** from the Linuxconf screen. You will see a window similar to the one shown in Figure 4-10.
2. Click the **Add** button to add a new system profile. You will be asked to enter a name for the new system profile, as shown in Figure 4-12. The name must be a single word and cannot contain any space characters. Enter a name of your choice and click **Accept**.

![](img/f9ec99365f159bfe663f8ac29732663c_104_1.png)

Figure 4-12 Adding a name for the new system profile

3. You are now asked to enter a title for your new profile. This can be anything you want; it is used only to help you distinguish the profile from the others. Enter something meaningful in terms of your needs.
4. You need to provide the archiving family names (that is, `/etc/linuxconf/archive/subsystem-family-name`) for various subsystems, such as `crond`, `PPP/SLIP/PLIP`, `DNS server`, `firewalling rules`, `wu-ftpd server`, `gated`, `inet`, `httpd`, `lpd`, and so on. You can also provide a default archiving family name, to be used when you don’t explicitly define an archiving family name for a certain subsystem. If you neither set a default family name nor provide an explicit family name, the subsystem’s data is stored in the `/etc/conf.linuxconf` file. If you want to use an existing subsystem from another profile, enter the existing family name for that profile. Note that if a subsystem is shared between multiple archives, any changes to the subsystem’s configuration files will be effective in all system profiles using that subsystem.
5. After you specify all the archiving family names, click the **Accept** button. Your new profile will be added to the list of available profiles. Click **Accept** again.
6. To use your newly created profile, select **Control Panel - Switch system profile** from the Linuxconf screen. Click your profile to switch to it. After you switch to your new profile, it is automatically archived when you switch back to another profile. If you want to archive it manually, select **Control Panel - Archive configurations** from the Linuxconf screen.

As you can see, Linuxconf provides a very powerful means for you to experiment with various configurations without the fear of losing your existing configuration.

## Part II
### Advanced Configuration

- 5 User Administration
- 6 Process Administration
- 7 Network Administration
- 8 DNS Service
- 9 E-mail Service
- 10 FTP Service
- 11 Sharing Files and Printers with Samba
- 12 Web Service Using Apache
- 13 Using NFS File Servers
- 14 Configuring X Window

## Chapter 5
### User Administration
#### Creating Multiple Superuser Accounts

Many novice system administrators think that the user `root` is the only superuser. This is not true at all. The username "root" is not what makes an account into a superuser. Take a look at the following lines from an example `/etc/passwd` file:

```text
root:dcw12YbBSUFyo:0:0:root:/root:/bin/tcsh
bin::1:1:bin:/bin:
daemon::*:2:2:daemon:/sbin:
kabir:.HoiiviYBP4/8U.û:0:Mohammed
sheila:g7wD/qLMFW9M.:501:501:/home/sheila:/bin/tcsh
apache:!1:502:502::/usr/local/apache:/bin/false
```

This password file has two superuser accounts: `root` and `kabir`. To understand why, you have to remember that the `/etc/passwd` file has the following format:

```text
username:password:UID:GID:full-name:home-dir:shell
```

Notice the UID (user ID) and GID (group ID) fields of the `root` account. They are both set to 0. And, if you look back at the line for the ordinary-looking user `kabir`, you see that his UID and GID are also set to 0. This is what turns a user into a superuser. In other words, any user with a UID and GID of 0 is equivalent to what is called `root`.

As you can see, you can turn any ordinary user account into a superuser account. In most situations, you do not want to do that, because having multiple superuser accounts could mean additional security risks. But, multiple superuser accounts sometimes are used in organizations that have multiple system administrators working on the same systems. This is done to ensure a little more accountability in a multi-administrator environment. For example, if the `kabir` and `root` accounts in the password file just described are for two different system administrators, then it will be a bit easier to tell who did what as the superuser by looking at various log files than if the two system administrators were to *SHARE* the default *root* account.

Multiple superuser accounts can be used in one other, not-so-desirable situation—when a system has been hacked by someone. In such a case, the hacker creates an ordinary-looking superuser account by setting the UID and GID values to 0. This allows the hacker to log back in and become a superuser without knowing the root user's password. This trick works on systems where the system administrator is a novice or just too busy to keep an eye open for such things.

Realistically, no system administrator has the time (in the context of a real for-profit organization) to monitor for hackers on a daily basis, so you might want to employ some scripts as your helpers in such a case. For example:

```bash
/bin/grep '0:0' /etc/passwd | awk 'F$5=="0" {print $1}' | mail -s "$(date +%d %m)" root
```

This small script uses a few standard commands to check the `/etc/passwd` file for users with UID and GID values set to 0. It can mail the root user a list of such accounts. If you place this script in `/etc/cron.daily` to run it once a day, you will get an e-mail message from it every day that will show you the list of superusers. You can then quickly check the e-mail every day to know which accounts have superuser privileges. Of course, a smart hacker can find out about this and will be able to change the script to feed you fake information. But, in my experience, most hacking is done by thrill seekers who hardly spend the time to investigate things for themselves. These so-called hackers just find an exploitable program on the Internet, compile it, and run it to get access; they often lack the skills to go through the checks that a careful system administrator might have put in place.

Now that you know how any user account can be turned into a superuser account, you might think that any such user can log in to a Red Hat Linux system quite easily. Not so. The Red Hat Linux system, by default, uses the Pluggable Authentication Module (PAM) for login authentication, which requires that superuser access be allowed only from terminals that are considered secure. By default, the PAM configuration file for login, `/etc/pam.d/login`, contains a line such as the following:

```text
auth required /lib/security/pam_securetty.so
```

This line states that the security restrictions enforced by the `pam_securetty.so` module need to be satisfied before a login can be permitted. This particular module considers a superuser login attempt satisfactory only if the login is being attempted from a TTY listed in the `/etc/securetty` file. So, if you decide to turn an ordinary user into a superuser and attempt to log in via Telnet (which will have a pseudo-TTY device), you will not be able to log in. But, you can easily change this by adding the pseudo-TTY devices (typically, `tty1` to `tty12`) in the `/etc/securetty` file. This is not recommended, however, because it creates a security risk. Instead, if you must use multiple superuser accounts for administrative and accountability reasons, do the following:

1. Create multiple superuser accounts.
2. Create one ordinary user account per superuser.
3. Instruct each superuser to log in to the system as an ordinary user and change to the superuser account by using the `su` command.

The `su` command can be used to substitute UIDs and GIDs. For example, you can log in as an ordinary user and change to the `root` account by running `su` without any argument. You will be prompted for the `root` password; if you know the `root` password, `su` will start a new shell, and you will be logged in as the `root` user.

Remember that superusers (UID = 0, GID = 0) have full access to everything, and thus these are very sensitive accounts.

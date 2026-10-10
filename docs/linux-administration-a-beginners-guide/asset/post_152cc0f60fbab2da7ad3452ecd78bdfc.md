
# Allowing Remote Users

If you want to allow printers on your network to use your system as a print server, you need to tell `lpd` which systems are allowed to do so. This is done by listing them in the `/etc/hosts.lpd` file or the `/etc/hosts.etcquiv` file.

> **NOTE**: By removing the files `/etc/hosts.lpd` and `/etc/hosts.etcquiv` altogether, you can allow any computer to connect to your `lpd` server. This is, of course, a dangerous arrangement, especially if the system has a direct connection to the Internet.

# Configuring /etc/printcap

The best way to update the `/etc/printcap` file is through a management tool such as Red Hat Linux's `printtool` utility. Such management tools take care of maintaining the print formatting information. Of course, if you want to be able to customize your printing solutions (one of the many things that make Linux fun to work with), you'll want to be able to edit the `/etc/printcap` file yourself.

The entry for each printer listed in the `/etc/printcap` file should be formatted as follows:

```
printername1|printername2|printername3....\
    :command=value1\
    :command2:\
    :command=value
```

where `printername1` is the name of the printer, and `printername2` and `printername3` are aliases to `printername1`. Each **command** may be followed by a value (see Table 21-1 in the next section). For example, in the following `/etc/printcap` file, the printer's name is `myprinter`, and its alias is `lp`:

```
myprinter|lp:\
    :sd=/var/spool/lpd/lp:\
    :sh:\
    :rm=intrepid:\
    :rp=engrtspd
```

# Commands in /etc/printcap

Table 21-1 lists the valid commands available for use as commands in the printcap file, and their corresponding values.

Most of the time, the defaults for the `/etc/printcap` commands are fine. Values that typically get changed are **if** (for accounting purposes), **mc**, **of**, **rm**, and **rp**.

### Table 21-1. Commands in /etc/printcap File

| Name | Default Value | Description |
| :--- | :--- | :--- |
| af | N/A | Specifies the name of the file in which accounting information is kept. Necessary only if you want to track detailed printer usage. |
| br | 0 | Printer’s baud rate (applies only to serial printers). |
| ff | \f | Character used to generate form feeds. |
| fo | N/A | Generates a form feed before every print job. By default, this is not specified (which implies false). If you need to have the form feed (sometimes necessary for older tractor feed printers), include this in the file (which implies true). |
| lf | None | Name of text filter that performs input filtering. |
| lf | /dev/console | Filename to which error logs are sent. |
| lo | lock | Name of lock file. The default filename is "lock." |
| lp | /dev/lp | Device name to open for output (applies only if printer is local). |
| mx | 1000 | Maximum size of a file that can be printed in kilobytes. Setting this value to zero means there is no limit. |
| of | None | Name of outbound filter (filter applied to file on the way out of the queue and to the printer). |
| pl | 66 | Page length (in text lines). |
| pw | 132 | Page width (in characters). |
| px | 0 | Page width (in pixels). |
| py | 0 | Page length (in pixels). |
| rm | None | Machine name for remote printing. |
| rp | lp | Queue name for remote printer. |
| sd | /var/spool/lpd | Name of spool directory. |
| st | status | Name of status file. The default filename is "status." |
| sh | N/A | Suppresses printing of burst page header. |

# Example

Here is the /etc/printcap entry for a machine that is printing to a network printer called `zaphod`:

```
lp|zaphod:\
\ :sd=/var/spool/lpd/lp:\
\ :md#0:\
\ :sh:\
\ :rm=zaphod:\
\ :rp=
```

In this case, the name of the print queue isn't specified because the remote host listed is the printer itself and thus has only one queue. This is common with a lot of network-aware printers that support the `lpd` protocol. (Almost all the HP series of printers with built-in Ethernet support the `lpd` protocol.)

> **Note** that the “sh” entry implies that “suppress burst page header” is true.

# Using Samba to Print

By taking advantage of the fact that `lpd` allows use of arbitrary programs as filters, it's possible to use Samba's `smbclient` program to allow your Linux machine to use a printer shared from a Windows machine.

When `lpd` invokes a filter, it passes the following arguments to the filter:

```
-w width -l length -i indent -n login -h host accounting-file
```

The width and length parameters are taken from the `pw` and `pl` settings; login is the user's login, and host is the name of the machine where the user originated the request. The account-log-file parameter is from the **af** setting.

Obviously these parameters can't be passed to the `smbclient` program directly, so we use a wrapper to turn the parameters into something that `smbclient` can use. Red Hat Linux comes with a wrapper called `smbprint`, which we will use as a basis for our script. The script can be named anything (we'll call ours `smb2linc`) and be located anywhere; however, either `/usr/bin` or `/usr/local/bin` is suggested for the location, and we will assume `/usr/local/bin` for this example. Here is the script itself:

```
#!/bin/sh

# This next line assumes that the smbclient program is installed
# in the /usr/local/samba/bin directory. If it is not, be sure to
# change it.
SMBC=/usr/local/samba/bin/smbclient

eval acct_file=${$}
spool_dir=dirname ${acct_file}
config_file=${spool_dir}/.config
eval `cat ${config_file}`
(
echo 'print -'
cat
) | $SMBC '\\\\${server}\${service} $password -U $server -N -P
```

This **smbprint** script assumes the following:

- The accounting file option (the *af* entry) is enabled in the */etc/printcap* file for this printer.
- The */var/spool/lpd/PRINTER-NAME/.config* file exists, where *PRINTER-NAME* is the name of the printer. This configuration file should contain the following lines.

```
server=PC_SERVER
service=PR_SHARENAME
password='password'
```

where *PC_SERVER* is the name of the Windows machine where the printer resides, *PR_SHARENAME* is the name of the printer on the Windows machine; and *password* is your password for that system.

> **WARNING**: This particular arrangement is somewhat dangerous because it requires that you leave your password in a plain text format written to disk. Furthermore, it assumes only one person will be using the system; you. A better arrangement is to share the printer with *users* in such a manner that passwords aren't necessary for printing.

Once this **smbprint** script is set up, we need to create the *users* in *printcap* that entry for the script, as follows:

```
printername:\
:sd=/var/spool/lpd/printername:\
:if=/var/spool/lpd/printername/:acc:\
:if=/usr/local/bin/smbprint:\
:mx=0:\
:lp=/dev/null;
```

where *printername* is the name of the printer where you want the print jobs to go. Remember that we assume you named the script **smbprint** and placed it in the */usr/local/bin*. If you placed it elsewhere or named it something else, be sure to reflect that in the input filter (the *if*=) line.

# Implementing Your Changes

Once you update the */etc/printcap* file, you need to restart `lpd` in order for your changes to take effect. To do that, find the process ID (PID) of the line printer daemon, with this command:

```
[root@ford /root]# ps -C lpd
```

Then issue a *kill* statement to kill the process, like so:

```
[root@ford /root]# kill XXXX
```

where *XXXX* is the PID of `lpd`. (The PID number, of course, won't necessarily be four digits long.) Then restart `lpd`:

```
[root@ford /root]# /usr/sbin/lpd
```

> **TIP**: If you have Red Hat Linux, you can simply run the following instead of killing the process and restarting it by hand:

```
[root@ford /root]# /etc/rc.d/init.d/lpd restart
```

# Clients of LPD

There are several peripheral tools that work along with `lpd` as clients. They are discussed in the following sections.

## lpr

Under Linux, *lpr* is the command-line tool for performing printing operations. Most applications that offer printing services mask `lpr` behind a dialog box under X Windows. Using `lpr` is pretty straightforward; simply type

```
[root@ford /root]# lpr filename
```

where *filename* is the name of the file you want to print. This command sends the file to the default printer (the first printer listed in the */etc/printcap* file). If you want to send the job to another printer, use the *-P* option like so:

```
[root@ford /root]# lpr -P printername filename
```

where *printername* is the name of the printer and *filename* is the name of the file you want to print. Table 21-2 shows all the options available for use with `lpr`.

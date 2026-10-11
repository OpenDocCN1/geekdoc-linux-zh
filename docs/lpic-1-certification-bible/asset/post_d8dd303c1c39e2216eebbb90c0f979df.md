
| Definition | Function | Arguments | Example |
| --- | --- | --- | --- |
| mx | Defines the maximum size of the print job. | The size in blocks, `:mx#0:\` with 0 meaning unlimited. | |

Consider the previous example file.

```
lp|hp1j:\
```

Since this line does not begin with a colon or a pipe, it is the beginning of another printer definition. The printer’s name is `lp`, which is short for line printer and has an alias of `hp1j`. It is important to have a printer named `lp`, and it should be the one you use most often since this is the default printer that most applications use, unless told otherwise.

```
:sd=/var/spool/lpd/lp:\
```

This line configures the spool directory, which is where documents are stored before they are sent to the printer hardware.

```
:mx#0:\
```

This line removes any print job size limit. Users are free to submit jobs of any length.

```
:sh:\
```

Some people like to use banner pages to separate print jobs at a busy printer. In this case banner pages have been disabled to save paper.

```
:rm=192.168.1.12:\
```

This printer is shared out from a print server on the network. This definition configures the remote address of that print server. Hostnames or IP addresses can be used, but if you use hostnames, remember that a DNS failure can stop users from printing. The advantage is that if the print server should ever move, only the DNS entry needs to be changed, and not every workstation.

```
:rp=hpjlj:\
```

This line specifies the name of the printer on the remote print server.

```
::/usr/share/printtool/master-filter:
```

This definition specifies the print filter to use for this printer. A print filter is similar to a printer driver in other operating systems, such as Windows. It formats the data to accommodate the language that the printer can use. When most people think of printing on a UNIX system, they think of a PostScript printer. But as Linux has moved into the consumer market where most people do not have expensive PostScript printers, print filters have become very important. Several different print filters are available, and the most common are covered later in this chapter.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_480_0.png)

All lines in the `/etc/printcap` file end in `:\`, except for the last line in a printer block.

## Creating the spool directory and log file

Once you edit the `/etc/printcap` file and add the necessary printer definitions, you then need to create the spool directory and log file.

### Print spool directory

The print spool directory is where print jobs are sent before they are streamed to the printing device. When you manually create a printer configuration you must make this directory by hand. You should make sure to give this directory the exact path and name you defined in `/etc/printcap`. For example:

```
debian:~# mkdir /var/spool/lpd/lp
```

Next, you need to set the proper ownership and permissions on the newly created directory. Most distributions have a special user or group that owns the LPR directories and files. Usually these are called `lp`. For example:

```
debian:/var/spool/lpd# ls -l

    total 5
    drwx------ 2 daemon lp 232 Jan 12 12:40 lp
    -rw-r--r-- 1 root lp 6 Dec 18 10:55 lp.lock
```

Check your distribution to make sure your new directory has the correct ownership and permissions. In this example you can see that Debian has user ownership of the `daemon` because its LPR daemon (`lprd`) runs as the user `daemon`. If your distribution has `lpd` running as `root`, give `root` ownership. Directory permissions should be set to 700 or 770.

**Exam Tip** The spool directory must be created manually.

### Log file

The optional log file defined with the `lf` option in the `/etc/printcap` must also be created manually. This can be done with the `touch` command to create an empty file. For example:

```text
debian:~# touch /var/spool/lpd/lp1/errorlog
```

Set the ownership the same as the spool directory, and change the file permissions to 666, or `rw-rw-rw`.

**Exam Tip** If you use the optional log file, you must create the file manually.

## Controlling printer access

Access to printers can be restricted to certain hosts and users if needed by using the `/etc/hosts.lpd` file. To limit access to the local printer to only the three defined workstations, you would use the following:

```text
dekoenigsberg.bowling.com
mcmillan.bowling.com
golaski.bowling.com
```

The `/etc/hosts.lpd` file can also be used to restrict access to only certain users by putting the user name after the host. For example:

```text
dekoenigsberg.bowling.com greg
mcmillan.bowling.com brett
golaski.bowling.com lorie
```

Keep in mind that if even one host or user is listed in the `hosts.lpd` file, then only the listed host(s) can access the printer. You must add all hosts or users to the file. If no hosts or users are listed then everyone is given access.

**Exam Tip** If you put any entries in the `hosts.lpd` file, only those entries will be given access and all others will be denied.

## Using Print Filters

- Install and configure local and remote printers. Install a printer daemon, install and configure a print filter (e.g., *apsfilter*, *magicfilter*). Make local and remote printers accessible for a Linux system, including postscript, non-postscript, and Samba printers. Involves the daemon*lpd. Involves editing or reviewing the files and directories: `/etc/printcap`, `/etc/apsfilterrc`, `/usr/lib/apsfilter/filter/*`, `/etc/magicfilter/*`, `/var/spool/lpd/*`.

Print filters convert the data to be printed to the format that the print device can understand. If you only print text documents, you do not need a print filter, but if you print graphics, charts, or specially formatted text from most word processors, you do.

As an administrator, you have the option of either creating your own print filter or downloading one from the Internet that has already been created. Unless you are very familiar with writing shell scripts and working with all different types of files, it is best to just use a filtering package from someone else. The three most popular print filter packages are as follows:

- Apsfilter
- Magicfilter
- Red Hat’s PrintTool

The choice of which to use depends on your preference and the printers that each package supports. The print filter should be installed on the print server. Network attached printers do not run print filters, so the job should be run through the local filter before being sent to the print device.

Some versions of LPR, especially the one that ships with Debian, do not send the print job through a filter before sending it to a remote print host. To fix this problem upgrade to LPReq.

### Installing Apsfilter

The Apsfilter package is available from `http://www.apsfilter.org`. It provides a very easy to use menu-based interface to set up and configure many different printers. The Apsfilter package is not used to manage printers, so it is not used to change or remove already installed printers. To install and configure the filter follow these steps.

1. Download the Apsfilter package from the `http://www.apsfilter.org` site. Usually getting the latest version is the best idea since it should have fewer bugs and supports more printers.
2. Uncompress and untar the package. For example:
   ```
   [root@redhat /root]# tar zxfv apsfilter-6.0.0.tar.gz
   ```
3. Execute the `./SETUP` install script. Pay close attention to the first several screens as they provide information on exactly what will happen.
4. The install script will check several things on the system and will prompt you for confirmation. Make sure all of the detected settings are correct.
5. Choose your printer driver. This is done by selecting 1 from the menu. The next menu asks you where the driver would be located. If you do not know, just guess and look through the different options. Once you have found your printer, or one compatible with it, enter the number given.
6. The next option is to configure the printer interface. This is done by selecting 2 from the main menu. As you can see, Apsfilter supports many different connections including parallel, serial, USB, `lpd`, AppleTalk, and Samba (Windows).

The next questions asked depend on the interface you have selected. If you choose `lpd`, you will enter the remote system's address and printer name. A serial or parallel connection requires the local device name, and a Samba share requires Windows information. All of the options are well documented with examples.

7. The next step is to test the printer by printing a test page. This is done by selecting T from the menu. Before doing this you may need to set the paper type and whether you want color or black and white. Make sure the test page prints correctly before continuing. Change the driver if needed.
8. Next, you write the `/etc/printcap` file with the information you have configured. This is done by selecting I from the menu. You will be prompted for some information during this step including the printer and print queue names.
9. The next step is to exit Apsfilter by pressing Q. You will be prompted about where to install the man pages and how to compress them. `/usr/local/man` and `gzip` are good answers.
10. The final step includes reading the informational screens telling you about the setup and sending the author the requested postcard if you like the software.

### Installing Magicfilter

Magicfilter is available at `ftp://metalab.unc.edu/pub/Linux/system/printing/`. It provides a set of printer filters that you can compile and install on your system. It does not provide the configuration support that Apsfilter does. You must manually configure the `/etc/printcap` file and then just insert a Magicfilter filter.

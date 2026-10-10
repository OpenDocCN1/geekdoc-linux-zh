| File | Description |
| :--- | :--- |
| /etc/ppp/scripts/ppp-off | # the actual chat script |
| itself | |
| /etc/ppp/options | # the options pppd uses for |
| all connections | |
| /etc/ppp/options.ttyXX | # the options specific to a |
| connection on this port | |

Red Hat Linux users should note that the standard Red Hat 4.x installation places these scripts in /usr/doc/ppp-2.2.0f-2/scripts.

In your /etc directory there should be a PPP directory:

```
drwxr-x 2 root root 1024 Oct 9 11:01 ppp
```

If it does not exist, create it with these ownerships and permissions.
If the directory already existed, it should contain a template options file called options. tpl. This file is included below in case it does not. Print it out as it contains an explanation of nearly all the PPP options. (These are useful to read in conjunction with the pppd man pages.) While you can use this file as the basis of your /etc/ppp/options file, it is probably better to create your own options file and does not include all the comments in the template--it will be much shorter and easier to read/maintain.
If you have multiple serial lines/modems (typically the case for PPP servers), create a general /etc/ppp/options file containing the options that are common for all the serial ports on which you are supporting dial-in/out and set up individual option files for each serial line on which you will be establishing a PPP connection with the individual settings required for each port.
These port specific option files are named options. tty x1, options. tty x2, and so forth (where x is the appropriate letter for your serial ports). However, for a single PPP connection, you can happily use the /etc/ ppp/options file. Alternatively, you can put all the options as arguments in the pppd command itself.
It is easier to maintain a setup that uses /etc/ppp/options.ttySx files. If you use PPP to connect to a number of different sites, you can create option files for each site in /etc/ppp/options.site and then specify the option file as a parameter to the PPP command as you connect (using the file option-file pppd option to pppd on the command line).

# ## The Supplied Options.tpl File

Some distributions of PPP seem to have lost the options. tpl file, so here is the complete file. I suggest that you do *not* edit this file to create
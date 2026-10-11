# ## Disable Extraneous Applications

In addition to running only the necessary daemons, likewise limit your active network applications with this same simple rule: *Nothing extraneous*. For example, you would not have the Web-server daemon (httpd) running on a mail server. This server's function is to provide mail, not to send out HTML. In this case, you would also be enabling a possible denial-of-service attack and possible program exploits.

If you have extra applications available, especially with the increase of buffer overflow exploits, you'll have more ways for someone to root your system. It also means you'll have less to patch, so it's your incentive to not install all these cool applications that someone sends e-mail about because you may not use them and they might need patches.

# ## Disable Known Insecure Applications

For some reason, people are still using the Berkeley r commands. These include `rsh`, `rlogin`, and `rcp`. With enough freeware security software to replace these – including Secure Shell, which is described later in the chapter – there's no reason to keep r commands usable or even on your system. Believe it or not, some firewall products (including Checkpoint Firewall-1) are configurable to enable `rlogin`. Because of the `.rhosts` and `/etc/hosts.equiv` file, the r commands can be easily fooled into believing they are letting in a trusted host.

# ## Check Permissions

You want to be especially careful with permissions (for more about permissions, see the previous chapter). Plenty of tools out there (such as COPS and TAMU Tiger) can run through your system security if your permissions are at all lax. If tightening them isn't sufficient, you can always create a script to find all the files that have the SUID bit enabled. Here is an example of a `find` command that can look for the SUID bit:

```
find / ( -perm -4000 -o -perm -2000 ) -type f -exec ls -l {} ;
```

If you're running a script, you can run it nightly in a `cron` job to look for suspicious files along with suspicious permissions.

You also want to check permissions for root-owned writable devices. If someone can write to a root console or terminal, they can send commands as root without being root. Don't allow root to own any group-writable (or other writable) files. Hackers can use them to exploit root commands.

## Troubleshooting Problems in Zone Files

The most common error in zone data is to forget that names in a zone file are relative to the origin of the zone, not to the root. Writing `www.example.com` in the zone file for `example.com`, and expecting it to be fully qualified, causes names such as `www.example.com.example.com` to show up in the DNS. You should either write `www`, which is qualified to the correct `www.example.com`, or write `www.example.com.` (with the trailing period) to indicate that the name is fully qualified.

The SOA record should contain (as the first field) the domain name of the master server (not a CNAME) and a contact address (with the @ replaced by a ".") to report problems to. Mail sent to this address should be read frequently. The other fields should contain sensible values for your zone, and the serial number should be correctly incremented after each change.

As discussed earlier, A and PTR records should always match; that is, the A record pointed to by a PTR should point back to the address of the PTR record. Remember to quote the two arguments of HINFO records if they contain any whitespace. Avoid the use of CNAME records for MX, NS, and SOA records.

In general, after making changes to zone data, it is a good idea to reload `named` and examine the logs for any errors that cause `named` to complain or reject the zone. Even better, you could use one of the verification tools such as `dnswalk`, discussed briefly next.

## Tools for Troubleshooting

BIND includes the always useful `dig` program, as well as `named-checkconf` (to check `/etc/named.conf` for syntax errors) and `named-checkzone` (to do the same for zone files). We also especially recommend `dnswalk` and `nslint`. `dnswalk` is a Perl script that scans the DNS setup of a given domain for problems. It should be used in conjunction with RFC 1912, which explains most of the problems it detects. `nslint`, like the analogous `lint` utility for C programs, searches for common BIND and zone file configuration errors.

By occasionally using these programs to troubleshoot DNS problems (especially after non-trivial zone changes) you go far toward keeping your DNS configuration healthy and trouble free.

## Using Fedora Core’s BIND Configuration Tool

Fedora provides a dozen or more different graphical configuration tools system administrators can use to configure network (and system) services. One of these tools is `system-config-bind`, a deceptively simple BIND configuration tool that requires an active X session and must be run with root privileges.

You can launch this client by using the command `system-config-bind` from a terminal window or by selecting the domain name service menu item from the Server Settings menu. It is automatically installed if you select the Fedora configuration tools.

**NOTE**
Using `system-config-bind` and then saving any changes will overwrite existing settings! If you prefer to manually edit your `named` configuration files, do not use `system-config-bind`. Always make a backup of the configuration files in any event—you’ll be glad you did.

After you type the root password and press Enter, the client launches. You will then see its main window, as shown in Figure 26.2.

![](img/774d40fd20903495c5cd00e2efad3f33_775_0.png)

**FIGURE 26.2** Fedora’s `system-config-bind` utility can be used to create, modify, and save basic domain nameserver settings.

`system-config-bind` can be used to add a forward master zone, a reverse master zone, MX records or a slave zone. Click the Add Record button to select an entry for configuration, as shown in Figure 26.3.

![](img/774d40fd20903495c5cd00e2efad3f33_775_1.png)

**FIGURE 26.3** Use `system-config-bind` to add a new DNS record to your server or edit the existing settings.

Existing settings can be edited or deleted by first selecting and then clicking the Edit or Delete buttons in the `system-config-bind` dialog. When you have finished entering or editing your custom settings, select the **Apply** menu item from the **File** menu. Configuration files will be saved in `/etc/named.conf` and under the `/var/named` directory.

# Managing DNS Security

Security considerations are of vital importance to DNS administrators because DNS was not originally designed to be a very secure protocol and a number of successful attacks against BIND have been found over the years. The most important defense is to keep abreast of developments in security circles and act on them promptly.

DNS is especially vulnerable to attacks known as poisoning and spoofing. *Poisoning* refers to placing incorrect data into the DNS database, which then spreads to clients and caches across the world, potentially causing hundreds of thousands of people to unwittingly use the bad data. Although DNS poisoning can occur because of carelessness, it has serious implications when performed deliberately. What if someone set up a clone of a common website, redirected users to it by DNS poisoning, and then asked them for their credit card numbers? *Spoofing* is the practice of forging network packets, and making nameservers believe that they are receiving a valid answer to a query is one of the ways malicious poisoning can be performed.

BIND has often been criticized as being very insecure, and although recent versions are greatly improved in this regard, DNS administrators today must take several precautions to ensure that its use is adequately protected from attacks. Of course, it is important to always run the latest recommended version of BIND.

> **TIP**
> One of your strongest defenses against DNS security risks is to keep abreast of developments in security circles and act on them promptly. The BugTraQ mailing list, hosted at `http://www.securityfocus.com/`, and the SANS Institute at `http://www.sans.org/` are good places to start.

## Unix Security Considerations

The most important step in securing any Unix system is to configure the environment BIND runs in to use all the security mechanisms available to it through the operating system to its advantage. In short, this means you should apply general security measures to your computer.

Run `named` with as few privileges as it needs to function. Don't run `named` as root. Even if an attacker manages to exploit a security hole in BIND, the effects of the break-in can be minimized if `named` is running as user `nobody` rather than as root. Of course, `named` needs to be started as root (because it needs to bind to port 53), but it can be instructed to switch to a given user and group with the `-u` and `-g` command-line options.

Starting `named` with a command such as `named -u nobody -g nogroup` is highly recommended. Remember, however, that if you run multiple services as `nobody`, you increase the risks of a compromise. In such a situation, it is best to create separate accounts for each service and use them for nothing else. Fedora Core runs `named` as the user `named`.

You can also use the `chroot` feature of Unix to isolate `named` into its own part of the file system. If correctly configured, such a file system "jail" will restrict attackers—if they manage to break in—to a part of the file system that contains little of value. It is important to remember that a `chroot jail` is not a panacea, and it does not eliminate the need for other defensive measures.

> **CAUTION**
> Programs that use `chroot` but do not take other precautions as well have been shown to be insecure. BIND does take such precautions. See the chroot-BIND HOWTO at http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Chroot-BIND-HOWTO.html.

For a `chroot` environment to work properly, you need to set up a directory that contains everything BIND needs to run. It is recommended that you start with a working configuration of BIND, create a directory, say `/usr/local/bind`, and copy over the files it needs into subdirectories under that one. For instance, you will need to copy the binaries, some system libraries, the configuration files, and so on. Consult the BIND documentation for details about exactly which files you need.

When your `chroot` environment is set up, you can start `named` with the `-t /usr/local/bind` option (combined with the `-u` and `-g` options) to instruct it to `chroot` to the directory you have set up.

You might also want to check your logs and keep track of resource usage. `named` manages a cache of DNS data that can potentially grow very large; it will also happily hog CPU and bandwidth, making your server unusable. This is something that can be exploited by clever attackers, but you can configure BIND to set resource limits. Several such options in the `named.conf` file are available, including `datasize`, which limits the maximum size of the data segment (and thus the cache). One downside of this approach is that `named` might be killed by the kernel if it exceeds these limits, meaning that you have to run it in a loop that restarts it if it dies (or run it from `/etc/inittab`).

## DNS Security Considerations

Several configuration options exist for `named` that can make it more resistant to various potential attacks. The most common ones are briefly described next.

For more detailed discussions of the syntax and use of these options, refer to the BIND 9 documentation.

> **TIP**
> The Security Level Configuration Tool (`system-config-securitylevel`) has been updated to make implementation of the firewall simpler. The new "on/off" choice (rather than "levels" as before) allows you to employ a firewall without requiring any special configuration for your DNS server.

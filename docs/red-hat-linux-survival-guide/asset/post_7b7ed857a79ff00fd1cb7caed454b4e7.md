
```
IN MX preference_value mail_server_hostname.
```

For example:

```
IN MX 0 mail.ad-engine.com.
```

The preference number is useful only if you have more than one mail server. For example:

```
IN MX 10 fast-mail-server.ad-engine.com.
```

```
IN MX 20 slow-mail-server.ad-engine.com.
```

Here, the lower preference number indicates a higher precedence. Now that you have learned the basics of DNS resource records, you are ready to create primary, secondary, and cache-only DNS servers.

## Configuring a DNS Server Using bindconf

Normally it is not advisable to have X Window system on a server because it is not necessary to have such a GUI environment to manage the server and also because X can open your system to more hacker attacks because many X programs are constantly found to be buggy. However, if you must have the X Window system on your DNS server you can also take advantage of the Bind Configuration Tool (bindconf) to configure the DNS server (BIND). If you do not have X installed on your server, which is my recommendation, then you can skip to the next section.

![](img/9eb7e89292d2f85707b4d49102c865b7_475_0.png)

> If you do decide to use bindconf, you must never manually modify the /etc/named.conf file because bindconf will recreate the file every time you use bindconf. That is, if you manually modify this file your changes will be lost the next time you use bindconf!

When you run bindconf from an xterm window, a window similar to Figure 15-1 appears.

By default, bindconf creates a master zone called localhost with the appropriate reverse DNS configuration. This is shown in the main menu window. This configuration is used for the loopback address only.

![](img/9eb7e89292d2f85707b4d49102c865b7_476_0.png)

Figure 15-1 The bindconf main screen.

## Creating a forward master DNS zone for a domain

Say you want to create a forward master zone for a new domain called evoknow.com. Do the following:

- 1. Click the Add button in the main bindconf window and you will see a screen as shown in Figure 15-2. Select Forward Master Zone option and enter the appropriate domain name in the name entry area and click OK to continue.

![](img/9eb7e89292d2f85707b4d49102c865b7_476_1.png)

Figure 15-2 Selecting a zone type.

- 2. You will see a screen as shown in Figure 15-3. You can change the contact address to a more appropriate address than root@localhost.

![](img/9eb7e89292d2f85707b4d49102c865b7_477_0.png)

Figure 15-3 The Name to IP Translation window.

If you wish to set the zone life cycle information, click the Time Settings button, which brings up the screen shown in Figure 15-4. Set the refresh rate, retry rate, expiration rate, minimum time, etc., to any desired settings. In most cases the default values are fine.

![](img/9eb7e89292d2f85707b4d49102c865b7_477_1.png)

Figure 15-4 The Zone Life Cycle Information window.

- 3. Now you must add a name server (NS) record for this domain. Before you can add a NS record, make sure you have defined an A (Address) record for the name server host. Clicking the Add button under Records in the window shown in Figure 15-3 brings up the screen shown in Figure 15-5. Select Host as the resource record type and enter a host name and IP address for this A record.

![](img/9eb7e89292d2f85707b4d49102c865b7_478_0.png)

Figure 15-5 Adding an A (Address) record.

Add as many hosts as you want for this domain in the same manner. In this example I have added ns1.evoknow.com and mail.evoknow.com.

- 4. From the window shown in Figure 15-3, select the domain name (evoknow.com) and click the Edit button to bring up the Settings for domain window, as shown in Figure 15-6. Under the Name Servers section, click the Add button and enter the name of the name server host, which in this example is ns1.evoknow.com. Similarly, if you have set up a host for your mail server you can add it under the Mail Exchangers section, as shown in this example. Mail exchanger priority is an arbitrary number. If you set up multiple mail servers, the lowest numbered mail server will be considered the highest-priority mail server. Click OK to return to the main menu.

![](img/9eb7e89292d2f85707b4d49102c865b7_478_1.png)

Figure 15-6 Adding name servers and mail servers for the new domain.

- 5. After you have added at least one name server to the new domain configuration, you can choose File ⇨ Apply in the main menu screen and a new /etc/named.conf will be created with appropriate master configuration for the chosen domain (evoknow.com in this case). Also, a new zone file will be created in the /var/named directory called evoknow.com.zone, which includes the zone’s master configuration data.

## Creating a reverse master zone configuration for a domain

Say you want to create a reverse master zone for a new domain called evoknow.com. Do the following:

- 1. Make sure you have already created the forward master zone as discussed in the previous section.
- 2. Click the Add button in the main bindconf window and you will see a screen like that shown in Figure 15-7. Select Reverse Master Zone option and enter the first three octets of the IP address of the network in the IP address entry area. Click OK to continue.

![](img/9eb7e89292d2f85707b4d49102c865b7_479_0.png)

Figure 15-7 Adding a reverse zone.

- 3. In the IP to Name translation screen (shown in Figure 15-8), you should add the name server and any other hosts that you would like to provide reverse DNS for.
- 4. After you have added all the hosts, you should click OK and return to the main menu, which should display your forward and reverse

![](img/9eb7e89292d2f85707b4d49102c865b7_480_0.png)

Figure 15-8 Adding name server(s) and other host(s) in reverse DNS configuration.

zone configuration names. Choose File ⇔ Apply to apply your configuration, create the necessary reverse zone file, update /etc/named.conf.

## Manually Configuring a DNS Server

If you are not using the X Window System-based bindconf tool, you must manually configure the DNS server by editing and creating the configuration files using a text editor such as vi.

## Configuring the master (primary) DNS server

These instructions in this section assume that I have a DNS server (named) running on the ns.evoknow.com host and that I just registered a domain called classifiedworks.com with Internic. Now I want to set up DNS on ns.evoknow.com to provide primary name service for the new domain. Here's how.

- 1. First, I need to create the following zone statement in the /etc/named.conf file:

```
zone "classifiedworks.com" {
    type master;
    file "classifiedworks.db";
};
```

This statement specifies that my name server is the master name server for the classifiedworks.com domain.

- 2. Now I need to create a zone file called classifiedworks.db in the name server's working directory (specified by the options { directory path }; statement). Listing 15-2 is an example of such a zone file for the classifiedworks.com domain.

### Listing 15-2 An example zone file

```
@   IN  SOA  ns.evoknow.com. kabir.evoknow.com. (
        1999020100  ; Serial
        7200        ; Refresh - 2 hours
        3600        ; Retry  - 1 hour
        43200       ; Expire - 12 hours
        3600 )      ; Minimum - 1 hour

IN NS ns.evoknow.com.
IN MX 10 mail.evoknow.com.

www IN CNAME www.evoknow.com.
ftp IN A 206.171.50.55
```

Here I have set up SOA and NS records to state that ns.evoknow.com is the name server for the classifiedworks.com domain.

- 3. Because I want to receive mail for this domain on the mail.evoknow.com host, I set up an MX record that does just that.

- 4. I set up an alias called `www.classifiedworks.com` for `www.evoknow.com`.
- 5. Finally, I set up an A record for `ftp.classifiedworks.com` to point to 206.171.50.55.

Using the various resource records, you can configure the zone file as you need. After the zone file is configured and stored in the working directory of the DNS server, the primary name server configuration for the domain is complete.

## Configuring the slave (secondary) DNS server

Configuring a slave or secondary DNS server is quite simple. The only file you need to update by hand is the `/etc/named.conf` file. For example, say that I want to use a DNS server called ns2.evoknow.com as the secondary name server for the classifiedworks.com domain. The very first thing I need to do is create a zone statement such as the following in the `/etc/named.conf` file of the ns2.evoknow.com named server:

```
zone "classifiedworks.com" {
    type slave;
    file "classifiedworks.db";
};
```

Because this is a slave or secondary server, I do not need to create the classifiedworks.db file by hand. I can just grab the file from the primary name server for the classifiedworks.com domain using a program called named-xfer, which comes with the named distribution. Because I know the name of the primary name server for the classifiedworks.com domain to be ns.evoknow.com, I can run the named-xfer command as follows:

```
named-xfer -z classifiedworks.com -f classifiedworks.db \
-s 0 ns.evoknow.com
```

Here the -z option specifies the zone name, the -f option specifies the zone file name, and the -s option specifies the name server where the information currently resides.

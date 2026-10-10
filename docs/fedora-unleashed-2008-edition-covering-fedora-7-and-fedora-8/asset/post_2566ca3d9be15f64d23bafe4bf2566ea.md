
# Operators That Cannot Be in Local Usernames (i.e., Network Indicators)
CO @ % !

# A Class with Just Dot (For Identifying Canonical Names)
C....

# A Class with Just a Left Bracket (For Identifying Domain Literals)
C[[

# access_db Acceptance Class
C{Accept} OK RELAY
C{ResOk} OKR

# Hosts for Which Relaying Is Permitted ($=R)
FR-o /etc/mail/relay.domains

And here's a quote from the `sendmail.mc` file for comparison:

```
dnl define(`SMART_HOST', 'smtp.your.provider')
define(`confDEF_USER_ID', `08:12')dnl
undefine(`UCP_RELAY')dnl
undefine(`BITNET_RELAY')dnl
dnl define(`confAUTO_REBUILD')dnl
define(`confTO_CONNECT', `1m')dnl
define(`confTRY_NULL_MX_LIST', true)dnl
```

You can see why the file is described as cryptic.

Complicated email server setup is beyond the scope of this book; for more information on this topic, we suggest *Sendmail, 3rd Edition* by Costales and Allman, a 1,200-page comprehensive tome on Sendmail configuration. However, the following five sections address some commonly used advanced options.

## Configuring Masquerading

Sometimes you might want to have Sendmail masquerade as a host other than the actual hostname of your system. Such a situation could occur if you have a dialup connection to the Internet and your ISP handles all of your mail for you. In this case, you want Sendmail to masquerade as the domain name of your ISP. For example:

```
MASQUERADE_AS(`samplen.net.org')dnl
```

## Using Smart Hosts

If you do not have a full-time connection to the Internet, you probably want to have Sendmail send your messages to your ISP's mail server and let it handle delivery for you. Without a full-time Internet connection, you could find it difficult to deliver messages to some locations (such as some underdeveloped areas of the world where email services are unreliable and sporadic). In those situations, you can configure Sendmail to function as a smart host by passing email on to another sender rather than attempting to deliver the email directly. You can use a line such as the following in the `sendmail.mc` file to enable a smart host:

```
define(`SMART_HOST', `smtp.samplenet.org')
```

This line causes Sendmail to pass any mail it receives to the server `smtp.samplenet.org` rather than attempt to deliver it directly. Smart hosting will not work for you if your ISP, like many others, blocks any mail relaying. Some ISPs block relaying because it is frequently used to disseminate spam.

## Setting Message Delivery Intervals

As mentioned earlier, Sendmail typically attempts to deliver messages as soon as it receives them, and again at regular intervals after that. If you have only periodic connections to the Internet, as with a dialup connection, you likely would prefer that Sendmail hold all messages in the queue and attempt to deliver them at specific time intervals or at your prompt. You can configure Sendmail to do so by adding the following line to `sendmail.mc`:

```
define(`confDELIVERY_MODE', `d')dnl
```

This line causes Sendmail to attempt mail delivery only at regularly scheduled queue processing intervals (by default, somewhere between 20 and 30 minutes).

However, this delay time might not be sufficient if you are offline for longer periods of time. In those situations, you can invoke Sendmail with no queue processing time. For example, by default, Sendmail might start with the following command:

```
# sendmail -bd -q30m
```

This tells Sendmail that it should process the mail queue (and attempt message delivery) every 30 minutes. You can change 30 to any other number to change the delivery interval. If you want Sendmail to wait for a specific prompt before processing the queue, you can invoke Sendmail with no queue time, like this:

```
# sendmail -bd -q
```

This command tells Sendmail to process the queue once when it is started, and again only when you manually direct it to do so. To manually tell Sendmail to process the queue, you can use a command like the following:

```
# sendmail -q
```

![](img/34e72348d53ca54c2a1d9c871316691b_515_0.png)

If you use networking over a modem, there is a configuration file for `pppd` called `ppp.linkup`, which is located in `/etc/ppp`. Any commands in this file are automatically run each time the PPP daemon is started. You can add the line `sendmail -q` to this file to have your mail queue automatically processed each time you dial up your Internet connection.

## Building the sendmail.cf File

Books are available to explore the depths of Sendmail configuration, but the *Sendmail Installation and Operation Guide* (check on Google for this) is the canonical reference.

Configuration guidance can also be found through a Google search; many people use Sendmail in many different configurations. Fortunately, Fedora has provided a default Sendmail configuration that works out of the box for a home user as long as your networking is correctly configured and you do not require an ISP-like Sendmail configuration.

After you have made all your changes to `sendmail.mc`, you have to rebuild the `sendmail.cf` file. First, back up your old file:

```
# cp /etc/mail/sendmail.cf /etc/mail/sendmail.cf.old
```

You must run `sendmail.mc` through the m4 macro processor to generate a usable configuration file. A command, such as the following, is used to do this:

```
# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

This command loads the `cf.m4` macro file from `/usr/share/sendmail/cf/m4/cf.m4` and then uses it to process the `sendmail.mc` file. The output, normally sent to STDOUT, is then redirected to the file `sendmail.cf`, and your new configuration file is ready. You have to restart Sendmail before the changes take effect.

> **TIP**
>
> Fedora also provides an alternative to using awk to rebuild the Sendmail configuration. As root, execute the following:
>
> ```
> # make -C /etc/mail
> ```

## Mail Relaying

By default, Sendmail does not relay mail that did not originate from the local domain. This means that if a Sendmail installation running at `hudson.org` receives mail intended for `huzzilla.com`, and that mail did not originate from `hudson.org`, the mail is rejected and not relayed. If you want to allow selected domains to relay through you, add an entry for the domain to the file `/etc/mail/relay-domains`. If the file does not exist, create it in your favorite text editor and add a line containing the name of the domain that you want to allow to relay through you. Sendmail has to be restarted for this change to take effect.

> **CAUTION**
>
> You need a very good reason to relay mail; otherwise, do not do it. Allowing all domains to relay through you makes you a magnet for spammers who want to use your mail server to send spam. This could lead to your site being blacklisted by many other sites, which then will not accept any mail from you or your site’s users—even if the mail is legitimate!

## Forwarding Email with Aliases

Aliases enable you to have an infinite number of valid recipient addresses on your system, without having to worry about creating accounts or other support files for each address. For example, most systems have `postmaster` defined as a valid recipient, yet do not have an actual login account named `postmaster`. Aliases are configured in the file `/etc/aliases`. Here is an example of an alias entry:

```
postmaster: root
```

This entry forwards any mail received for `postmaster` to the `root` user. By default, almost all the aliases listed in the `/etc/aliases` file forward to `root`.

## CAUTION

Reading email as root is a security hazard; a malicious email message can exploit an email client and cause it to execute arbitrary code as the user running the client. To avoid this danger, you can forward all of root’s mail to another account and read it from there. You can choose one of two ways for doing this.

You can add an entry to the `/etc/mail/aliases` file that sends root’s mail to a different account. For example, `root: foobar` would forward all mail intended for root to the account `foobar`.

The other way is to create a file named `.forward` in root’s home directory that contains the address to which the mail should forward.

Any time you make a change to the `/etc/mail/aliases` file, you have to rebuild the aliases database before that change takes effect. This is done with the following:

```
# newaliases
```

## Rejecting Email from Specified Sites

You read earlier in this chapter that you must be careful with mail relaying to avoid becoming a spam magnet. But what do you do if you are having problems with a certain site sending you spam? You can use the `/etc/mail/access` file to automatically reject mail from certain sites.

You can use several rules in the access file. Table 21.1 lists these rules.

### TABLE 21.1 The Various Possible Options for Access Rules

| Option | Action |
| :--- | :--- |
| OK | Accepts mail from this site, overriding any rules that would reject mail from this site. |
| RELAY | Allows this domain to relay through the server. |
| REJECT | Rejects mail from this site and sends a canned error message. |
| DISCARD | Simply discards any message received from the site. |

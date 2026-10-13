
The resulting file looks similar to a typical ASCII armored encrypted file, but when the file is decrypted, the extra steps that were taken to sign it pay off. Signing encrypted files or binary files is a good way to ensure they have not been tampered with since you encrypted them. Many software packages, especially security-related software packages, are signed. This process has prevented the sabotage of at least one security program offered using anonymous FTP on the Internet.

## TROUBLESHOOTING

*I’ve set up my email client, but I seem to be having trouble sending mail. It keeps bouncing with a message about sender domain must resolve.*

You’ve probably configured your email client to use your localhost’s sendmail instead of your ISP. This will no longer work, thanks to spammers’ abuse of the email systems. Most MTAs don’t accept mail from systems if they don’t have a valid MX record. Change your email client to point to your ISP’s outgoing mail host.

*I set up my email at home to run through the sendmail server at my work rather than at my ISP, but I keep getting an error message 550 relaying denied and the messages won’t go out.*

By default, sendmail will not permit any messages to come from an external system with another external system as its destination. This is called relaying, and is prohibited. You’ll need to ask your administrator to open up your ISP’s network, your IP, or your range of IPs (if you have a dialup with dynamic IP allocation). Alternately, you’ll need to dial in to your place of work to send mail through your work mail server.

*But I am the administrator of my work system. How do I accomplish the above?*

Unfortunately, in the past, Caldera has elected not to build in the access_db into their sendmail configuration. If this is still the case, you’ll need to add access_db in a line like this in your sendmail.mc file:

```
FEATURE(`access_db', `hash /etc/mail/access.db')
```

After you’ve rebuilt your sendmail config file, you can start this and do the following:

As root, cd to /etc/mail. Create a file called access. In this file put the appropriate entry to allow yourself access, for example:

```
192.168.0        RELAY
```

The first column can be a full or partial IP address (partial assumes the entire range of IPs in that block) or a domain name. You can also specify an email address in some cases. Legitimate values that can replace RELAY include OK, REJECT, DISCARD, or certain error codes and text.

You then need to issue the following command to create the access.db file:

```
makemap hash access.db <access
```

If you feel uncertain about how to do this, you might want to consider using Webmin, which uses drop down boxes in many places and performs sanity checking.

See the sendmail documentation for more information on the use of `access_db`.

*I run a mail server. A local company asked if we could swap services, us as a secondary email server for them and they for us in case one of our mail systems goes down. Do I need to do anything special?*

Short answer: no. The only thing that needs to happen is each of you will need a second MX entry in your DNS records specifying the other sendmail system, and with a higher priority. You should not just arbitrarily add someone else’s mail server as a secondary without asking first, however.

*I’m using GnuPG and I occasionally use it when someone needs to send me confidential information. But I forgot what my pass phrase is. Can I recover it?*

Unfortunately, no. What you’ll need to do is immediately create a new private and public key pair using the method discussed in this chapter and contact anyone who has your old key and give them your new one. Don’t forget to do this if you’ve put your public key on a key server.

## DNS AND BIND

### In this chapter

- About DNS 486
- What Is BIND? 487
- BIND Files 489
- Name Server Tools 496
- Troubleshooting 504

### About DNS

You might not be familiar with DNS, but if you’ve ever surfed the Internet, you’ve made extensive use of it. Computers know how to find each other by means of their addresses, and specifically by an IP address, just as you can (usually) find the book store after looking up its address in the phone book. DNS is to computers what the phone book is to you. You don’t remember Internet sites by their IP addresses, but by their names. But you don’t know where the FOOBAZ bookstore is if you’ve never been there (or seen it in passing), so you need to look up the address. Similarly, when you want your Web browser to find www.calderasystems.com, your system uses DNS to look up the IP address.

On your Linux system you have resolver libraries that know how to resolve names into IP addresses. In your /etc/nsswitch.conf (name service switch configuration) file you have a line that looks like the following:

```
hosts:        files dns
```

This line tells the resolver routines that when they are looking for hosts, they need to first consult the system’s files, and if they don’t find what they’re looking for there, they need to perform a DNS lookup.

> **Note**
>
> The nsswitch.conf file replaced the /etc/host.conf file when Linux moved from libc5-based systems to the new glibc (libc6). The nsswitch.conf file follows Sun Microsystems’s lead and acts as a single reference for system database files for applications requiring this information.

The system files start with /etc/hosts, where commonly accessed local network hosts might be listed. This lookup is faster than a DNS lookup. But if names that might change are included, you might wonder why the lookup failed to find what you were looking for. Therefore, refrain from putting any entries over which you have no control into /etc/hosts.

The resolver libraries, failing to find the address they seek in /etc/hosts, consult /etc/resolv.conf to find the IP addresses of machines known as Domain Name Servers, or name servers for short. Up to three, but not fewer than two, need to be entered in this file. Why two? In case one is down. But no more than three are consulted, so all name server entries beyond the first three are ignored.

> **Note**
>
> If you run your own name server, you’ll want to make sure all your hosts point to your name server first. The host the name server is running on should point to 127.0.0.1 for name resolution.

### What Is BIND?

Several different DNS servers are available under different names. The most common, and the one you’ll find on your Linux system, is the Berkeley Internet Nameserver Daemon (BIND). As of this writing, the current major version number is 8.

#### About Domains

Before you go further, it is helpful to understand a little about domains. You’ve seen domain names before. They are in the form of bar.org, and contain at least two parts. Reading from the right, the org part is called a *top-level domain*. A number of top-level domains exist. In the United States, currently, are the following top-level domains:

- `.com`—Commercial entities (businesses)
- `.org`—Non-commercial organizations
- `.net`—Network affiliated organizations
- `.mil`—U.S. military branches
- `.gov`—U.S. government agencies
- `.edu`—Educational institutions
- `.int`—International organizations
- `.us`—The U.S. domain, which has each state as lower-level divisions

Additional top-level domains have been proposed, but have not yet been implemented.

In other countries, top-level domains are administered by the Internet authorities of those countries and include a two-letter country suffix. Some examples are as follows:

- `.uk`—United Kingdom
- `.ca`—Canada
- `.mx`—Mexico
- `.za`—Zuid Africa (South Africa)

Within each of the countries, a top-level domain structure, which is decided by the country’s Internet authority, exists. These might or might not correspond to the top-level domains found in the U.S.

Below the top-level domain is the name of the institution or organization that constitutes the actual domain name. For example, ibm.com, or ibm.co.uk. These examples are IBM’s domain names in the United States and the United Kingdom, respectively.

Some large domains also have *subdomains*. Very large institutions might have subdomains. For example, the army.mil domain, which has military bases all over the world and which has very large units on those bases, might be further broken down into subdomains. Therefore, a large base such as Fort Bragg, North Carolina, will have a subdomain ftbragg.army.mil. Because

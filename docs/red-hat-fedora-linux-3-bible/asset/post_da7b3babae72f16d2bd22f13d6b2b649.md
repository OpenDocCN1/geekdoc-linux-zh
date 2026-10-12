
### Checking MyISAM file: names.MYI

```
Data records:         5   Deleted blocks:           0
- check file-size
myisamchk: Warning: Size of datafile is: 89 Should be: 204
- check key delete-chain
- check record delete-chain
- check index reference
- check record links
myisamchk: error: Found wrong record at 0
MyISAM-table 'names.MYI' is corrupted
Fix it using switch "-r" or "-o"
```

3. To fix a corrupted database, you could run the following command:
   ```bash
   # myisamchk -r /var/lib/mysql/allusers/names.MYI
   - recovering (with keycache) MyISAM-table 'names.MYI'
   Data records: 5
   Found wrong stored record at 0
   Data records: 4
   ```

4. If for some reason the -r option doesn't work, you can try running the myisamchk command with the -o option. This is a slower, older method of repair, but it can handle a few problems that the -r option cannot. Here is an example:
   ```bash
   # myisamchk -o /var/lib/mysql/allusers/names.MYI
   ```

If your computer has a lot of memory, you can raise the key buffer size value on the myisamchk command line, which will lessen the time it takes to check the databases. For example, you could use the following command line:

```
myisamchk -r -O --key_buffer_size=64M *.MYI
```

This would set the key buffer size to 64MB.

## Summary

MySQL is a structured query language (SQL) server that runs on Fedora Linux, as well as other operating systems. Using a start-up script (`/etc/init.d/mysqld`) and a configuration file (`/etc/my.cnf`), you can quickly get a MySQL server up and running.

With tools such as the `mysqladmin` and `mysql` commands, you can administer the MySQL server and create databases and tables that are as simple or complex as you need. During `mysql` sessions, you can modify the structure of your database tables or add, update, and delete database records. You have a variety of options for querying data and sorting the output. You also have a lot of control over who can access your database tables and what privileges users have to modify, add to, or delete from the databases you control.

# Chapter 25
## Making Servers Public with DNS

### In This Chapter

- Determining goals for your server
- Connecting a public server
- Configuring a public server
- Setting up a DNS server

In previous chapters you built Web, mail, and FTP servers in Linux. Now you want to expose those servers to the outside world. Options range from handing them to a hosting company and saying, “Take care of it,” to managing the servers yourself out of your own home or office.

The following are some cases where you may want to consider some level of self-hosting:

- You’re willing to provide the level of support that your organization needs in its servers.
- You just want an inexpensive way to publish some documents on the Web or maintain a public mail server for a few people, and 24/7 support isn’t critical.
- You think self-hosting is cool and you want to try it.

The first goal of this chapter is to help you decide how much server support you want to maintain or provide to someone else. The second goal is to suggest how to set up your own public servers, including possibly configuring your own Domain Name System (DNS) server.

The descriptions of setting up your LAN (see Chapter 15) and connecting it to the Internet (see Chapter 16) focus on how to share information locally and let local users share an outgoing Internet connection, respectively. Building on that information, this chapter explains how to set up a DNS server, as well as other issues that relate to securing and maintaining public servers.

> CAUTION: After you open your server to Internet traffic, break-in attempts will occur. Most will come from automated scripts, sent from infected computers on the Internet. Because Red Hat Linux comes with good built-in security features, many attacks bounce off harmlessly (after logging messages). Allowing incoming connections, however, creates vulnerabilities that aren’t there with an outgoing-only Internet connection. I recommend you use security tools, described in Chapter 14, to protect your servers.

## Determining Goals for Your Server

Before you open up that server sitting in your back office to the Internet, stop for a moment and think about your goals. Here are a few questions that you may want to ask yourself:

- How critical is this server for supporting your business?
- How much traffic do you expect on your server?
- Do you need to support the server 24 hours per day, 365 days per year?
- Do you know enough to maintain and secure your server?
- Can you get the connection speed that you require at a reasonable cost for your location?
- Do you need special equipment to keep the server running, such as an uninterruptible power supply?

Maintaining a public server requires some resources. If the server is critical to your business and in high demand, you may not have the time or expertise to support this server yourself. Also, if no high-speed Internet access is available to your location, even a well-configured server may not have the bandwidth to support your clients.

## Using a hosting service

Tons of places are ready and willing to host your Web content. The number gets a bit smaller, however, if you need to find a place that can help you maintain your Red Hat Linux server. In that case, you want to find a company that offers dedicated hosting (that is, gives you control of an entire server) or permits you to co-locate your server on its premises. In either case, you want to make sure that your server:

- Is physically secure.
- Can access enough Internet bandwidth.
- Has someone there if the server goes down.

You can use such a hosting provider in these ways and still use Fedora or Red Hat Linux as your server:

- Co-locate your server at a hosting provider or ISP. In this arrangement, you can get lots of bandwidth and retain your root privileges so that you can still maintain the server yourself. The downside is that the provider probably isn’t expected to fix your server if a hardware failure occurs.
- “Rent” a server (at a place such as Rackspace.com), where you get the bandwidth and someone to fix the hardware (which that organization often puts together and maintains) if something goes wrong.

Although this setup probably costs more money, the added support and security may prove well worth it. In either of the preceding cases, where the server resides at the hosting provider, you can also expect that service to include such extras as the use of its DNS service. (In other words, after you register a domain name and sign up with the hosting service, you can probably skip the rest of this chapter.)

## Connecting a Public Server

If your organization’s Internet service is currently used for outgoing connections, you must consider different security issues if you intend to allow incoming connections. The following are some differences:

- **Outgoing connection** — By providing outgoing Internet access, you need only enable your users to connect to the Internet and gain access to other computers’ services. You don’t need a domain name, and you don’t need your own static IP address. (Chapter 16 describes how to set up a LAN to share an Internet service used primarily for outgoing service.) The focus of your network is on outgoing requests for service.
- **Incoming connection** — If you’re setting up a public server, you want people from the Internet to find you and access services that you offer. The focus is on incoming requests for your computer’s services, which means that you probably want a public host/domain name for the server and one or more static, public IP addresses for the server.

You have many different ways to connect your Fedora or Red Hat Linux server to the Internet and offer its services to the public. In the following sections, I describe what you need to get your server up and running on the Internet.

## Choosing an ISP

Although every ISP expects to see outgoing traffic on your Internet connection, not all of them expect incoming traffic (that is, traffic that someone initiates from outside your network). So although your ISP — which may be your local phone company, your cable TV company, or an independent ISP — may expect you to download files from remote servers, it may not expect people to download large files from you.

Assuming that you’re going to house the server in your place of work or residence, you need to obtain the following information from a potential ISP:

- Does its Terms of Service agreement enable you to offer services over its connection?
- Does it have static IP addresses that it’s willing to assign to you?
- Does it provide connections robust enough to handle the traffic demands on your server?

## Checking Terms of Service

Any ISP that handles more than a few users has a document that describes what you can do with the Internet connection that it provides you. That document probably carries a name such as “Terms of Service” or “User Agreement.” If you can’t find it on the ISP’s Web site, you will almost certainly see it after you click a link to sign up for an account.

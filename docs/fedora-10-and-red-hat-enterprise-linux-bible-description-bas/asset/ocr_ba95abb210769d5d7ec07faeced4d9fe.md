# Chapter 25: Making Servers Public with DNS 957

Although this setup probably costs more money, the added support and security may prove well worth it. In either of the preceding cases, where the server resides at the hosting provider, you can expect that service to include such extras as the use of its DNS service. (In other words, after you register a domain name and sign up with the hosting service, you can probably skip the rest of this chapter.)

# Connecting a Public Server

If your organization's Internet service is currently used for outgoing connections, you must consider different security issues if you want to allow incoming connections. The following are some differences:

+   * **Outgoing connection** — By providing Internet access, you only enable your users to connect to the Internet and gain access to other computers' services. You don't need a domain name, and you don't need your own static IP address (Chapter 16 describes how to set up a LAN to share an Internet service used primarily for outgoing service.) The focus of your network is on outgoing requests for services.
* **Incoming connection** — If you're setting up a public server, you want people from the Internet to find and access services that you offer. The focus is on incoming requests for your computer's services, which means you probably want a public host/domain name for the server or one more static, public IP addresses for the server.

You have many different ways to connect your Fedora or Red Hat Linux server to the Internet and offer its services to the public. In the following sections, I describe what you need to get your server up and running on the Internet.

# Choosing an ISP

Although every ISP expects to see outgoing traffic on your Internet connection, not all of them expect incoming traffic (that, traffic that someone initiates from outside your network). Although your ISP — may be your local phone company, your cable TV company, or an independent ISP — may expect you to download files from remote servers, it may not expect people to download large files from you.

Assuming that you're going to host the server in your place of work or residence, you will need to obtain the following information from a potential ISP:

+   * Does its Terms of Service agreement enable you to offer services over your connection?
* Does it have static IP addresses that it's willing to assign to you?
* Does it provide robust enough to handle the traffic demands on your server?

# Checking Terms of Service

Any ISP that has more than a few users has a document that describes what you can do with the Internet connection that it provides. That document probably carries a name such
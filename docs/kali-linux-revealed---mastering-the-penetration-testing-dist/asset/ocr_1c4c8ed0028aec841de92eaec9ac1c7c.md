# 7.3. Securing Network Services

In general, it is a good idea to disable services that you do not use. Kali makes it easy to do this since most network services are disabled by default.

As long as services remain disabled, they do not pose any security threat. However, you must be careful when you enable them:

+   - there is no firewall by default, if they listen on all network interfaces, they are effectively publicly available.
- some services have no authentication credentials and let you set them on first use; others have default (and thus widely known) credentials preset. Make sure to (re)set any password to something that you know.
- many services run as root with full administrator privileges, the consequences of unauthorized access or a security breach are therefore severe.

# Default Credentials

We won't list all tools that come with default credentials, instead you should check the README Debian file of the respective packages, as well as docs.kali.org and tools.kali.org to see if the service needs some special care to be secured.

If you run in live mode, the password of the root account is "toor". You should not enable SSH before changing the password of the root account, or before tweaked its configuration to disallow password-based logins.

Note that the Beef project (from the already-installed package beef-xss) is also known to have default credentials user "beef", password "beef" hardcoded in its de-fault configuration file.

# 7.4. Firewall and Packet Filtering

A firewall is a piece of computer equipment with hardware, software, or both that parses the incoming or outgoing network packets (coming to or leaving from a local network) and only lets through those matching predefined conditions.

A filtering network gateway is a type of firewall that protects an entire network. It is usually installed on a dedicated machine configured for the network so that it can parse all packets that pass in and out of the network. Alternatively, a local firewall is a software service that runs on one particular machine in order to filter or limit access to services on that machine, or possibly to prevent outgoing connections by rogue software that a user could, willingly, or not, have installed.

> https://docs.kali.org

> https://tools.kali.org
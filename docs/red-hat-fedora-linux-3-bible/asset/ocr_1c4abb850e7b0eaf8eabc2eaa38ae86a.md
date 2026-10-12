# Keeping up with updates

You can expect to find and correct security breaches continuously. You must keep up with software updates that are published to plug security holes. Although some of these updates address theoretical security problems, others are created in response to real break-ins or denial-of-service attacks that are known to exploit weaknesses in the components that come with your operating system.

For Red Hat Enterprise Linux systems, using the Red Hat Network (and its update facility) is the best way of getting security updates on a timely basis. That database also contains information tailored for Red Hat Linux. For Fedora Linux, you can use update or yum to download and install updates from Fedora mirror sites that carry those updates (see Chapter 5 for information on using yum). You should also check CERT and other organizations (which I describe in Chapter 14) for security alerts.

After your server is secure and correctly configured, your last step is to start the server on the Internet with a domain name that points to it. Either ask your service provider to configure DNS for you, or set up your own DNS server, as I describe in the following section.

# Setting Up a Domain Name System Server

The Domain Name System (DNS) is essentially a distributed database that translates host names into IP addresses (and IP addresses back to host names). That database also contains information related to each domain, such as how the domain is organized into zones, where to route mail for that domain, and who to contact with questions associated with the domain.

By setting up a DNS server, you become part of a hierarchy of DNS servers that make up the Internet. At the top of this hierarchy is the root server, represented by a dot (.). Below the root server are the Top Level Domains, or TLDs (such as .com, .org, and so on). Domains that individual organizations own and maintain lie below the TLDs. That’s where you come in.

As someone who’s setting up a DNS server, you be responsible for managing the host names and IP addresses for the computers in the domain (or domains) for which you’re responsible. Keeping your DNS information current means that people can access the services that you want to share, and the Internet as a whole works that much better as a result.

Besides using your DNS server to help people from the Internet find the public servers in your domain, you can also use DNS to provide name and IP address mapping for computers on your private network. The example in the “DNS name server example” section later in this chapter describes how to configure both private and public name and IP address records for a domain.
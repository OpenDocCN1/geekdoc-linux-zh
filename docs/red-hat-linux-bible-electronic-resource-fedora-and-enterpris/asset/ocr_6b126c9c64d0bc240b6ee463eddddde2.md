If you need to communicate across the peer to another computer, make sure that you have set the routes up to do that. In particular, if you are creating a CIPE connection over a PPP dial-up connection directly to your company, and are routing from there to the Internet, make sure that the remote CIPE computer knows to route data back to your CIPE interface.

# # Setting up Red Hat Linux as a Proxy Server

You have a LAN set up, and your Red Hat Linux computer has both a connection to the LAN and a connection to the Internet. One way to provide Web-browsing services to the computers on the LAN without setting up routing is to configure Red Hat Linux as a proxy server.

The Squid proxy caching server software package comes with Red Hat Linux. In a basic configuration, you can get the software going very quickly. However, the package is full of features that let you adapt it to your needs. You can control which hosts have access to proxy services, how memory is used to cache data, how logging is done, and a variety of other features. Here are the basic proxy services available with Squid:

+   • **HTTP** — Allowing HTTP proxy services is the primary reason to use Squid. This is what lets client computers access Web pages on the Internet from their browsers (through your Red Hat Linux computer). In other words, HTTP proxy services will find and return the content to you for addresses that look similar to this: www.ab.com.

+   • **FTP** — This represents File Transfer Protocol (FTP) proxy services. When you enable HTTP for a client, you enable FTP automatically (for example, ftp://ftp.ab.com).

+   • **Gopher** — The gopher protocol proxy service was one of the first mechanisms for organizing and searching for documents on the Internet (it predates the Web by more than a decade). It isn’t used much anymore. However, if you need to use it, gopher is supported when you enable HTTP for a client.

Besides allowing proxy services, Squid can also be part of an Internet cache hierarchy. Internet caching occurs when Internet content is taken from the original server and copied to a caching server that is closer to you. When you, or someone else in the caching hierarchy, requests that content again, it can be taken from the caching server instead of from the original server.

You don’t have to cache Internet content for other computers to participate in caching with Squid. If you know of a parent caching-computer that will allow you access, you can identify that computer in Squid and potentially speed your Web browsing significantly.

Caching services in Squid are provided through your Linux system’s ICP port. Besides ICP services, you can also enable Simple Network Management Protocol (SNMP) services. SNMP lets your computer make statistics and status about itself available to SNMP agents on the network. SNMP is a feature for monitoring and maintaining computer resources on a network.

> **CAUTION:** SNMP poses a potential security risk if it is not configured properly. Use caution when configuring SNMP with Squid.
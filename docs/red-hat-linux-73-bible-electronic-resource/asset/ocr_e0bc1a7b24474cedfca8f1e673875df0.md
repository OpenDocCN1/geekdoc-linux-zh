+   6. Click the DNS Configuration tab, type in the number of the DNS server that you use to resolve addresses on the Internet, and then click Add. Repeat this step if you have multiple DNS servers.

+   7. Click OK.

+   8. You may need to reboot your computer at this point, if Windows requires you to do so.

At this point, try accessing a Web site from your Internet browser on the Windows computer. If the Internet connection is up on your Red Hat Linux computer, you should be able to connect to the Internet through your LAN connection to the Red Hat Linux computer.

# ## Setting up Red Hat Linux as a Proxy Server

You have a LAN set up, and your Red Hat Linux computer has both a connection to the LAN and a connection to the Internet. One way to provide Web-browsing services to the computers on the LAN without setting up routing is to configure your Red Hat Linux computer as a proxy server.

The Squid proxy caching server software package comes with Red Hat Linux. In a basic configuration, you can get the software going very quickly. However, the package is full of configuration features that let you adapt it to your needs. You can control which hosts have access to proxy services, how memory is used to cache data, how logging is done, and a variety of other features. Here are the basic proxy services available with Squid:

+   *   **HTTP** — Allowing HTTP proxy services is the primary reason to use Squid. This is what lets client computers access Web pages on the Internet from their browsers (through your Red Hat Linux computer). In other words, HTTP proxy services will find and return the content to you for addresses that look similar to this:
+       www.whatever.com.

+   *   **FTP** — This represents File Transfer Protocol (FTP) proxy services. When you enable HTTP for a client, you enable FTP automatically (for example, ftp://ftp.whatever.com).

+   *   **Gopher** — The gopher protocol proxy service was one of the first mechanisms for organizing and searching for documents on the Internet (it predates the Web by more than a decade). It isn’t used much anymore. However, if you need to use it, gopher is supported when you enable HTTP for a client.

Besides allowing proxy services, Squid can also be part of an Internet cache hierarchy. Internet caching occurs when Internet content is taken from the original server and copied to a caching server that is closer to you. When you, or someone else in the caching hierarchy, requests that content again, it can be taken from the caching server instead of having to be retrieved from the original server.
and launching the appropriate service program when needed. The inetd program uses the `/etc/inetd.conf` configuration file to allow you to define the services for which it handles requests.

The *extended internet daemon* (xinetd) application is an advanced version of inetd. It too launches service programs as requested by clients, but it contains additional features, such as access control lists (ACLs), more advanced logging features, and the ability to set schedules to turn services on and off at different times of the day or week.

![](bbox=[0.13, 0.26, 0.84, 0.32])

# ### Listening for Clients

A standard Linux server supports lots of services. Usually, a single Linux server will support multiple services at the same time. This means multiple clients will be making requests to the server for multiple services. The trick is in getting requests from clients to the correct server service.

Each service, whether it’s running as a *daemon* or running from a super-server, uses a separate network protocol to communicate with its clients. Common service protocols are standardized by the *Internet Engineering Task Force* (IETF) and published as *Request for Comments* (RFC) documents. Each server software program communicates with its clients using the protocol specified for its service, such as a web server using HTTP or an email server using SMTP.

The network protocol for a service defines exactly how network clients communicate with the service, using preassigned *network ports*. Ports are defined within the TCP and UDP standards to help separate network traffic going to the same IP address. The IETF assigns different services to different ports for communication. This works similarly to telephone extensions used in a large business. You enter a single phone number to reach the business and then select a separate extension to get to a specific individual within the office. With services, clients use a common IP address to reach a server and then different ports to reach individual services.

The IETF has defined a standard set of ports to common services used on the Internet. These are called *well-known ports*. Table 2.1 shows just a few of the more common well-known ports assigned.

A host of Linux services are available for serving applications to clients on the network. The `/etc/services` file contains all of the ports defined on a Linux server.

The following sections explore the different types of services you will find on Linux servers as well as common Linux applications that provide those services.
# 7.2.2 Thin client

Thin client solutions involve many clients (either standard workstations or diskless terminals) booting over the network off of a central server. Because applications are all run on the server, upgrades and patches only need to be applied to one location. Also, most user data is stored on the server, so users can use any client connected to the server and receive the same experience. Depending on the solution in use, thin clients can require a substantial amount of network bandwidth between the clients and the server. Modern thin client solutions include the Linux Terminal Server Project at:

```
http://www.ltsp.org
```

And various thin client solutions from Neoware:

```
http://www.neoware.com
```

# 7.2.3 Application forwarding

The X client/server environment (as described in 5.2.4, "Graphical and text-based environments") on page 118 allows a more granular approach to remotely. Because X clients send their displays through networking sockets to connect to a local X server, forwarding the display to a remote X server is trivial and requires no changes to the client. There are numerous scenarios where application forwarding could reduce technical support issues, such as configuring a desktop to run-mail and Web browsing applications locally, but to connect to a network server to run an in-house application which receives frequent updates. X forwarding can be tunneled over a Secure Shell (SSH) to connect the session, allowing for secure application forwarding over the Internet or an unsecured portion of your intranet. It is also possible to use NoMachine or FreeNX, which compresses the session significantly, making applications far more responsive over slower connections, and usable over dial-up connections.

Similar application renting can be done with Windows applications running through products such as San Secure Global Desktop Software (formerly Tarantella) or Microsoft Terminal Server. These services can be useful for unmigratable applications; the unmigratable application can run on the server, while all other applications run locally.

# 7.2.4 Multi-station computing

Thin client solutions are often limited in performance their deployment require extensive infrastructure. Performance and response time are highly sensitive to network traffic between the client and the server, potentially frustrating some users. Multi-station computing based on standard desktop computing
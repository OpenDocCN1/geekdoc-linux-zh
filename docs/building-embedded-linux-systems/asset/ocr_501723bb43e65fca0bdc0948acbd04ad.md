![](bbox=[0.14, 0.07, 0.86, 0.48])

*Figure 4-13. Eclipse Remote System Explorer browser*

**Defining remote connections.** To use all the features the RSE framework has to offer, you must configure some remote machines or target boards to interact with. To do this, open the Open Perspective submenu in the Window menu and choose Remote Systems Perspective (Figure 4-13).

At the right of the screen, the Remote Systems list will open with a list of all previously configured remote systems. To create a new connection, right-click in the Remote Systems list window and choose New Connection. This displays a Remote System Type wizard (Figure 4-14).

If autdiscovery via DNS-SD Service Discovery (previously known as Zeroconf) is available, it will be automatically selected for you. Otherwise, you can manually configure a new remote connection.

After a connection has been created, you can browse the resources it provides via the Remote Systems view. Resources include remote files, remote shells, and views of remote processes, if available. Not all types of connections provide all the functionality, and some require the store agent to be running on the remote target.

In addition, once a connection has been defined in such a fashion, it will show up in the list of available connections in the *C/C++* Remote Application menu in both the
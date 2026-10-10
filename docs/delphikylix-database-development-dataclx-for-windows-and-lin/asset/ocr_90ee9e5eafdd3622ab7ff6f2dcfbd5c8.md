Client 5: Server3, Server1, Server2

Client 6: Server3, Server2, Server1

Assuming that all servers are up and running, this will balance the load equally over the three servers, with two clients connected to each server.

# ## Summary

This chapter discussed DataSnap, Delphi's remote access technology for multiier database development.

+   - The first step in creating a separate application server is to set up one or more remote data modules. Delphi supports the creation of standard, MTS, CORBA, and SOAP remote data modules.

+   - To create methods for use with an application server, use the Add to Interface menu item. To create a callback interface, use the Type Library editor to create a new interface.

+   - To create a simple user interface for the application server, post a custom message to the main form whenever a remote data module is created or destroyed. A reasonable place to do this is in the data module's `OnCreate` and `OnDestroy` event handlers.

+   - You can connect to the application server from a client application, using a variety of connection protocols, including `TSocketConnection`, `TDCOMConnection`, `TWebConnection`, `TSOAPConnection`, and `TCORBAConnection`.

+   - The briefcase model allows your application to download data to the local machine for use when it is impossible to connect to the server.

+   - To facilitate the use of multiple application servers in a large-scale application, Delphi provides the `TConnectionBroker` component.

The next chapter introduces a complete application that uses many of the techniques discussed in this chapter and throughout the rest of the book.
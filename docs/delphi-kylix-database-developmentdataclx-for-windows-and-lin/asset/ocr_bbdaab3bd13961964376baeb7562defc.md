The previous chapter gave an overview of providers and explained how to use them in a multi-  
tier application where the client and application server are physically located in a single exe-
cutable.

This chapter expands the discussion to show you how to create multitier database applications where the client and application server are in different executables, which may then run on the same machine or, more likely, on two separate computers.

Delphi supports a number of underlying protocols to connect to an application server, in-  
cluding DCOM, CORBA, HTTP, and SOAP. This book does not attempt to explain any of these 
technologies in detail. Rather, it describes how to set up the required connection component for 
each of the technologies. It is assumed that you already have the necessary software installed 
and functioning properly for the protocol that you will use to connect to the application server.

# # What Is DataSnap?

DataSnap is the technology that allows client applications to connect to providers in an appli-
cation server. DataSnap is implemented by a number of components that can be used to con-
nect different machines through such underlying technologies as sockets, DCOM, CORBA, 
HTTP, and SOAP.

> **NOTE** 
> In earlier versions of Delphi, DataSnap was named MIDAS. Because of international 
> trademark considerations, the name MIDAS has been changed to DataSnap.

# # Creating the Application Server

This section describes the steps necessary to create an application server. The application 
server contains all the code necessary to connect to the underlying database and provide the 
resulting data to the client application. As you’ll learn later in this section, the application 
server can also provide other, possibly non-database related, services to the client.

# # Remote Data Modules

When creating the application server, the first order of business is to set up one or more 
remote data modules. A remote data module is simply a data module that can be accessed 
remotely from a client application. The remote data module contains the components that we 
placed on the server-side data module in the previous chapter.

To check whether details have been fetched for the current contact, the code looks at `cddsTodos.RecordCount`. `RecordCount` will be `MaxInt - 1` if details have not yet been fetched. Figure 7.6 shows the main form of the DataFetch application at runtime.

![](img/fe651f295b5f960d5463c4fb581d2281_327_0.png)

## **FIGURE 7.6**
*DataFetch shows how to fetch details and BLOBs on demand.*

## Summary

This chapter introduced you to providers and multitier database development, including the following key concepts:

-   A `DatasetProvider` is a conduit between a client dataset and an external data store. It provides data to the client dataset on request and resolves data back to the database when the client applies updates.
-   You need to call the client dataset's `ApplyUpdates` method to save changes to a database permanently.
-   For greatest control over reconciliation errors, you should provide an event handler for the client dataset's `OnReconcileError` event. Delphi comes with a prewritten function, named `HandleReconcileError`, that you can use to facilitate this process.
-   By calling `TClientDataSet.Refresh`, you can ensure that the client always has the latest copy of the data from the server.
-   You can set the provider's update mode to `upWhereAll`, `upWhereChanged`, or `upWhereKeyOnly` for finer control over how each record is updated.
-   You can take advantage of numerous provider options and events for finer control over the entire provide/resolve process.
-   When creating a master/detail relationship on the server-side components, the client dataset will represent that relationship as a nested dataset.
-   By handling the provider's `OnGetTableName` event, you can update data returned from a stored procedure.
-   By handling the provider's `BeforeUpdateRecord` event, you can update data returned from a join operation.
-   You can call `TClientDataSet.SetProvider` at runtime to establish a connection between client datasets and providers on different forms or data modules.
-   To replace separate `TSQLDataSet`, `TDataSetProvider`, and `TClientDataSet` components, use `TSQLClientDataSet`.
-   To limit the amount of data returned by the server at a single time, set the provider's `poFetchBlobsOnDemand` and/or `poFetchDetailsOnDemand` options, and then call `TClientDataSet.FetchBlobs` or `TClientDataSet.FetchDetails` manually.

The next chapter expands on this discussion to show you how to create a multitier application with separate server and client executables.

# DataSnap

# CHAPTER 8

# IN THIS CHAPTER

-   What Is DataSnap? 318
-   Creating the Application Server 318
-   Creating the Client Application 329
-   A Complete Example 336
-   The Briefcase Model 340
-   Stateless Servers 341
-   Sharing a Connection Between Multiple Client DataSets 343
-   Brokering Connections Between Multiple Servers 348

The previous chapter gave an overview of providers and explained how to use them in a multitier application where the client and application server are physically located in a single executable.

This chapter expands the discussion to show you how to create multitier database applications where the client and application server are in different executables, which may then run on the same machine or, more likely, on two separate computers.

Delphi supports a number of underlying protocols to connect to an application server, including DCOM, CORBA, HTTP, and SOAP. This book does not attempt to explain any of these technologies in detail. Rather, it describes how to set up the required connection component for each of the technologies. It is assumed that you already have the necessary software installed and functioning properly for the protocol that you will use to connect to the application server.

## What Is DataSnap?

DataSnap is the technology that allows client applications to connect to providers in an application server. DataSnap is implemented by a number of components that can be used to connect different machines through such underlying technologies as sockets, DCOM, CORBA, HTTP, and SOAP.

> **NOTE**
> In earlier versions of Delphi, DataSnap was named MIDAS. Because of international trademark considerations, the name MIDAS has been changed to DataSnap.

## Creating the Application Server

This section describes the steps necessary to create an application server. The application server contains all the code necessary to connect to the underlying database and provide the resulting data to the client application. As you’ll learn later in this section, the application server can also provide other, possibly non-database related, services to the client.

### Remote Data Modules

When creating the application server, the first order of business is to set up one or more remote data modules. A remote data module is simply a data module that can be accessed remotely from a client application. The remote data module contains the components that we placed on the server-side data module in the previous chapter.

In many, if not most, application servers, a single remote data module will suffice. However, you can create multiple remote data modules in a single application server if you want. Some reasons for doing so include the following:

-   The application server needs to connect to multiple databases, and you want to create a distinct remote data module for each database connection.
-   Two types of users will run this application—perhaps a “normal” user and an administrator. You may want to create two separate remote data modules, in which the remote data module used for administrators contains additional tables or queries for sensitive data.
-   One data module is used to provide access to the underlying database, and another data module is used to provide other, non-data-aware services, such as numeric calculations. This capability is discussed later, in the section titled “Adding Methods to the Remote Data Module.”

### Creating a Remote Data Module

Creating a remote data module for non-SOAP applications is a straightforward operation.

-   Create a new application, which will be the application server.
-   From Delphi’s main menu, select File, New, Other. Delphi’s New Items dialog is displayed. Select the Multitier tab. The New Items dialog should look like the image shown in Figure 8.1.
-   Select one of the remote data modules from the list and click OK. The different data modules are discussed in the following sections.

![](img/fe651f295b5f960d5463c4fb581d2281_331_0.png)

## **FIGURE 8.1**

Delphi supports three remote data modules—Remote Data Modules, Transactional Data Modules, and CORBA Data Modules.

### Creating a Standard Remote Data Module

The examples presented in this book all use a standard remote data module. This type of data module is used for clients connecting through sockets, DCOM, or HTTP connections.

To create a TRemoteDataModule, select Remote Data Module from the Multitier page of the New Items dialog and click OK. The dialog shown in Figure 8.2 appears.

![](img/fe651f295b5f960d5463c4fb581d2281_332_0.png)

## **FIGURE 8.2**

*Creating a standard remote data module.*

Enter a CoClass name for the data module, such as **ContractDataServer** or some other meaningful name. The application name and CoClass together form the name by which the remote data module is referenced. For example, if the application name is ContractServer and the CoClass name is ContractDataServer, the remote data module is referenced from the client application as **ContractServer.ContractDataServer**.

Select the type of instancing to use for the remote data module. Table 8.1 lists the possible values for this selection.

**TABLE 8.1** *Instancing Values*

| Value | Description |
| :--- | :--- |
| Internal | The remote data module cannot be created from an external client. Internal remote data modules are always created from within the server application. |
| Single Instance | Each client that attempts to connect to the server will cause a separate instance of the server executable to run. |
| Multiple Instance | Only one copy of the server executable will run, but it will instantiate a separate remote data module for each client that connects to it. |

In most situations, you should leave the Instancing combo box set to **Multiple Instance**.

Lastly, select the threading model to use for the remote data module. Table 8.2 lists the possible values for the Threading Model combo.

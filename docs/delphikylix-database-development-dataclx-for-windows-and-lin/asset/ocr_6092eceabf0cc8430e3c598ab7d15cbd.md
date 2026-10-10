# # Connecting to a Local Database

This chapter explains how to take advantage of providers in a multitier application in which the client and server are both physically located in the same executable. Even under this arrangement, it is beneficial to structure the application such that it is a relatively simple matter to move the server into its own application if you then decide to move to separate server and client applications.

To facilitate this, you should put server-side components on a separate data module from client-side components. Under this arrangement, your application would have the following structure:

+   - Server data module This contains the connection to the database, along with the necessary datasets and providers.
+   - Client data module This contains the client datasets and (optionally) data sources.
+   - Forms and units The forms and supports units in the application will reference the data from the client data module.

Other than from inside the server data module, you should not reference any components on the server side of the equation, including the database connection or datasets. All data access should be performed through the client data module. If you impose this restriction on your code, it will go a long way toward simplifying moving the server data module out into its own application.

# ## Using Providers Located on a Different Form

After you move the data access components and providers onto a separate data module, the client dataset won't be able to directly connect to the dataset provider. In other words, the `TClientDataSet`'s `ProviderName` property won't list the provider in its drop-down list, because the provider is not on the same form (or data module).

To provide access to the provider(s) on the server-side data module to your client datasets, you either need to call `TClientDataSet.SetProvider` or use a `TLocalConnection` component, discussed in the next chapter.

For now, at runtime, you can call `TClientDataSet.SetProvider` to establish a connection to a provider on a different form or data module. The following line of code shows how this is done:

```
`ClientDataSet1.SetProvider(ServerDM.pvContacts);`
```
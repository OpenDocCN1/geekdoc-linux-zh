For example, a database might include a trigger for autogenerating a table's primary key, using a generator. At the time a new record is posted to the database, the value of that field may be NULL. During the post operation, the database will fill in the value of the primary key, and poAutoRefresh will then reread the record so the Delphi application knows the value of the primary key.

Without the poAutoRefresh option, you can still autoassign primary key values to a record, but you will need to perform a little work in the server-side data module. This technique is explained later, in the section titled "Changing Field Values on the Server."

# # Provider Events

TDataSetProvider publishes two types of events—OnXxx and BeforeXxx/AfterXxx. The BeforeXxx/AfterXxx events fire before and after “interesting” things happen in the provider, such as when updates are applied to the underlying database.

Table 7.7 lists the Before and After events supported by TDataSetProvider.

TABLE 7.7 TDataSetProvider BeforeXxx/AfterXxx Events

| Event | Description |
| :--- | :--- |
| AfterApplyUpdates | Fired after the updates to the database are complete. |
| AfterExecute | Fired after the server executes the query or stored procedure that will ultimately return data to the client. |
| AfterGetParams | Fired after the server returns output parameters from the dataset to the client dataset. |
| AfterGetRecords | Fired after the provider creates the data packet to send to the client. |
| AfterRowRequest | Fired after the provider refreshes the current record because of a call to TClientDataSet.RefreshRecord or any other method that fetches data. |
| AfterUpdateRecord | Fired after a record is successfully updated. |
| BeforeApplyUpdates | Fired before updates are applied to the database. |
| BeforeExecute | Fired before the server executes a query or stored procedure. |
| BeforeGetParams | Fired before the server returns output parameters from the dataset to the client dataset. |
| BeforeGetRecords | Fired before the provider creates the data packet to send to the client. |
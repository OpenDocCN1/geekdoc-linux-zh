# # Stateless Servers

In the last chapter, I showed you how you can limit the amount of data returned at a given time from the application server. The catch with limiting the amount of data returned from the server is that you must let the server know from where to start retrieving data each time it fetches a new data packet. Delphi database applications are stateless, meaning that the server-side database components don't keep track of their current location in the dataset. When the provider retrieves data from a TSQLDataSet or other dataset component, the dataset is opened, data is sent to the provider, and then the dataset is closed. Because the dataset is accessed only for a short period of time, a single server-side dataset can service multiple client applications, reducing memory load and increasing performance. This isn't much of an issue with a local connection, but it becomes an important consideration when using remote connections.

Conceptually, incremental data fetching on a stateless server works like this:

+   - The provider fetches a set of records, remembering the ID of the last record in the batch.
+   - The provider notifies the client application of the last record.
+   - The client remembers the last record fetched.
+   - When the client fetches the next batch of records from the server, it notifies the server of the last record previously retrieved.
+   - The server retrieves the next batch of records that occurs after the last record previously retrieved.

To implement a stateless server, you need to supply event handlers for three provider events on the server, as well as for two client dataset events on the client. Let's start with the server:

In the application server, you need to set up the TSQLDataSet as a parameterized query, like this:

```
SELECT * FROM CONTACTS WHERE ID > :MinID ORDER BY ID
```

This will select only contacts with an ID greater than the last ID that has already been fetched. Now, provide an event handler for the provider's OnGetData event. In this event, you'll save the last ID retrieved from the contact table.

```
procedure TStatelessServerData.pvContactsGetData(Sender: TObject;
DataSet: TCustomClientDataSet);
begin
DataSet.Last;
pvContacts.Tag := DataSet.FieldName('ID').AsInteger;
end;
```

![](bbox=[0.85, 0.45, 0.98, 0.59])
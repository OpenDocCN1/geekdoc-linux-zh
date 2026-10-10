| **TABLE 7.6** | Continued |
|:--|:--|
| *Option* | *Description* |
| poCascadeDeletes | Used when the provider is part of a master/detail relationship. When True, the server deletes detail records automatically when the master record is deleted. |
| poCascadeUpdates | Used when the provider is part of a master/detail relationship. When True, the server automatically updates detail records when the key value(s) of the master record changes. |
| poReadOnly | When True, you can’t edit the data in the client dataset. |
| poAllowMultiRecordUpdates | When True, allows updates that affect multiple records. When False, updates that affect more than one record raise an exception. |
| poDisableInserts | When True, client datasets will not be able to `Insert` or `Append` new records. |
| poDisableEdits | When True, client datasets will not be able to `Edit` existing records. |
| poDisableDeletes | When True, client datasets will not be able to `Delete` existing records. |
| poNoReset | When True, calls to AS_GetRecords ignore the reset flag. |
| poAutoRefresh | When True, the provider automatically refreshes updated records with the latest data from the database. It is important to note that this option is not yet implemented in Delphi as of version 6. |
| poPropagateChanges | When True, any changes made to data during the `BeforeUpdateRecord` or `AfterUpdateRecord` event handlers are sent back to the client. |
| poAllowCommandText | When True, the client dataset can override the `CommandText` property of the provider’s dataset. When False, attempting to set the client dataset’s `CommandText` property raises an exception. |
| poRetainServerOrder | When True, alerts the client dataset that it should not attempt to sort the data returned from the server. |

At the time of this writing, the `poAutoRefresh` option is not implemented. `poAutoRefresh` will be useful for refreshing an updated record from the database when the database fills in field values automatically.
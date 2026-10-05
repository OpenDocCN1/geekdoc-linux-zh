Using comparisons property, you can test attributes. But how can you find out which attributes are there? Turns out that there is a method, RetrieveArgumentDescription, on the EventManager object which returns all arguments (or attributes) that you can use with an event trigger. Table 17.4 lists the attributes that you can use with any event. The attributes that are marked as having void types are, in fact, managed object IDs. Not hard to use in a comparison, but we included them in the table since the RetrieveArgumentDescription method will return them!

# Table 17.4 Common event attributes

| Attribute | Type |
| --- | --- |
| changeTag | string |
| computeResource | mold |
| computeResource.name | string |
| datacenter | mold |
| datacenter.name | string |
| ds | mold |
| ds.name | string |
| dvs | mold |
| dvs.name | string |
| fullFormattedMessage | string |
| host | mold |
| host.name | string |
| net | mold |
| net.name | string |
| username | string |
| vm | mold |
| vm.name | string |

In addition to the common attributes, some events accept additional attributes. They are listed under the Attributes property in the objects of the Get-AlarmEvent function returns. With the AccountRemovedEvent event, for example, you can use the attribute to filter out the alarms for test accounts. The operators you use for these comparisons are documented in the EventAlarmExpressionComparisonOperator enumerator that you can find in the API Reference. The other properties in the EventAlarmExpression object are clearly explained in the vSphere API Reference documentation.
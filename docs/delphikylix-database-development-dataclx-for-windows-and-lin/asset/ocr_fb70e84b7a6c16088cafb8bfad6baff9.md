This is what the lookup data-aware controls are designed for—displaying a list from one dataset and enabling the user to select an item to be stored in another dataset.

To complete the link to the lookup dataset, lookup data-aware components provide four additional properties: ListSource, ListField, KeyField, and ListFieldIndex.

+   - ListSource references the data source of the dataset from which to retrieve the list of values.

+   - ListField is a semicolon-delimited list of field names that are to be displayed in the component.

+   - KeyField determines the field whose value is to be stored in the dataset.

+   - ListFieldIndex is a zero-based number that determines the field to be used for incremental searching in the component. For example, say that you set the ListField property to FirstName; LastName. This instructs the component to display the first name and the last name in the list. If you set ListFieldIndex to 1, as the user types set in the control, it performs automatic incremental searching on the LastName field.

Lookup data-aware components consist of TDBLookupComboBox and TDBLookupListBox. These components look and act like TDBComboBox and TDBListBox (respectively), except that rather than populating the items manually, TDBLookupComboBox and TDBLookupListBox retrieve their items from the dataset referenced through the component's ListSource property.

![](bbox=[0.04, 0.68, 0.15, 0.72])

> You can duplicate the functionality of the TETHDBComboBox and TETHDBListBox components by using TDBLookupComboBox and TDBLookupListBox. To do this, create a TCClientDataSet that contains the Items and Values associations that are set in the TETHDBComboBox or in the TETHDBListBox. If you only have a single occurrence of this in your application, you might elect to go this route. However, if you have numerous occurrences, your form becomes littered with lookup datasets and you might find it easier to use TETHDBComboBox and TETHDBListBox instead.

# # TDBNavigator

The remaining components discussed in this chapter are used for displaying and editing data, but TDBNavigator provides a code-free means of navigating and manipulating a dataset. Visually, TDBNavigator looks like a toolbar because it contains a horizontal array of predefined buttons (actually, TSpeedButtons), which are listed in Table 5.8.
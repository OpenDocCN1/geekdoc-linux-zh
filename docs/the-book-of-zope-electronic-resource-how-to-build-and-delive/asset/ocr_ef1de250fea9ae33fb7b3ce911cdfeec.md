# Table 11-3: Usage values for range matching

| Range usage value | Description |
| range:min | Matches indexed values equal to or greater than the range value. |
 range:max | Matches indexed values less than or equal to the range value. |
 range:min:max | Matches indexed values between a specified and maximum value. |

For example, let's consider how we query the ZCatalog by date, using the bobabase_modification_time index to find objects based on their modified date and time.

For our first example, let's find all cataloged objects modified in the last 30 days. This could be used in our bookstore application to find recently added or modified instances.

```
expr="Catalog(bobabase_modification_time=ZopeTime())-30,
bobabase_modification_time_usage='range:min'
```

In the first argument, which matches the index name, we pass the value of the current Zope system date and time minus 30, which calculates the date 30 days prior to our search value. The second usage argument instructs the ZCatalog to return objects whose date is equal to or greater than the search value.

By simply changing the usage value, we could find all object that have not been modified for 30 days, as follows:

```
expr="Catalog(bobabase_modification_time=ZopeTime())-30,
bobabase_modification_time_usage='range:max'
```

To match values that fall between two values (a minimum and maximum), you must pass a list containing at least two items as the search value. The item of the list with the smallest value is treated as the minimum search value and the item with the largest value as the maximum search value. For example, to find all cataloged objects modified yesterday, we could use the following expression:

(ZopeTime()-1) returns the date and time 24 hours ago as a Date Object. To determine the starting and ending time of the previous day for our use as minimum and maximum values, we use the earliest() and latestTime() method respectively of the DateTime object. These are passed in a two-item list as the search value. We then use the range:min:max usage value to instruct the ZCatalog to perform the bounded query.
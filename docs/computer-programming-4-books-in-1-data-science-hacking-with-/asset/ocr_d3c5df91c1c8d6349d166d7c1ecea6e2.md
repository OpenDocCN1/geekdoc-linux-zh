For the case of DataSeriesGrouped, every subseries will be attached to a scalar, and all the following scalars will be joined into a DataSeries. When it comes to the DataFrameGrouped, it will include the block to every column of each sub-data frame and display the eventual matrix of scalars as a new DataFrame.

Aggregation happens with the use of messages. It requires a block as an argument, and uses it on every value of the groups series, and then integrates into a new data structure.

The most common aggregation functions, such as average, min, and max deliver shorter messages. In the following iteration, these messages are useful and work as shortcuts.

```
average
\^ self apply: [:each | each average].
```

However, these messages will carry the optimized implementations of the likened aggregations because it is necessary that these functions are time and memory efficient.

Let’s examine the grouping series.

The easiest example of using this groupBy operator is to classify the values of a series using values of the same size.

```
bill := tips column: #total bill.
sex := tips column: #sex.bill groupBy: sex.
```

The result of the above query will be an object. This object will separate the bill into two series.

Because a lot of time, you need to classify the group series that resemble columns of a single data frame. There is a useful shortcut.

# How to Group Data Frames?

Besides the shortcut for classifying columns. The DataFrame has a method for classifying one of its columns.

The response of the above query will be an object of DataFrameGrouped, keeping two different data frames for smokers and non-smokers.
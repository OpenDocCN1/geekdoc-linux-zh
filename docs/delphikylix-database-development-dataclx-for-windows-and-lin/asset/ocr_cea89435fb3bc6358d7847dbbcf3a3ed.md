**TABLE 3.4** Sample Data for Ranges and Filters

| ID | Name | Birthday | Salary |
| :--- | :--- | :--- | :--- |
| 4 | Bill Peterson | 3/28/1957 | $60,000.00 |
| 2 | Frank Smith | 8/25/1963 | $48,000.00 |
| 3 | Sarah Johnson | 7/5/1968 | $52,000.00 |
| 1 | John Doe | 5/15/1970 | $39,000.00 |
| 5 | Paula Wallace | 1/15/1971 | $36,500.00 |

The data in this much-abbreviated table is indexed by birthday. Ranges can only be used when there is an active index on the dataset.

Assume that you want to see all employees who were born between 1960 and 1970. Because the data is indexed by birthday, you could apply a range to the dataset, like this:

```
ClientDataSet1.SetRange(['1/1/1960'], ['12/31/1970']);
```

Ranges are *inclusive*, meaning that the endpoints of the range are included within the range. In the preceding example, employees who were born on either January 1, 1960 or December 31, 1970 are included in the range.

To remove the range, simply call CancelRange, like this:

```
ClientDataSet1.CancelRange;
```

# Filters

Unlike ranges, filters do not require an index to be set before applying them. Client dataset filters are powerful, offering many SQL-like capabilities, and a few options that are not even supported by SQL. Tables 3.5–3.10 list the various functions and operators available for use in a filter.

**TABLE 3.5** Filter Comparison Operators

| Function | Description | Example |
| :--- | :--- | :--- |
| = | Equality test | Name = 'John Smith' |
| <> | Inequality test | ID <> 100 |
| < | Less than | Birthday < '1/1/1960' |
| > | Greater than | Birthday > '12/31/1960' |
| <= | Less than or equal to | Salary <= 80000 |
| >= | Greater than or equal to | Salary >= 40000 |
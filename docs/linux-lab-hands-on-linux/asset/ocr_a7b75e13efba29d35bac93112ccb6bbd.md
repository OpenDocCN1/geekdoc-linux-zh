| firstname | lastname | streetaddr | city | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Ramesh | Patil | 10B D N Road | Mumbai | MH | 400058 |
| Mayank | Agarwal | 24 D M 5E B Road | Thane | MH | 400184 |
| Venkat | Raje | 16 F Church Road | Mumbai | MH | 400065 |

The following command displays all records from the name table that have the lastname column set to Jones. Instead of using lastname, you could search for a value from any column name used in the table.

```
mysql> SELECT * FROM name WHERE lastname = "Raje";
```

The output of the preceding command is as follows:

| firstname | lastname | streetaddr | city | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Venkat | Raje | 16 F Church Road | Mumbai | MH | 400065 |

Using the OR operator, you can select records that match several different values. Use the following command, to display records that have either Mayank or Venkat as the firstname:

```
mysql> SELECT * FROM name WHERE firstname = "Mayank" OR firstname =
"Venkat";
```

The table shows the following output:

| firstname | lastname | streetaddr | city | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Mayank | Agarwal | 24 D M 5E B Road | Thane | MH | 400184 |
| Venkat | Raje | 16 F Church Road | Mumbai | MH | 400065 |

To match and display a record based on the value of two columns in a record, you can use the AND operator. Use the following command to display any record that has Mayank as the firstname and Smith as the lastname is matched:

```
mysql> SELECT * FROM name WHERE firstname = "Venkat" AND lastname = "Raje";
```

The following table shows the desired output of the preceding command:

| firstname | lastname | streetaddr | city | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Venkat | Raje | 16 F Church Road | Mumbai | MH | 400065 |
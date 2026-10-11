**Using Quotes.** Quotes are always an issue in programming languages. Should you use a set of single quotes or double quotes, and when should you use them?

SQL uses single quotes around text values (most database systems, including MySQL, also accept double quotes). Numeric values should not be enclosed in quotes.

For text values, this example is correct:

```
`SELECT * FROM Students WHERE FirstName='Marco'`
```

and this example is wrong:

```
`SELECT * FROM Students WHERE FirstName=Marco` _Marco should be “Marco”_
```

For numeric values, this example is correct:

```
`SELECT * FROM Students WHERE Year>2004`
```

and this example is wrong:

```
`SELECT * FROM Students WHERE Year>'2004'` _‘2004’ should be 2004_
```

**Using the = and <> Operators.** In Figure 8.9, the _CompanyName_ and _Phone_ fields are retrieved from the _Customers_ table if the condition following the WHERE clause is true; that is, if the string values in the _Country_ field are exactly equal to the string _Italy_ (they must contain the same number and type of characters). The <> operator can be used to test for “not equal to.”

```
```mysql
mysql> select CompanyName, Phone FROM Customers
       -> WHERE Country='Italy';
+----------------+---------------------+
| CompanyName    | Phone               |
+----------------+---------------------+
| Franchi S.p.A. | 011-49882260        |
| Magazzini Alimentari Riuniti | 035-640230       |
| Reggiani Caseifici | 0522-556721       |
+----------------+---------------------+
3 rows in set (0.00 sec)
```
```

**Figure 8.9** The _WHERE_ clause with the = operator.

**What Is NULL?** NULL means that there is not a value in a field, or it is unknown, but does not mean a value of zero. If a field is _NULL_, it is empty, and if it is _NOT NULL_, it has data. Fields have _NULL_ as a default unless they are specified by _NOT NULL_ in the definition of the table.
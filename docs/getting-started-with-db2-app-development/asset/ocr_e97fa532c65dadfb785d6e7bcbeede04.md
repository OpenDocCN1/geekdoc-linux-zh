| /dept/employee/name/text() | Peter Pan<br>John Doe |
| :--- | :--- |

# Table 2.2 – XPath expression examples

# 2.3.2.2 XPath wildcards

There are two main wildcards in XPath:

+   - `*` matches any tag name
+   
+   - `/` is the "descendant-or-self" wildcard

*Table 2.3* provides more examples using the XML document from *Listing 2.1*

| XPath | Result |
| :--- | :--- |
| /dept/employee/*/text() | John Doe<br>408 555 1212<br>344<br>Peter Pan<br>408 555 9918<br>216 |
| /dept/*/ @id | 901<br>902 |
| //name/text() | Peter Pan<br>John Doe |
| /dept//phone | <phone>408 555 1212</phone><br><phone>408 555 9918</phone> |

# Table 2.3 – XPath wildcard examples

# 2.3.2.3 XPath predicates

Predicates are enclosed in square brackets [ ]. As an analogy, you can think of them as the equivalent to the WHERE clause in SQL. For example `[@id="902"]` can be read as: “WHERE attribute id is equal to 902”. There can be multiple predicates in one XPath expression. To specify a positional predicate, use [n] which means the nth child would be selected. For Example, `employee[2]` means that the second employee should be selected. *Table 2.4* provides more examples.

| XPath | Result |
| :--- | :--- |
| /dept/employee[@id="902"]/name | <name>Peter Pan</name> |
| /dept[@bldg="101"]/employee[office>"300"]/name | <name>John Doe</name> |
| | | | |
| --- | --- | --- | --- |
| //employee[office="344" | OR | 901 |  |
| office="216"]/@id | 902 |  |
| /dept/employee[2]/@id | 902 |  |

Table 2.4 – XQuery predicate examples

# 2.3.2.4 The parent axis

Similar to MS-DOS or Linux/UNIX, you can use a “." (dot) to indicate in the expression that you are referring to the current context, and a “. .” (dot dot) to refer to the parent context. Table 2.5 provides more examples.

| XQuery | Result |
| --- | --- |
| /dept/employee/name[.. /@id="902"] | <name>Peter Pan</name> |
| /dept/employee/office[. >"300"] | <office>344</office> |
| /dept/employee[office > "300"]/office | <office>344</office> |
| /dept/employee[name=. "John Doe"]/.. /@bldg | 101 |
| /dept/employee[name[.= "John Doe"]/.. /.. /@bldg | 101 |

Table 2.5 – XQuery parent axis

# 2.3.3 XQuery basics

XQuery is a query language created for XML. XQuery supports path expressions to navigate the XML hierarchical structure. In fact, XQuery is a subset of XQuery; therefore, everything we learned earlier about XQuery applies to XQuery too. XQuery supports both typed and untyped data. XQuery lacks null values because XML documents omit missing or unknown data. XQuery and XQuery expressions are case sensitive, and XQuery returns sequences of XML data.

XQuery supports the FLWOR expression. If we use SQL for an analogy, it is equivalent to a SELECT-FROM-WHERE expression. The next section describes FLWOR in more detail.

# 2.3.3.1 XQuery: FLWOR expression

FLWOR stands for:

+   - FOR: iterates through a sequence, binds a variable to items
+       - LET: binds a variable to a sequence
+       - WHERE: eliminates items of the iteration
+       - ORDER: reorders items of the iteration
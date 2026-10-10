| TABLE 3.2 | Index Properties | | |

| Property | Description |
| :--- | :--- |
| Name | The name of the index. I recommend prefixing index names with the letters by (as in byName, byState, and so on). |
| Fields | Semicolon-delimited list of fields that make up the index. Example: `ID` or `Name;Salary`. |
| DescFields | A list of the fields contained in the **Fields** property that should be indexed in descending order. For example, to sort ascending by name, and then descending by salary, set **Fields** to `Name;Salary` and **DescFields** to `Salary`. |
| CaseInsFields | A list of the fields contained in the **Fields** property that should be indexed in a manner which is not case sensitive. For example, if the index is on the last and first name, and neither is case sensitive, set **Fields** to `Last;First` and **CaseInsFields** to `Last;First`. |
| GroupingLevel | Used for aggregation. |
| Options | Sets additional options on the index. The options are discussed in Table 3.3. |
| Expression | Not applicable to client datasets. |
| Source | Not applicable to client datasets. |

Table 3.3 shows the various index options that can be set using the **Options** property.

| TABLE 3.3 | Index Options | | |

| Option | Description |
| :--- | :--- |
| `IxPrimary` | The index is the primary index on the dataset. |
| `IxUnique` | The index is unique. |
| `IxDescending` | The index is in descending order. |
| `IxCaseInsensitive` | The index is not case sensitive. |
| `IxExpression` | Not applicable to client datasets. |
| `IxNonMaintained` | Not applicable to client datasets. |

You can create multiple indexes on a single dataset. So, you can easily have both an ascending and a descending index on **EmployeeName**, for example.
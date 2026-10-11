| Type | Meaning |
|---|---|
| UNION RESULT | The result of a UNION |
| SUBQUERY | The first SELECT in a subquery |
| DEPENDENT SUBQUERY | Like SUBQUERY, but dependent on an outer query |
| DERIVED | A subquery in the FROM clause |

+   * table
+      The table to which the output row refers.
+   * partitions
+      The partitions that would be used. This column is displayed only if the PARTITIONS option is present. For non-partitioned tables, the value is NULL.
+   * type
+      The type of join that MySQL will perform. The possible types are, from best to worst: system, const, eq_ref, ref, ref_or_null, index_merge, unique_subquery, index_subquery, range, index, and ALL. The better types are more restrictive, meaning that MySQL has to look at fewer rows from the table when performing the retrieval.
+   * possible_keys
+      The indexes that MySQL considers candidates for finding rows in the table named in the table column. A value of NULL means that no indexes were found.
+   * key
+      The index that MySQL actually will use for finding rows in the table. (There might be several keys listed here if MySQL uses an index_merge join type, because that optimization uses several indexes to process the query.) A value of NULL indicates that no index will be used.
+   * key_len
+      How much of the index will be used. This will be less than the full index row length if MySQL will use a leftmost prefix of the index.
+   * ref
+      The values to which MySQL will compare index values. The word const or '???’ means the comparison is against a constant; a column name indicates a column-to-column comparison.
+   * rows
+      An estimate of the number of rows from the table that MySQL must examine to perform the query. The product of the values in this column is an estimate of the total number of row combinations that must be examined from all tables.
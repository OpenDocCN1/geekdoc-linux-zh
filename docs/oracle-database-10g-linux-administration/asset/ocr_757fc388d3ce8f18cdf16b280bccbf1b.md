but the likelihood of Oracle 10g using the index on TABLE2 is remote at best. Oracle 10g would incur significant amounts of I/O to use this index versus just doing a full table scan.

# Listing 17-3: The Index_Info.sql script

```
* File:             Index_Info.sql
* Type:             SQL*Plus script
* Author:           Jonathan Lewis (www.jlcomp.demon.co.uk)
                    Enhanced by Dan Hotka
* Date:             May 9, 2003
*
* Description:
*
                    This script lists statistics about indexes.
*
*
* Modifications: 10-22-03 Added Table Block and Row info
*
/****/ 
column table_name format a15 heading 'Table'
column index_name format a15 heading 'Index'
column num_rows format 999,999 heading 'Rows'
column num_blocks format 999,999 heading 'Data Blocks'
column avg_data_blocks_per_key format 999,999 heading 'Data Blks per Key'
column avg_leaf_blocks_per_key format 999,999 heading 'Leaf Blks per Key'
column clustering_factor format 999,999 heading 'Clust Factor'

SELECT i.table_name, i.index_name, t.num_rows, t.blocks,
       i.avg_data_blocks_per_key, i.clustering_factor,
       to_char(o.created,'MM/DD/YYYY HH24:MI:SSSSS') Created
  FROM user_indexes i, user_objects o, user_tables t
 WHERE i.index_name = o.object_name
   AND i.table_name = t.table_name
 order by 1;
```
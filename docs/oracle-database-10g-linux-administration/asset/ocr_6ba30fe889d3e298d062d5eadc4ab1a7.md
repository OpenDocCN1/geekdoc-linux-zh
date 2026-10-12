![](bbox=[0.24, 0.12, 0.78, 0.44])

FIGURE 17-1. A simple b-tree index structure

TIP  
Oracle 10g supports multiple block sizes at the tablespace level. The larger the block size, the more key values/ROWIDs you can store per physical read. This means faster index processing for larger objects.

NOTE  
ROWID is made up of four parts that uniquely identify a row and its location within Oracle. The four parts are object ID, file number, block number, and row number. This number is stored in base64 character format. The DBMS_ROWID package is useful to interpret parts of this ROWID field back to meaningful numbers.

When Oracle uses an index for a single-row lookup (an equal condition), it will start at the top branch and navigate through the branch blocks to the leaf block with that key value. In the case of repeating key values, the branch block always points to the left-most leaf block where the key value is found, since Oracle always reads
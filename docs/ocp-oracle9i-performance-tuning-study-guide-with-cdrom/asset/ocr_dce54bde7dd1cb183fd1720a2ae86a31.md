# Contents of the *EMPLOYEE_HISTORY* table

![](bbox=[0.305, 0.14, 0.895, 0.272])

Figure 3.19 shows how the data for this table would be physically stored between the IOT Segment and the IOT Overflow Segment.

# Physical storage of the *EMPLOYEE_HISTORY* data

![](bbox=[0.319, 0.375, 0.897, 0.57])

Notice in Figure 3.19 that the entire row of data associated with employee 107, Gastel, fits into one of the blocks allocated to the *EMPLOYEE HISTORY* IOT. However, employee 112, Macomber, has a title that is too long to fit into the space reserved by PCTTHRESHOLD. Therefore, the row for Macomber is cut off at the INCLUDING column (*FIRST_NAME*), and the remaining row data is instead stored in a block belonging to the overflow segment in another tablespace. Finding the name of this overflow segment is discussed in the following section.

Bitmapmed indexes can be built on both heap and index-organized tables. When a Bitmapmed index is built on a Heap Table, the index stores bitmap along with physical row IDs to locate rows in the Heap Table. However, a Bitmap index on an IOT must make use of a mapping table to locate indexed IOT rows. *The Mapping Table* maps the index’s physical row IDs to
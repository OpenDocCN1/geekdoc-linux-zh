of blocks in an extent is determined by what mode you are running extent management in, as well as the storage parameters.

**Dictionary Managed Tablespace Extent Management**	The traditional method of managing extents is specifying the extent size within the storage clause of the CREATE TABLE or CREATE TABLESPACE statement. Here, you specify the minimum size, the size of the second extent, and the percentage of growth of each additional extent. This allows for larger and larger extents to be created as more space is needed in the object. Although this was very efficient, because of the fact that the tablespace extent information was stored in the data dictionary, there is a lot of overhead associated with it. Because of that, locally managed tablespace extent management was invented.

**Locally Managed Tablespace Extent Management**	Locally managed tablespace extent management manages the tablespace extents within the tablespace itself. Depending on how it is configured the extents are created in either a uniform size or a progressively larger size. This is determined by the UNIFORM or AUTOALLOCATE clauses, which allow the extents to be managed within a bitmap instead of within a table in the Data Dictionary. Although this might lead to the creation of more extents than you would have within dictionary managed tablespaces, the management is simpler and faster. In addition, if the extents are of uniform size, there is not the type of fragmentation experienced in dictionary or autoallocated managed extents. Locally managed tablespaces with autoallocated extents are recommended.

# ## Segments

A segment is simply a collection of extents that make up a particular Oracle object, such as a table, index, and so on. There are several different types of segments as described next:

| Segment Type | Purpose |
| :--- | :--- |
| Data Segments | These are the basic type of segment. The data segment can be used to hold both tables and clusters. |
| Index Segments | Index segments are used to hold indexes. |
| Rollback Segments | Rollback segments are special types of segments that are used to store undo information. Rollback segments have been replaced by undo tablespaces and system managed undo tablespaces. The use of UNDO tablespaces is highly recommended. |
| Temporary Segments | Temporary segments are used for storing temporary data generated during Oracle operations. Temporary segments might be used for sorts or joins. |
# GETTING STARTED

LibreOffice Base

| | | |
|---|---|---|
| TABLE 1: DATABASE FIELDS | | |
| Field Name | Field Type | Description |
| Article | Text [VARCHAR] | Object description |
| Image | Text [VARCHAR] | Image of the object linked to the database by its URL |
| Room | Text [VARCHAR] | Room name |
| Cupboard | Small Integer [SMALLINT] | Cupboard number |
| Rack | Small Integer [SMALLINT] | Rack number |
| Number_Needed | Small integer [SMALLINT] | Number of required objects |
| Category | Text [VARCHAR] | Article type (e.g., electronics, optics, etc.) |

![](bbox=[0.08, 0.27, 0.61, 0.55])

lowing three tables: Every *Article* would be assigned no more than one *Category* and one *Place* (*Room*, *Cupboard*, and *Rack*). In database-speak, this is known as a many-to-one (n:1) relationship, which suffices as long as something is assigned only once. For this example database, however, each article can have multiple storage options and *vice versa* – that is, a many-to-many (n:m) relationship. To ensure this connection, an additional table has a new *ID* created from the *ID* from *Article* and *ID* from *Place*, both primary keys, and with *Number_Needed* moved over from the *Article* table (Figure 2).

# CREATING THE DATABASE

These tables are now created one by one in an internal Firebird database:

+   - Start the Database Wizard in LibreOffice with *File* \| *New* \| *Database*.
+   - Select the *Create a new database* radio button and choose *Firebird Embedded* from the drop-down.
+   - Click *Finish* to save a database file that does not need to be registered. After naming and saving the file, a multi-table window opens; starting in the Tables section and in the Tasks pane, choose *Create Table in Design View*. (To get this one, you need Java. Go to *Tools* \| *Options* \| *Advanced* to see the Java runtime environments that are present on

within the available space, I will describe a typical database scenario and take you through the steps of designing and building the database, then setting up forms and queries. For additional information on working with Base, see the LibreOffice Getting Started Guide \[1\] and the Base Handbook \[2\].

# DESIGNING A DATABASE

The example in this article is a simple database for storing an inventory of equipment for a company. Table 1 shows the basic database fields. The *Article* is a description of the object. The database also includes information on the room where the object is located,

| | |
|---|---|
| TABLE 2: DATABASE TABLES | |
| Article ID | Category ID | Place ID |
| Article | Category | Room |
| Image | | Cupboard |
| Number_Needed | | Rack |

the rack or cupboard number where the object is stored, as well as the category of the object, the number of objects at the location, and the URL to a digital image of the object.

The data in Table 1 could all reside in one table, however, if some fields occur multiple times with the same data, it is often more efficient to split the reoccurring data into a separate table and connect it to the main table by a unique *ID* field assigned as a primary key (Table 2).

A simple inventory database could be compiled with just the fol-

![](bbox=[0.51, 0.77, 0.92, 0.88])
# A.2.1.1.1.1. *Is There a Solution?*

The solution is to standardize the method by which information is retrieved from a file. This is done by creating a well-defined data structure that contains easily searched information about the data, and then physically separating that information from the data.

When the data is required, it is found by using the easily searched information, which points to the data itself. The benefits are that the data can be placed anywhere in the file, and that the format of the data itself can change.

# A.2.1.1.1.2. *The Solution: The Header Structure*

The header structure is RPM’s solution to the problem of easily manipulating information in a standard way. The header structure’s sole purpose in life is to contain zero or more pieces of data. A file can have more than one header structure in it. In fact, an RPM package file has two—the signature and the header. It was from this header that the header structure got its name.

There are three sections to each header structure. The first section is known as the *header structure header*. The header structure header is used to identify the start of a header structure, its size, and the number of data items it contains.

Following the header structure header is an area called the *index*. The index contains one or more index entries. Each index entry contains information about, and a pointer to, a specific data item.

After the index comes the *store*. It is in the store that the data items are kept. The data in the store is packed together as closely as possible. The order in which the data is stored is immaterial—a far cry from the C structure used in the lead.

# A.2.1.1.1.3. *The Header Structure in Depth*

Let’s take a more in-depth look at the actual format of a header structure, starting with the header structure header.

# A.2.1.1.1.4. *The Header Structure Header*

The header structure header always starts with a 3-byte magic number: `8e ad e8`. Following this is a 1-byte version number. Next are 4 bytes that are reserved for future expansion. After the reserved bytes is a 4-byte number that indicates how many index entries exist in this header structure, followed by another 4-byte number indicating how many bytes of data are part of the header structure.

# A.2.1.1.1.5. *The Index Entry*

The header structure’s index is made up of zero or more index entries. Each entry is 16 bytes long. The first 4 bytes contain a *tag*—a numeric value that identifies what type of data is pointed to by the entry. The tag values change according to the header structure’s position in the RPM file. A list of the actual tag values, and what they represent, is included in section A.2.1.3.2.
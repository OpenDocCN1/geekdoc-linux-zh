# 196 Exploring IBM @serverpSeries

Database programs organize information into files, records, and fields. Don't be intimidated by the words. This is exactly how the information in a phone book is structured. Figure 3.5 shows an example telephone book listing and the corresponding computer database structure. The phone book itself is analogous to a file or set of information, also called a database. The information about one person in the phone book would be analogous to a record. The records contain the information for a given entry, and each record contains the same information about its respective field. In this case, a record would contain the name, address, and phone number of person. Each of these items would be analogous to a field within a record. For example, the address part of a phone book entry would be called the address field.

Manually looking up information in a phone book quickly becomes fatiguing. The same is true for manually manipulating any large body of information. The information is entered into a database program, however, it can be retrieved quickly and easily. Databases contain information about store's inventory, a library's books, personnel records, medical records, or virtually any other type of information. Organizations such as banks, airlines, and insurance commonly use extremely large databases by many users. Database applications provide programming languages with which can customize their database environments and develop the interfaces or views needed by various departments within a company or by their customers.

| Information organized by a telephone book | Information organized by a database application program "Database as file" |
| --- | --- |
| (Name) (Address) (Phone #) | "Name" field "Address" field "Phone number" field |
| Record 1 | Packer J. C. 1012 SE 45th St------654-8499 | 1012 SE 45th St 654-8499 |
| Record 2 | Packer O. R. 244 W 13th St------878-2443 | 244 W 13th St 878-2443 |
| Record 3 | Pagano B. R. 667 NW 83rd St------655-0097 | 667 NW 83rd St 655-0097 |

Figure 3.5. (a) The information structure used in a telephone book. (b) The same information organized into a database structure. To efficiently manipulate large amounts of information, it is necessary to first organize the information into a consistent format. The organization used by database applications is not unlike that used in a telephone book.

## Data Structure

In applications where the raw data are already digital, data reduction may consist simply of such operations as adding, scaling, coding, sorting, collating, and tabular summarization.

More typically, the data reduction process is applied to readings or measurements involving random errors. These are the indeterminate errors inherent in the process of assigning values to observational quantities. In such cases, before data may be coded and summarized, the most probable value of a quantity must be determined. Provided the errors are normally distributed, the most probable (or central) value of a set of measurements is given by the arithmetic mean or, in the more general case, by the weighted mean. See STATISTICS.

Data reduction may also involve operations of smoothing and interpolation, because the results of observations and measurements are always given as a discrete set of numbers, while the phenomenon being studied may be continuous in nature.

A means of storing a collection of data. Computer science is in part the study of methods for effectively using a computer to solve problems, or in other words, determining exactly the procedure to be solved. This process entails:
- (1) gaining an understanding of the problem;
- (2) translating vague descriptions, goals, and contradictory requests, and often unstated desires, into a precisely formulated conceptual solution;
- (3) implementing the solution with a computer program.

This solution typically consists of two parts: algorithms and data structures.

### Relation to algorithms
An algorithm is a concise specification of a method for solving a problem. A data structure can be viewed as consisting of a set of algorithms for performing operations on the data it stores. Thus algorithms are part of what constitutes a data structure. In constructing a solution to a problem, a data structure must be chosen that allows the data to be operated upon easily in the manner required by the algorithm.

Data may be arranged and managed at many levels, and the variability in algorithm design generally arises in the manner in which the data for the program are stored; that is:
- (1) how data are arranged in relation to each other,
- (2) which data are calculated as needed,
- (3) which data are kept in memory, and
- (4) which data are kept in files, and the arrangement of the files.

An algorithm may need to put new data into an existing collection of data, remove data from a collection, or query a collection of data for a specific purpose. See ALGORITHM.

### Abstract data types
Each data structure can be developed around the concept of an abstract data type that defines both data organization and data handling operations. Data abstraction is a tool that allows each data structure to be developed in relative isolation from the rest of the solution. The study of data structure is organized around a collection of abstract data types that includes lists, trees, sets, graphs, and dictionaries. See ABSTRACT DATA TYPE.

### Primitive and nonprimitive structures
Data can be structured at the most primitive level, where they are directly operated upon by machine-level instructions. At this level, data may be character or numeric, and numeric data may consist of integers or real numbers.

Nonprimitive data structures can be classified as arrays, lists, and files. An array is an ordered set which contains a fixed number of objects. No deletions or insertions are performed on arrays. At best, elements may be changed. A list, by contrast, is an ordered set consisting of a variable number of elements to which insertions and deletions can be made, and on which other operations can be performed. When a list displays the relationship of adjacency between elements, it is said to be linear; otherwise it is said to be nonlinear. A file is typically a large list that is stored in the external memory of a computer. Additionally, a file may be used as a repository for list items (records) that are accessed infrequently.

### File structures
Not all information that is processed by a computer necessarily resides in immediately accessible memory because some programs and their data cannot fit into the main memory of the computer. Large volumes of data or records and archival data are commonly stored in external memory as entities called files. Any storage other than main memory may be loosely defined as external storage. This includes tapes, disks, and so forth. See COMPUTER STORAGE TECHNOLOGY.

### Virtual memory
This is a system that provides an extension to main memory in a logical sense. In a virtual system, all currently active programs and data are allocated space or virtual addresses in virtual memory. The program and data may not in fact reside in main memory but in an external storage. References to virtual addresses are translated dynamically by the operating system into real addresses in main memory. See DIGITAL COMPUTER.

## Database Management System

A collection of interrelated data together with a set of programs to access the data, also called database system, or simply database. The primary goal of such a system is to provide an environment that is both convenient and efficient to use in retrieving and storing information.

A database management system (DBMS) is designed to manage a large body of information. Data management involves both defining structures for storing information and providing mechanisms for manipulating the information. In addition, the database system must provide for the safety of the stored information, possible system crashes or attempts at unauthorized access. If data are to be shared among concurrent users, the system must avoid possible anomalous results due to multiple users concurrently accessing the same data.

Examples of the use of database systems include airline reservation systems, company payroll and employee information systems, banking systems, credit card processing systems, and sales and order tracking systems.

A major purpose of a database system is to provide users with an abstract view of the data. That is, the system hides certain details of how the data are stored and maintained. Therefore, the user sees a simplified and easy-to-use view of the data. The lowest level of abstraction, the physical level, describes how the data are actually stored and details data structures. The next-higher level of abstraction, the logical level, describes what data are stored, and what relationships exist among those data. The highest level of abstraction, the view level, describes parts of the database that are relevant to each user; application programs used to access a database form part of the view level.

The overall structure of the database is called the database schema. The schema specifies data, data relationships, data semantics, and consistency constraints on the data.

Underlying the structure of a database is the logical data model: a collection of conceptual tools for describing the schema. The entity-relationship data model is based on a collection of basic objects, called entities, and of relationships among these objects. An entity is a “thing” or “object” in the real world that is distinguishable from other objects. For example, each person is an entity, and bank accounts can be considered entities. Entities are described in a database by a set of attributes. For example, the attributes account-number and balance describe one particular account in a bank. A relationship is an association among several entities. For example, a depositor relationship associates a customer with each of her accounts. The set of all entities of the same type and the set of all relationships of the same type are termed an entity set and a relationship set, respectively.

Like the entity-relationship model, the object-oriented model is based on a collection of objects. An object contains values stored in instance variables within the object. An object also contains bodies of code that operate on the object. These bodies of code are called methods. The only way in which one object

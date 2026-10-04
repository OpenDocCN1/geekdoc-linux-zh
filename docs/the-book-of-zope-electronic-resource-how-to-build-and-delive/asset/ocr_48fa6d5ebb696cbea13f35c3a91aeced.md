# 9.2.1 Creating a ZClass

There are four steps to creating a ZClass:

+   1. Create the product with Zone's Control Panel (see section 9.3.1) to house your ZClass and its associated objects. (A single product can hold multiple ZClasses.)
2. Create the ZClass and specify certain information about it as the id and title (see section 9.3.2).
3. Define any property sheets and instance methods for the ZClass (see section 9.3.7).
4. Establish views for the ZClass.

# 9.2.2 Example: CarClass

Suppose you create a ZClass called CarClass that defines the object type Car

> Changes you make to an existing class are applied to all the class's instances; this powerful feature allows you to make sweeping changes across an application from a central point.

# 9.2.2.1 Class Property Example

If you add ISBN_Number to the ZClass Books. an ISBN_Number field is added to each object created (in other words, each book) using this class.

# 9.2.3 Identification Numbers

Each object and ZClass is automatically assigned a unique identification number, or OID, that Zone uses to store the item in the internal Zope Object Database (ZODB). (Do not confuse this with the user-defined id described later.) Normally you do not need to be aware of this internal id.

# 9.2.4 Property Sheets

A property sheet is a list of properties that acts like a container; you create properties (like the properties for a book) on a property sheet. Properties specify the characteristics used to describe an object of your ZClass. Each property has a name, a property value, and a data type.

Data types define the type of property in question, as as text, numeric, and so on, and control the type of data that can be stored in the property, like the data type of a field in a database table. For example, for a property called Title, you would select the string data type. An overview of all the data types is contained in section 3.1.6.
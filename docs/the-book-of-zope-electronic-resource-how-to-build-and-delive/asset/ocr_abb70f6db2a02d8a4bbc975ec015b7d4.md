Another list of strings like the lines type except that this property consists of a single line with each list item separated by a space. This property is useful for storing keywords.

A string type with a discrete set of allowed values, only one of which can be selected at a time. The value field points to a property or method that returns a list of the allowed values (a lines defined in a parent folder or the root is used for this list). Selection properties are represented by a drop-down list on the property sheet.

Like a selection, except that multiple values can be selected at one time. These selected values are kept as a list of strings in the property.

Now establish the properties for Book_description. The book should have the following properties:

+   * title with the string type
* author with the string type
* publisher with the string type
* date_of_publication with the string type
* genre with the selection type
* price with the string type
* delivery_time with the string type

Let's create the title property as an example (see Figure 9-16):

+   1. In the Id field, enter title.
2. Leave the Value field blank. This specifies a blank string as the default value.
3. For the type, select string from the pull-down menu.
4. Click Add to create the first property.

![](bbox=[0.198, 0.623, 0.796, 0.831])

Figure 9-16: Management screen for creating properties

If you enter a value in the Value field, every object you create using ZClass is initially assigned this value for the title property. The Value field creates a default value that can be modified later for each object you create.
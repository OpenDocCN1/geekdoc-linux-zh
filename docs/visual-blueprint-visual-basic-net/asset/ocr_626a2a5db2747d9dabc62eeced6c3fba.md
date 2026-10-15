# DEFINE A PROPERTY

In classes you use, such as forms and controls, properties enable you to specify the details that make up the characteristics of that component. Most classes and components require information to operate and adapt to different functions. You can define properties to let the user of your class specify how your class should perform and which data it uses to perform operations.

To define a property in VB .NET, use the Property... End Property statement block. After the Property keyword, specify the name of the property. Property names follow standard variable-naming techniques. Following the name of the property, you specify an argument list in parentheses. You only define an argument list if the property allows the user to edit a particular index of a list of data. For simple properties, you do not need to specify any arguments. Following the argument list, you specify the variable type of the property using the As keyword.

Inside of the block, the Get... End Get and Set... End Set blocks provide separate blocks of code for when the user of the class retrieves the property and when the user sets the value of the property. A Set block always receives a parameter Value that is of the same type as the property. This variable contains the value the user assigned to the property.

Normal code for a property revolves around a private member variable. For more information on member variables, see the section "Define a Member Variable." In most cases, a property functions as a public access point to a variable the class needs to operate. The class stores the value of this variable in a private variable, and provides the opportunity to change this value through the property, where it can perform error checking and validation. The Set code assigns Value to a private member variable, and Get uses the Return function to return the member variable.

# DEFINE A PROPERTY

![](bbox=[0.05, 0.58, 0.99, 0.84])

+   1. Create a new class or open an existing one.
+   Note: See the section "Create a Class" to create a class.

+   2. Declare a private member variable to hold the property value.
+   Note: See the section "Define a Member Variable" to create a member variable.

+   3. On an empty line inside the Class block, type Property Property1() As String, replacing Property1() with the name of the property and String with the property type.

+   4. Press Enter.
+   If you need parameters for the property, type them after the name inside parentheses.
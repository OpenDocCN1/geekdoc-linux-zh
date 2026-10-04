
Another list of strings like the lines type except that this property consists of a single line with each list item separated by a space. This property is useful for storing keywords.

A string type with a discrete set of allowed values, only one of which can be selected at a time. The value field points to a property or method that returns a list of the allowed values (a lines defined in a parent folder or the root is used for this list). Selection properties are represented by a drop-down list on the property sheet.

Like a selection, except that multiple values can be selected at one time. These selected values are kept as a list of strings in the property.

Now establish the properties for Book_description. The book should have the following properties:

- title with the string type
- author with the string type
- publisher with the string type
- date_of_publication with the string type
- genre with the selection type
- price with the string type
- delivery_time with the string type

Let's create the title property as an example (see Figure 9-16):

1. In the Id field, enter title.
2. Leave the Value field blank. This specifies a blank string as the default value.
3. For the type, select string from the pull-down menu.
4. Click Add to create the first property.

![](img/43a28cce5475b2f487bf455365567fb6_188_0.png)

Figure 9-16: Management screen for creating properties

If you enter a value in the Value field, every object you create using ZClass is initially assigned this value for the title property. The Value field creates a default value that can be modified later for each object you create.

You must specify a property value for any boolean, int, long, float, or date properties. Property types will not accept a blank default value.

create all remaining properties except the genre property. The genre property requires extra explanation, provided in section 9.3.7.2.

# 9.3.7 Creating a Selection or Multiple Selection

To use selection and multiple selection type variables, you must first create a lines property in the root folder, which allows you to use the values from the lines property your ZClass. This property type represents a selection list for a selection or multiple selection type property.

You can also use a DTML method or Python script as the source for the items in a selection list. To use a method, it must return a list of strings. In DTML, you can use the dtml-return tag to accomplish this.

# 9.3.7.1 The Selection Type

The selection type specifies a pull-down menu and contains the values from a lines property contained in a superordinate folder. Only one value can be selected at a time. One example of an object that uses the selection property is a selection list called Delivery with the values Available for Delivery and Not Available for Delivery.

# 9.3.7.2 The Multiple Selection Type

The multiple selection type also specifies a selection list that contains the values from a lines property located in a superordinate folder, but you can select multiples. One example of an object with the multiple selection property is a selection list called "Interests" with the values Sport, Internet, Finance, and Music.

Therefore, to create the Genre property, you first create the necessary lines property as follows:

1. Open the root folder.
2. Click the Properties tab.
3. In the Id field, enter book_genre and select the lines type from the pull-down menu. Leave the Value field blank.
4. Click Add.
5. Enter the following values in the text field for book_genre; each book genre must be on a separate line:

- Romantic Novel
- Science Fiction
- Thriller
- Philosophy
- Short Stories

6. You should now see the screen shown in Figure 9-17.
7. Click Save Changes.

# Folder 2 | View | Properties | Security | Info | Ownership | Edit

Saved changes (2021-05-17 12:00)

| Name | Value | Type |
|---|---|---|
| title | | |
| book_genre | Comic Novel, Science Fiction, Thriller, Philosophy, Short Stories | lines |

Properties also allow you to assign simple values to Zope objects. To change property values, edit the values and "Save Changes".

Save Changes Delete

To add a property, enter a name, type and value for the new property, and click the 'Add' button.

| Name | Type |
|---|---|
| Value | Add |

Figure 9-17: Management screen for the book_genre property

This selection list should now be available throughout the hierarchy beneath your root folder, but it must still be assigned to the genre selection list property. To create the genre property using the selection type, do the following:

1. Go back to the property sheet Book_description in which you have already created the properties title, author, publisher, year of publication, price, and delivery time. (You'll find the values you just entered for book_genre here.)
2. In the id field, enter genre and choose selection from the Type menu. In the Value field, enter book_genre.
3. Click Add.

Zope will create the genre property, which can use the values in the book_genre property as its own. Once you have created all of the properties, your management screen should look like Figure 9-18.

NOTE: The float type is not used for Year of publication; you may need to enter string as well. 

# 9.3.8 Establishing Views

Once you have specified your properties, you will need to establish views for ZClass so that you can manage the properties of book instances. Follow these steps:

1. Click Control Panel and then Sales. The management screen will look like:
2. Click the Views button in the tab bar. Your management screen will look like Figure 9-19.
3. In the Name field, enter Properties and select properpertyheets/Book_description/manage from the pull-down menu. The following items are available:

![](img/43a28cce5475b2f487bf455365567fb6_191_0.png)

Figure 9-19: Management screen for adding views

4. Click Add.

Zope now creates a management tab called Properties, which appears in the tab bar when you click an object in ZClass (visible in Figure 9-20).

| View method | Description |
|---|---|
| manage_unda | Shows the standard information and allows users to perform actions on the object. |
| manage_access | The method used for the Security tab. Allows Zope managers to change permissions and rules. |
| manage_main | The main object management screen. The Contents tab for folderish objects; for non-folderish it is usually the Edit tab. |
| manage_owner | The method used for the Ownership tab. Allows changes to object ownership. |
| properpertyheets/Book_description/manage | The property management interface. Each property sheet your ZClass has its own manage method. |

Figure 9-20: Management screen after creating the view

As you can see from this organization, every class includes all of the data from all of its base classes. And, because the data of the base class is always at the very top of the struct, it is possible to cast a class to any of its base classes. This makes it possible to call the methods of any class in the inheritance, as explained in the next section.

> Note: We are all guilty of allowing some laziness to creep in by not using the terms class and object consistently. Strictly speaking, a class is the definition code that is used to construct an object, while an object is a particular instance of the class. The process of creating an object is instantiation. That is, there is only one definition of the `GtkButton` class, but your program can have dozens of `GtkButton` objects. You will see and hear the term `GtkButton` used when referring to either the class or the object.

# Methods

A method is used to create a new object from a class. For example, a `GtkButton` can be created by this function call:

```
```
GtkWidget *button;
button = gtk_button_new_with_label("Label");
```
```

All functions that create objects have the word `new` in their name. The function `gtk_button_new_with_label()` creates a button that displays the text “Label”. Although the item created is a `GtkButton` object, its address is stored in a `GtkWidget` pointer. This is possible because of an object-oriented capability known as *polymorphism*. Polymorphism simply means that any object can be treated exactly as if it were one of its base classes. Using a `GtkWidget` pointer has some programming advantages because there are so many GUI interface functions that operate on `GtkWidget` objects.

When calling a method to operate on an existing object, the address of the specific object is passed as the first argument. For example, once the button is properly assigned to a position in a container, it can be displayed with the following function call:

```
```
gtk_widget_show(button);
```
```

The pointer data type of `button` is `GtkWidget`, so the function accepts it the same as it does any other widget. The methods of all the classes in the inheritance can be called by using the special casting macros. For example, to change the appearance of the decoration surrounding a button from the default appearance of beveled edges to a simple undecorated button, use the following:

```
```
gtk_button_set_relief(GTK_BUTTON(button), GTK_RELIEF_NONE);
```
```
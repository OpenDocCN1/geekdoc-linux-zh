# Chapter 11 . Swing Components

You may have already come across the term Model-View-Controller (MVC) in other contexts: it's a standard pattern and has been for a long time. Unfortunately, its exact meaning depends on whose book you're reading. For the purpose of understanding JTable, it's important to know what MVC means to the designers of Swing.

In Swing, a component's model is the data that the component presents to a user. A field's model is the text it contains. A combo box's model is the list of values it displays when pulled down. Swing components we have studied so far have all simple models, so it hasn't been necessary to discuss them. But if you check the APIs, you'll see that some of these components have methods called get(), indicating the presence of a model lurking inside the class.

In Swing, a view is the region of the screen dedicated to displaying the current state of the model, the software that supports displaying the model. A view consists of code and pixels. A component's controller is the region dedicated to modifying the state of the model, with the software that supports this activity. A controller also consists of code and pixels. Sometimes a view and controller share pixels. For example, in any text component, the screen region where the component displays its model's text is the region where the user enters new text.

This book isn't going to tell you everything about JTable—there's too much to tell. Here you'll get enough of the basics to get through your project exam. We'll start by saying that when you use JTable, you get to choose the level of complexity which you will operate. Broadly speaking, the levels available to you are:

+   1. Use the methods of the JTable class. Use the standard model.
2. Create your own table class by extending AbstractTableModel.
3. Create your own table class by implementing TableModel.
4. Create your own renderer and editors classes.

Level 1 is the simplest way. You don't get lot of control. The table's appearance is standard. You can change the model by calling the table's setValue() method, whose arguments are row, column number, and a value. Operating at this level is free for many applications that need to display data, but many programmers prefer the flexibility (with some additional cost) of level 2.

At level 2, you control the table's contents by extending the javax.table.AbstractTableModel abstract class provides all the glue that connects the model to its view and controller; all you need to implement a few simple methods to control the model's data. We'll look at how to do this in a moment, but first let's look at levels 3 and 4.

Most people use the level 3 approach by mistake. They see that JTable has a number of methods (as a constructor) that require a TableModel, so they go and implement that interface. This is usually unnecessary work. TableModel defines methods for maintaining the model's data and for communicating with the other's parts. The java.swing.table.AbstractTableModel class implements TableModel, providing perfectly methods for handling the internal communication. If you stick to level 2, you don't to reinvent code; you just have to implement the functionality that is unique to your application. Occasionally situations may call for the level 3 approach, but the Developer's Exam isn't one of those situations.